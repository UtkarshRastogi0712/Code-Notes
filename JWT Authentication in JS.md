#JS/TS 
The flow for JWT Authentication is the same as using [[OAuth2]] in FastAPI. We generate an access token and send the object ID of the user as the payload. The access token is then sent in the Bearer Auth field of the requests that require authentication before allowing access.

### App.js boilerplate:
```Javascript
const express = require("express");
const createError = require("http-errors"); //Create HTTP Errors
require("./Helpers/database");
const { verifyAccessToken, signRefreshToken } = require("./Helpers/token");

const AuthRoutes = require("./Routes/Auth.route");

const app = express();
app.use(express.json());

const PORT = process.env.PORT || 3000;  

//Auth router
app.use("/auth", AuthRoutes);

//Protected Route
app.get("/", verifyAccessToken, async (req, res, next) => {
  res.send("It works!");
});

//Run the server
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
```

### Routes:
- Register makes Mongo Objects with user schema
- Login takes credentials and reply with a JWT token
- Logout just removes JWT from frontend store
- Refresh helps login again by generating new JWT when Auth JWT expires
```Javascript
const express = require("express");
const router = express.Router();

const {
  registerController,
  loginController,
  logoutController,
  refreshTokenController,
} = require("../Controllers/Auth.controller");

router.post("/register", registerController);
router.post("/login", loginController);
router.post("/refresh-token", refreshTokenController);
router.delete("/logout", logoutController);

module.exports = router;
```

### Token creation functions:
Helper function for creating and verifying JWT tokens. 

```Javascript
const JWT = require("jsonwebtoken");
const createError = require("http-errors");

  
//Takes a user id and replies with a short lived JWT for authorisation
const signAccessToken = (user) => {
  return new Promise((resolve, reject) => {
    const payload = {};
    const secret = process.env.ACCESS_TOKEN_SECRET;
    const options = {
      expiresIn: "1h",
      issuer: "localhost:3000",
      audience: user._id.toString(),
    };
    JWT.sign(payload, secret, options, (err, token) => {
      if (err) {
        reject(createError.InternalServerError());
      }
      resolve(token);
    });
  });
};

  
//Takes a user id and reply with a long lasting JWT
const signRefreshToken = (user) => {
  return new Promise((resolve, reject) => {
    const payload = {};
    const secret = process.env.REFRESH_TOKEN_SECRET;
    const options = {
      expiresIn: "1y",
      issuer: "localhost:3000",
      audience: user._id.toString(),
    };
    JWT.sign(payload, secret, options, (err, token) => {
      if (err) {
        reject(createError.InternalServerError());
      }
      resolve(token);
    });
  });
};

  
//Verify JWT by checking with the SECRET and checking for the availablitiy of the bearer JWT
const verifyAccessToken = (req, res, next) => {
  if (!req.headers["authorization"]) return next(createError.Unauthorized());
  const authHeader = req.headers["authorization"];
  const bearerToken = authHeader.split(" ");
  const token = bearerToken[1];
  JWT.verify(token, process.env.ACCESS_TOKEN_SECRET, (err, payload) => {
    if (err) {
      const message =
        err.name === "JSONWebTokenError" ? "Unauthorized" : err.message;
      return next(createError.Unauthorized(message));
    }
    req.payload = payload;
    next();
  });
};

// Unravel the Refresh token to verify user id and return a new access JWT
const verifyRefreshToken = (refreshToken) => {
  return new Promise((resolve, reject) => {
    JWT.verify(
      refreshToken,
      process.env.REFRESH_TOKEN_SECRET,
      (err, payload) => {
        if (err) return reject(createError.Unauthorized());
        const userId = payload.aud;
        resolve(userId);
      }
    );
  });
};

module.exports = {
  signAccessToken,
  signRefreshToken,
  verifyAccessToken,
  verifyRefreshToken,
};
```

### Controller:
```Javascript
const createError = require("http-errors");
const Joi = require("@hapi/joi"); //Used to provide request validation
const { authSchema, loginSchema } = require("../Helpers/req.validators");

const {
  signAccessToken,
  signRefreshToken,
  verifyRefreshToken,
} = require("../Helpers/token");

const {
  registerService,
  findUserByEmail,
} = require("../Services/Auth.service");

const registerController = async (req, res, next) => {
  try {
    const result = await authSchema.validateAsync(req.body);
    const doesExist = await findUserByEmail(result.email);
    if (doesExist) {
      throw createError.Conflict(`${result.email} is already registered`);
    }
    const savedUser = await registerService(
      result.name,
      result.email,
      result.password
    );
    const accessToken = await signAccessToken(savedUser);
    const refreshToken = await signRefreshToken(savedUser);
    res.send({ accessToken, refreshToken });
  } catch (error) {
    if (error.isJoi === true) {
      error.status = 422;
    }
    next(error);
  }
};

const loginController = async (req, res, next) => {
  try {
    const result = await loginSchema.validateAsync(req.body);
    const user = await findUserByEmail(result.email);
    if (!user) {
      throw createError.NotFound("User not found");
    }
    const isMatch = await user.isValidPassword(result.password);
    if (!isMatch) {
      throw createError.Unauthorized("Email or password not valid");
    }
    const accessToken = await signAccessToken(user);
    res.send(accessToken);
  } catch (error) {
    console.error(error);
    if (error.isJoi === true) {
      return next(
        createError.BadRequest("Invalid username, email or password")
      );
    }
    next(error);
  }
};

const refreshTokenController = async (req, res, next) => {
  try {
    const { refreshToken } = req.body;
    if (!refreshToken) {
      throw createError.BadRequest();
    }
    const userId = await verifyRefreshToken(refreshToken);
    const accessToken = await signAccessToken(userId);
    const refToken = await signRefreshToken(userId);
    res.send({ accessToken: accessToken, refreshToken: refToken });
  } catch (error) {
    next(error);
  }
};

const logoutController = async (req, res, next) => {
  res.send("Logout router");
};

module.exports = {
  registerController,
  loginController,
  logoutController,
  refreshTokenController,
};
```

### Services:
```Javascript
const createError = require("http-errors");
const User = require("../Models/User.model");

const registerService = async (name, email, password, callback) => {
  try {
    const user = new User({ name, email, password });
    const savedUser = await user.save();
    return savedUser;
  } catch (error) {
    throw createError.InternalServerError();
  }
};

const findUserByEmail = async (userEmail) => {
  try {
    return await User.findOne({ email: userEmail });
  } catch (err) {
    throw createError.InternalServerError();
  }
};

module.exports = {
  registerService,
  findUserByEmail,
};
```

### Models Schema:
```Javascript
const mongoose = require("mongoose");
const bcrypt = require("bcrypt");
const Schema = mongoose.Schema;

//Object validation
const UserSchema = new Schema({
  name: {
    type: String,
    require: [true, "Please provide a name"],
  },
  email: {
    type: String,
    require: [true, "Please provide a email"],
    unique: true,
    lowercase: true,
  },
  password: {
    type: String,
    require: [true, "Please provide a password"],
    minlength: 6,
  },
  role: {
    type: String,
    default: "user",
    enum: ["user", "admin"],
  },
  createdAt: {
    type: Date,
    default: Date.now,
  },
});

//Executes once before saving the object in Mongo
UserSchema.pre("save", async function (next) {
  try {
    const salt = await bcrypt.genSalt(10);
    this.password = await bcrypt.hash(this.password, salt);
    next();
  } catch (error) {
    next(error);
  }
  next();
});

//DB method defined in Schema
UserSchema.methods.isValidPassword = async function (password) {
  try {
    return await bcrypt.compare(password, this.password);
  } catch (error) {
    throw error;
  }
};

const User = mongoose.model("user", UserSchema);
module.exports = User;
```
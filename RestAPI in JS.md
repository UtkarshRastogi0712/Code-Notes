#JS/TS 
### app.js boilerplate:
```js
const express = require("express");
const createError = require("http-errors");
require("dotenv").config();
const Router = require('./Routes/router.js')
require("./Helpers/database");

const app = express();
const PORT = process.env.PORT || 3000;

app.use(express.json());
app.use(express.urlencoded({ extended: true }));
app.use('/routers', Router)

app.get("/", async (req, res, next) => {
  res.send("It works!");
});

// Catchall error handling
app.use(async (req, res, next) => {
  const error = new Error("Not Found");
  error.status = 404;
  next(error);
});

app.use(async (error, req, res, next) => {
  res.status(error.status || 500);
  res.send({
    error: {
      status: error.status || 500,
      message: error.message,
    },
  });
});

app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
```

All modules of a [RestAPI](RESTful%20APIs) are built using a Route/Controller/Service/Model architecture in [this way](MongoDB%20with%20mongoose)

User Authentication implementation using [JWT](JWT%20Authentication%20in%20JS).
Building a _Front End_ using [[React and Hooks]].
API calls and fetching data using [[Fetch API]]
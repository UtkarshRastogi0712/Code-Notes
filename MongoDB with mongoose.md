#JS/TS #Mongo
Mongoose is a simple framework to interface with MongoDB with a similar implementation for both Javascript/Typescript and Python.

### Connecting to DB:
```javascript
const mongoose = require("mongoose");
const MONGO_URI = process.env.MONGO_URI;

mongoose
  .connect(MONGO_URI, {
    dbName: "lynchpin",
    useNewUrlParser: true,
    useUnifiedTopology: true,
  })
  .then(() => console.log("MongoDB connected..."))
  .catch((err) => console.log(err.message));

mongoose.connection.on("connected", () => {
  console.log("Mongoose connected to DB");
});

mongoose.connection.on("error", (err) => {
  console.log(err.message);
});

mongoose.connection.on("disconnected", () => {
  console.log("Mongoose connection is disconnected");
});

process.on("SIGINT", async () => {
  await mongoose.connection.close();
  process.exit(0);
});
```
### Schema creation:
```typescript
import mongoose, { Schema } from "mongoose";
  
const requestSchema: Schema = new Schema({
  id: {
    type: String,
    required: true,
  },
  certName: {
    type: String,
    required: true,
  },
  userName: {
    type: String,
    required: true,
  },
  orgName: {
    type: String,
    required: true,
  },
  aadharNumber: {
    type: String,
    required: true,
  },
  status: {
    type: String,
    enum: ["REQUESTED", "APPROVED"],
    default: "REQUESTED",
  },
});

export default mongoose.model("Request", requestSchema);
```
### Services for CRUD Routes boilerplate:
```typescript
import Request from "./request.schema";

const createRequest = async (request: any) => {
  try {
    const newRequest = new Request(request);
    const savedRequest = await newRequest.save();
    return savedRequest;
  } catch (err: any) {
    console.error(err);
    throw new Error(err);
  }
};

const getRequest = async (id: string) => {
  try {
    const request = await Request.findOne({ id: id });
    return request;
  } catch (err: any) {
    console.error(err);
    throw new Error(err);
  }
};

const updateRequest = async (id: string, status: string) => {
  try {
    const request = await Request.findOneAndUpdate(
      { id: id },
      { status: status }
    );
    const updatedRequest = await request?.save();
    return updatedRequest;
  } catch (err: any) {
    console.error(err);
    throw new Error(err);
  }
};
 
const deleteRequest = async (id: string) => {
  try {
    const request = await Request.findOne({ id: id });
    const deletedRequest = await request?.deleteOne();
    return deletedRequest;
  } catch (err: any) {
    console.error(err);
    throw new Error(err);
  }
};

export { createRequest, getRequest, updateRequest, deleteRequest };
```

### Controller for CRUD routes:
```typescript
import { Request, Response } from "express";
import {
  createRequest,
  getRequest,
  updateRequest,
  deleteRequest,
} from "./request.services";

const createRequestController = async (req: Request, res: Response) => {
  try {
    const request = await createRequest(req.body);
    res.status(201).json(request);
  } catch (err: any) {
    console.error(err);
    res.status(500).json({ message: err.message });
  }
};

const getRequestController = async (req: Request, res: Response) => {
  try {
    const request = await getRequest(req.params.id);
    if (!request) {
      return res
        .status(200)
        .json({ success: false, message: "Request not found" });
    }
    res.status(200).json({ success: true, data: request });
  } catch (err: any) {
    console.error(err);
    res.status(500).json({ message: err.message });
  }
};

const updateRequestController = async (req: Request, res: Response) => {
  try {
    const Request = await updateRequest(req.params.id, req.params.status);
    res.status(200).json(Request);
  } catch (err: any) {
    console.error(err);
    res.status(500).json({ message: err.message });
  }
};

const deleteRequestController = async (req: Request, res: Response) => {
  try {
    const request = await deleteRequest(req.params.id);
    res.status(200).json(request);
  } catch (err: any) {
    console.error(err);
    res.status(500).json({ message: err.message });
  }
};

export {
  createRequestController,
  getRequestController,
  updateRequestController,
  deleteRequestController,
};
```

### Routing:
```typescript
import { Router } from "express";
import {
  createRequestController,
  getRequestController,
  updateRequestController,
  deleteRequestController,
} from "./request.controller";

const router = Router();

router.post("/", createRequestController);
router.get("/:id", getRequestController);
router.put("/:id", updateRequestController);
router.delete("/:id", deleteRequestController);

export default router;
```
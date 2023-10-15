#JS/TS
FaceIO is a face recognition package on NPM that can be used to quicky implement a face identification in javascript backends.

### Install:
```shell
yarn add faceio/fiojs
npm install faceio/fiojs
```

### Setup:
Create an application on FaceIO console. Store the Public Key as an environment variable to create a faceIO object.

```javascript
import faceIO from "@faceio/fiojs";

const faceio = new faceIO(process.env.REACT_APP_FACEID);
```

### Enroll Users:
```jsx
const enrollNewUser = async () => {
    let promise = faceio.enroll({
      locale: "auto",
      payload: {},
      enrollIntroTimeout: 1,
    });
    promise
      .then((userInfo) => {
        console.log(userInfo);
        setFaceID(userInfo.facialId);
      })
      .catch((errCode) => {
        console.log("Something went wrong");
      });
  };

return(
                <button onClick={enrollNewUser}>
                  REGISTER FOR FACEID
                </button>
);
```
>Attributes:
>- payload: Data sent to FaceIO server to be stored beside the face data
>- enrollIntroTimeout: minimum time for loading the modal before accessing camera
>
>Response:
>- facialID : String UUID of the face data on server

### Delete face using API call:
Fetch the API key from FaceIO console and the face UUID to be deleted. Send a GET request with the two as parameters.
```
"params" : {
	"key" : <API_KEY>
	"fid" : <FACE_UUID>
}

# https://api.faceio.net/deletefacialid?key=<API_KEY>&fid=<FACE_UUID>
```

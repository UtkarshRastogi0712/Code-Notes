OAuth2PasswordBearer is an authorization library that can be used to authorize users to perform certain actions based on a JWT bearer token.

### Basic flow:
- User sends Username and Password to a designated URL for authorization
- The URL verifies the credentials and responds back a JWT token 
- The frontend can store the token with an expiration time
- Next time the frontend requires authorization, it can just use the token for the same


### HTTP Methods:

1. **GET**: Used to retrieve data from a resource.

2. **POST**: Used to create a new resource or perform actions that change the state of a resource.

3. **PUT**: Used to update an existing resource or create it if it doesn't exist.

4. **PATCH**: Used to partially update an existing resource.

5. **DELETE**: Used to remove a resource from the server.

6. **HEAD**: Similar to `GET` but only requests the headers of a resource without the actual data. It is often used for checking resource existence or obtaining metadata.

7. **OPTIONS**: Used to retrieve information about the communication options for the target resource.

8. **CONNECT**: Reserved for establishing network connections to a resource, typically through a proxy server.

9. **TRACE**: Used for diagnostic purposes to retrieve a diagnostic trace of the actions taken by intermediate servers on the way to the target resource.

### HTTP Headers:

1. **Authorization**: Used for authentication and authorization.

2. **Content-Type**: Specifies the media type (e.g., JSON, XML, HTML) of the data in the request or response body.

3. **Accept**: In a client request, it indicates the desired media type for the response.

4. **Content-Length**: Indicates the size of the request or response body in bytes.

5. **Cache-Control**: Specifies caching directives.

6. **Origin**: Used in Cross-Origin Resource Sharing (CORS) to indicate the origin of the requesting site.

7. **User-Agent**: Contains information about the user agent making the request.

8. **Location**: Often used in response headers to provide the URI of a newly created resource or a resource that has been moved.

9. **ETag**: Provides an entity tag for a resource, used for caching and conditional requests.

10. **Allow**: In a response, it lists the HTTP methods that are allowed for the requested resource.

### HTTP Response Status Codes:

1. **1xx (Informational)**:
   - 100 Continue: The request was received, and the client can continue to send the request body.
   - 101 Switching Protocols: The server is switching protocols as requested by the client.

2. **2xx (Successful)**:
   - 200 OK: The request was successful, and the response body contains the requested data.
   - 201 Created: The request was successful, and a new resource was created as a result.
   - 202 Accepted: The request was accepted for processing, but the outcome is not yet known.
   - 204 No Content: The request was successful, but there is no response body.

3. **3xx (Redirection)**:
   - 301 Moved Permanently: The requested resource has been permanently moved to a different URI.
   - 302 Found (or 303 See Other): The requested resource is temporarily located at a different URI.
   - 304 Not Modified: The client's cached version of the resource is still valid.

4. **4xx (Client Error)**:
   - 400 Bad Request: The request was malformed or invalid.
   - 401 Unauthorized: Authentication is required, and the client's credentials are missing or incorrect.
   - 403 Forbidden: The client is authenticated but does not have permission to access the resource.
   - 404 Not Found: The requested resource does not exist.

5. **5xx (Server Error)**:
   - 500 Internal Server Error: An unexpected error occurred on the server.
   - 502 Bad Gateway: The server received an invalid response from an upstream server.
   - 503 Service Unavailable: The server is temporarily unable to handle the request.
   - 504 Gateway Timeout: The server did not receive a timely response from an upstream server.

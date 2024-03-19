# Passing Secret Key in Header

To access the API endpoints securely, you need to include the secret key in the header of your HTTP requests. Follow the steps below:

1. Set the `X-Secret-Key` Header
   Include the `X-Secret-Key` header in your HTTP requests with the secret key as the value. This header is used for authentication and ensures the security of your requests.

# Schedule Posts API

### 1. Insert a New Scheduled Ping

- **Endpoint**: `/sp`
- **Method**: `POST`
- **Request Body**:
  - `channelid`: Channel ID for the scheduled ping (integer)
  - `content`: Content of the scheduled ping (string)
  - `name`: Name of the scheduled ping (string, max 25 characters)
  - `posttime`: Timestamp for when the ping should be posted (integer)

#### Response

- **Success**: 201 Created
  - `message`: Scheduled ping created successfully!

- **Error**:
  - 400 Bad Request: Name can be of maximum 25 characters
  - 401 Unauthorized: Invalid secret key
  - 500 Internal Server Error: Error details

### 2. Fetch All Scheduled Pings

- **Endpoint**: `/sp`
- **Method**: `GET`

#### Response

- **Success**: 200 OK
  - List of scheduled pings in JSON format:
    - `id`: Scheduled ping ID
    - `channelid`: Channel ID
    - `content`: Content of the ping
    - `created`: Timestamp when the ping was created
    - `name`: Name of the ping
    - `posttime`: Scheduled post time
    - `posted`: 'yes' if already posted, 'no' otherwise

- **Error**:
  - 401 Unauthorized: Invalid secret key
  - 500 Internal Server Error: Error details

### 3. Update a Scheduled Ping by ID

- **Endpoint**: `/sp/<int:id>`
- **Method**: `PUT`
- **Request Body**:
  - Same as the request body for creating a new scheduled ping

#### Response

- **Success**: 200 OK
  - `message`: Scheduled ping updated successfully!

- **Error**:
  - 400 Bad Request: Name can be of maximum 25 characters or already posted
  - 401 Unauthorized: Invalid secret key
  - 404 Not Found: Scheduled ping with the specified ID not found
  - 500 Internal Server Error: Error details

### 4. Delete a Scheduled Ping by ID

- **Endpoint**: `/sp/<int:id>`
- **Method**: `DELETE`

#### Response

- **Success**: 200 OK
  - `message`: Scheduled ping deleted successfully!

- **Error**:
  - 401 Unauthorized: Invalid secret key
  - 404 Not Found: Scheduled ping with the specified ID not found
  - 500 Internal Server Error: Error details


# ToDo API

### 1. Insert a New ToDo

- **Endpoint**: `/todo`
- **Method**: `POST`
- **Request Body**:
  - `userid`: User ID for the ToDo (integer)
  - `todo`: ToDo content (string, max 200 characters)

#### Response

- **Success**: 200 OK
  - `message`: ToDo inserted successfully!

- **Error**:
  - 400 Bad Request: ToDo can be of maximum 200 characters
  - 401 Unauthorized: Invalid secret key
  - 500 Internal Server Error: Error details

### 2. Update ToDo by ID

- **Endpoint**: `/todo/<int:id>`
- **Method**: `PUT`
- **Request Body**:
  - Same as the request body for creating a new ToDo

#### Response

- **Success**: 200 OK
  - `message`: ToDo updated successfully!

- **Error**:
  - 400 Bad Request: ToDo can be of maximum 200 characters
  - 401 Unauthorized: Invalid secret key
  - 404 Not Found: ToDo with the specified ID not found
  - 500 Internal Server Error: Error details

### 3. Delete ToDo by ID

- **Endpoint**: `/todo/<int:id>`
- **Method**: `DELETE`

#### Response

- **Success**: 200 OK
  - `message`: ToDo deleted successfully!

- **Error**:
  - 401 Unauthorized: Invalid secret key
  - 404 Not Found: ToDo with the specified ID not found
  - 500 Internal Server Error: Error details

### 4. Fetch ToDo for a User ID

- **Endpoint**: `/todo/<int:userid>`
- **Method**: `GET`

#### Response

- **Success**: 200 OK
  - List of ToDo items for the specified User ID in JSON format:
    - `id`: ToDo ID
    - `userid`: User ID
    - `todo`: ToDo content

- **Error**:
  - 401 Unauthorized: Invalid secret key
  - 500 Internal Server Error: Error details

### 5. Mark ToDo Completed or Partial

- **Endpoint**: `/todo/<int:id>/<status>`
- **Method**: `PUT`
- **Path Parameters**:
  - `id`: ID of the ToDo item (integer)
  - `status`: Updated status for the ToDo item (string, "partial" or "completed")

#### Response

- **Success**: 200 OK
  - `message`: ToDo status updated to {status} successfully

- **Error**:
  - 400 Bad Request: Invalid status. Status must be either 'partial' or 'completed'
  - 401 Unauthorized: Invalid secret key
  - 404 Not Found: ToDo with the specified ID not found
  - 500 Internal Server Error: Error details

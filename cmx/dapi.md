# Passing Secret Key in Header

To access the API endpoints securely, you need to include the secret key in the header of your HTTP requests. Follow the steps below:

1. Set the `X-Secret-Key` Header
   Include the `X-Secret-Key` header in your HTTP requests with the secret key as the value. This header is used for authentication and ensures the security of your requests.

# Schedule Posts API

### 1. Insert a New Scheduled Ping

- **Endpoint**: `/sp`
- **Method**: `POST`
- **Request Body**:
  - `channelid`: Channel ID for the scheduled ping (string)
  - `content`: Content of the scheduled ping (string)
  - `name`: Name of the scheduled ping (string, max 25 characters)
  - `posttime`: Timestamp for when the ping should be posted (string)

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

- **Endpoint**: `/sp/<str:id>`
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

- **Endpoint**: `/sp/<str:id>`
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
  - `guildid`: Guild ID for the ToDo (string)
  - `todo`: ToDo content (string, max 80 characters)
  - `description`: Description of the ToDo (string, max 1024 characters)
  - `user`: User mention (string, max 100 characters)

#### Response

- **Success**: 200 OK
  - `message`: ToDo inserted successfully!

- **Error**:
  - 400 Bad Request: ToDo can be a maximum of 80 characters; Description can be a maximum of 1024 characters; User can be a maximum of 100 characters
  - 400 Bad Request: Missing required parameter
  - 401 Unauthorized: Invalid secret key
  - 500 Internal Server Error: Error details

### 2. Update ToDo by ID

- **Endpoint**: `/todo/<str:id>`
- **Method**: `PUT`
- **Request Body**:
  - `todo`: ToDo content (string, max 80 characters)
  - `description`: Description of the ToDo (string, max 1024 characters)
  - `user`: User mention (string, max 100 characters)

#### Response

- **Success**: 200 OK
  - `message`: ToDo updated successfully!

- **Error**:
  - 400 Bad Request: ToDo can be a maximum of 80 characters; Description can be a maximum of 1024 characters; User can be a maximum of 100 characters
  - 400 Bad Request: Missing required parameter
  - 401 Unauthorized: Invalid secret key
  - 404 Not Found: ToDo with the specified ID not found
  - 500 Internal Server Error: Error details

### 3. Delete ToDo by ID

- **Endpoint**: `/todo/<str:id>`
- **Method**: `DELETE`

#### Response

- **Success**: 200 OK
  - `message`: ToDo deleted successfully!

- **Error**:
  - 401 Unauthorized: Invalid secret key
  - 404 Not Found: ToDo with the specified ID not found
  - 500 Internal Server Error: Error details

### 4. Fetch ToDos for a Guild ID

- **Endpoint**: `/todo/<str:guildid>`
- **Method**: `GET`

#### Response

- **Success**: 200 OK
  - List of ToDo items for the specified Guild ID in JSON format:
    - `id`: ToDo ID
    - `guildid`: Guild ID
    - `todo`: ToDo content
    - `description`: Description of the ToDo
    - `user`: User mention
    - `status`: ToDo status

- **Error**:
  - 401 Unauthorized: Invalid secret key
  - 500 Internal Server Error: Error details

### 5. Mark ToDo Completed, Partial, or Started

- **Endpoint**: `/todo/<str:id>/<status>`
- **Method**: `PUT`
- **Path Parameters**:
  - `id`: ID of the ToDo item (string)
  - `status`: Updated status for the ToDo item (string, "partial", "completed", or "started")

#### Response

- **Success**: 200 OK
  - `message`: ToDo status updated to {status} successfully

- **Error**:
  - 400 Bad Request: Invalid status. Status must be either "partial", "completed", or "started"
  - 401 Unauthorized: Invalid secret key
  - 404 Not Found: ToDo with the specified ID not found
  - 500 Internal Server Error: Error details

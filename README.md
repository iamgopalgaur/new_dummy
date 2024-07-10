# OnTrack-Backend

A Node.js application for managing an online shop, featuring CRUD operations for products, user authentication with JWT, and MongoDB integration.

## Installation

1. Clone this repository into your local system.
2. Go to the installed directory using terminal/command line.
3. Create .env file in the root folder and add all the keys provided in the email to this file.
4. Install the dependencies

```
npm install
```

4. Start the server

```
npm start
```

## Auth Endpoints

1. User signup

```
Endpoint - http://localhost:8080/signup
Request Type - POST
Body
 {
    "email": "abc@xyz.com",
    "username": "abc",
    "phone": "1234567890",
    "password": "mySecretPassword123"
}

cURL -

curl --location 'http://localhost:3000/signup' \
--header 'Content-Type: application/json' \
--data-raw '{
    "email": "abc@xyz.com",
    "username": "abc",
    "phone": "1234567890",
    "password": "mySecretPassword123"
}'
```

2. User Login

```
Endpoint - http://localhost:3000/login
Request Type - POST
Body
 {
    "email": "abc@xyz.com",
    "password": "mySecretPassword123"
}

cURL -

curl --location 'http://localhost:3000/login' \
--header 'Content-Type: application/json' \
--data-raw '{
    "email": "abc@xyz.com",
    "password": "mySecretPassword123"
}'

Response -
{
    "message": "User logged in successfully",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImFiY0B4eXouY29tIiwidXNlcl9pZCI6IjY2OGVjNjEwOTQzODgzOWEyYjZmNWE0ZiIsImlhdCI6MTcyMDYzMjk5OSwiZXhwIjoxNzIwNjM2NTk5fQ.zMoF_pdpjNdcgKSYqOZ0RxfSedICp0ghPeW7sJTkzbY"
}
```

[This token will be used to authenticate all the further requests.]

## Product Endpoints

1. Add new item

```
Endpoint - http://localhost:3000/item
Request Type - POST
Body
{
    "user_id": "abc@xy.com",
    "name": "Item 1",
    "description": "Very good item",
    "price": 8000,
    "quantity": 2
}

cURL -

curl --location 'http://localhost:3000/item' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImFiY0B4eXouY29tIiwidXNlcl9pZCI6IjY2OGVjNjEwOTQzODgzOWEyYjZmNWE0ZiIsImlhdCI6MTcyMDYzMjk5OSwiZXhwIjoxNzIwNjM2NTk5fQ.zMoF_pdpjNdcgKSYqOZ0RxfSedICp0ghPeW7sJTkzbY' \
--data-raw '{
    "name": "Item 1",
    "description": "Very good item",
    "price": 8000,
    "quantity": 2
}'
```

2. Get all items

```
Endpoint - http://localhost:3000/items
Request Type - GET

cURL -

curl --location 'http://localhost:3000/items' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImFiY0B4eXouY29tIiwidXNlcl9pZCI6IjY2OGVjNjEwOTQzODgzOWEyYjZmNWE0ZiIsImlhdCI6MTcyMDYzMjk5OSwiZXhwIjoxNzIwNjM2NTk5fQ.zMoF_pdpjNdcgKSYqOZ0RxfSedICp0ghPeW7sJTkzbY'
```

3. Get item by id

```
Endpoint - http://localhost:3000/item/{itemId}
Request Type - GET
cURL -

curl --location 'http://localhost:3000/item/668e87afd90709df9871190b' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImFiY0B4eXouY29tIiwidXNlcl9pZCI6IjY2OGVjNjEwOTQzODgzOWEyYjZmNWE0ZiIsImlhdCI6MTcyMDYzMjk5OSwiZXhwIjoxNzIwNjM2NTk5fQ.zMoF_pdpjNdcgKSYqOZ0RxfSedICp0ghPeW7sJTkzbY'
```

4. Update item by id

- Only the creator of the item can update it.

```
Endpoint - http://localhost:3000/item/{itemId}
Request Type - PUT
Body
{
    "name": "Pen",
    "description": "Ball pens",
    "price": "20",
    "quantity": "1"
}

cURL -

curl --location --request PUT 'http://localhost:3000/item/668e87afd90709df9871190b' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImFiY0B4eXouY29tIiwidXNlcl9pZCI6IjY2OGVjNjEwOTQzODgzOWEyYjZmNWE0ZiIsImlhdCI6MTcyMDYzMjk5OSwiZXhwIjoxNzIwNjM2NTk5fQ.zMoF_pdpjNdcgKSYqOZ0RxfSedICp0ghPeW7sJTkzbY' \
--data '{
        "name": "Pen",
        "description": "Ball pens",
        "price": "20",
        "quantity": "1"
    }'

```

5. Delete Item by Id

- Only the creator of the item can delete it.

```
Endpoint - http://localhost:3000/item/itemId
Request Type - DELETE

cURL -

curl --location --request DELETE 'http://localhost:3000/item/668ec94d9438839a2b6f5a55' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImFiY0B4eXouY29tIiwidXNlcl9pZCI6IjY2OGVjNjEwOTQzODgzOWEyYjZmNWE0ZiIsImlhdCI6MTcyMDYzMjk5OSwiZXhwIjoxNzIwNjM2NTk5fQ.zMoF_pdpjNdcgKSYqOZ0RxfSedICp0ghPeW7sJTkzbY'
```

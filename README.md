# ChatWave

A real-time chat application built with Node.js, Express, and WebSockets. This app includes a server-side implementation with an interactive chat feature, multiple user rooms, and message storage. It enables users to create, join, rename, and delete rooms, with full message history available in each room.

## Features

- **User Authentication**: Users set their username (stored in `localStorage`).
- **Messaging**: Each message displays the author, timestamp, and message text.
- **Rooms Management**: Users can create, rename, join, and delete rooms.
- **Persistent Messages**: All previous messages are visible in a room when a user joins.

## Endpoint Routing Scheme
```
GET    /rooms              # Get all rooms
POST   /rooms              # Create a new room
PATCH  /rooms/:roomId      # Rename a room
DELETE /rooms/:roomId      # Delete a room

GET    /messages/:roomId   # Get all messages in a room
POST   /messages/:roomId    # Send a message in a room
```

## Database Schema

### Users
| Column    | Type                      |
|-----------|---------------------------|
| id        | SERIAL PRIMARY KEY        |
| username  | VARCHAR(255) UNIQUE       |
| createdAt | TIMESTAMP DEFAULT NOW()   |
| updatedAt | TIMESTAMP DEFAULT NOW()   |

### Rooms
| Column    | Type                      |
|-----------|---------------------------|
| id        | SERIAL PRIMARY KEY        |
| name      | VARCHAR(255) UNIQUE       |
| createdAt | TIMESTAMP DEFAULT NOW()   |
| updatedAt | TIMESTAMP DEFAULT NOW()   |

### Messages
| Column    | Type                              |
|-----------|-----------------------------------|
| id        | SERIAL PRIMARY KEY                |
| userId    | INTEGER REFERENCES Users(id)      |
| roomId    | INTEGER REFERENCES Rooms(id)      |
| text      | TEXT                              |
| time      | TIMESTAMP DEFAULT NOW()           |


## Prerequisites

1. **Node.js**: Make sure Node.js is installed. [Download Node.js](https://nodejs.org/).
2. **PostgreSQL**: Ensure PostgreSQL is installed and running. [Download PostgreSQL](https://www.postgresql.org/download/).
3. **pgAdmin** (Optional): For easy database management, pgAdmin is recommended. [Download pgAdmin](https://www.pgadmin.org/download/).

## Setup Instructions

1. **Clone the repository**:
   ```bash
   git clone https://github.com/yourusername/ChatWave.git
   cd ChatWave
   ```

## Set up the database

1. **Create a PostgreSQL database.**
2. **Configure your database connection** in `databaseSetup.js`.
3. **Run the setup script**:
   ```bash
   node databaseSetup.js
  ```
## Start the server

1. **Run the server**:
   ```bash
   npm start
  ```
## Access the application

Open your browser and go to [http://localhost:3000](http://localhost:3000).

## Environment Variables

Create a `.env` file in the root directory with the following environment variables:

```plaintext
PORT=yourport
DB_HOST=localhost
DB_USER=postgres
DB_PASSWORD=yourpassword
DB_DATABASE=postgres
CLIENT_HOST=http://localhost:3000
```


# Dockerfile Practice for a Node.js Application

This task will guide you through creating a Dockerfile for a simple Node.js application. By following the steps, you will gain hands-on experience with various Dockerfile instructions.

## Prerequisites

- Basic understanding of Docker and Dockerfiles.
- Node.js installed on your local machine.
- Docker installed on your local machine.

## Steps

### 1. Setup Project Directory

Create a new directory for your project and navigate into it.

```sh
mkdir node-docker-app
cd node-docker-app
```

### 2. Create a Simple Node.js Application

Create a `package.json` file:

```json
{
  "name": "node-docker-app",
  "version": "1.0.0",
  "description": "A simple Node.js app to practice Dockerfile",
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  },
  "dependencies": {
    "express": "^4.17.1"
  }
}
```

Create an `app.js` file:

```js
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => {
  res.send('Hello World!');
});

app.listen(port, () => {
  console.log(`App running on port ${port}`);
});
```

### 3. Create the Dockerfile

In the project directory, create a file named `Dockerfile` and add the following instructions one by one as described in the steps below.

### 4. Use a Base Image

Start by specifying the base image using the `FROM` instruction.

```dockerfile
FROM node:14
```

### 5. Set Working Directory

Use the `WORKDIR` instruction to set the working directory inside the container.

```dockerfile
WORKDIR /usr/src/app
```

### 6. Copy Application Files

Use the `COPY` instruction to copy `package.json` and `package-lock.json` (if available) to the working directory.

```dockerfile
COPY package*.json ./
```

### 7. Install Dependencies

Use the `RUN` instruction to install the application dependencies.

```dockerfile
RUN npm install
```

### 8. Copy Application Code

Copy the rest of the application code to the container.

```dockerfile
COPY . .
```

### 9. Set Environment Variables

Use the `ENV` instruction to set an environment variable.

```dockerfile
ENV NODE_ENV=production
```

### 10. Expose Application Port

Use the `EXPOSE` instruction to specify the port the application will listen on.

```dockerfile
EXPOSE 3000
```

### 11. Specify Default Command

Use the `CMD` instruction to specify the command to run the application.

```dockerfile
CMD ["node", "app.js"]
```

### 12. Build the Docker Image

In your terminal, run the following command to build the Docker image:

```sh
docker build -t node-docker-app .
```

### 13. Run the Docker Container

Run a container from the built image:

```sh
docker run -p 3000:3000 node-docker-app
```

### 14. Verify the Application

Open your browser and navigate to `http://localhost:3000`. You should see "Hello World!" displayed.

## Complete Dockerfile Example

Here's what your final `Dockerfile` should look like:

```dockerfile
# Use an official Node runtime as a parent image
FROM node:14

# Set the working directory
WORKDIR /usr/src/app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Set environment variables
ENV NODE_ENV=production

# Expose the application port
EXPOSE 3000

# Specify the command to run the application
CMD ["node", "app.js"]
```

## Additional Challenges

1. **Use ARG and ENV:**
   Modify the Dockerfile to use an `ARG` for the Node.js version and pass it to the `FROM` instruction.

2. **Add Health Check:**
   Add a `HEALTHCHECK` instruction to periodically check if the application is running.

3. **Create a Volume:**
   Use the `VOLUME` instruction to create a volume for the application logs.

4. **Run as a Non-Root User:**
   Add a `USER` instruction to run the application as a non-root user.

This task covers most of the basic and some advanced Dockerfile instructions. By completing it, you'll gain practical experience in creating and optimizing Dockerfiles for Node.js applications.

ARG NODE_VERSION=19.0.0-alpine3.16

FROM node:${NODE_VERSION} as builder

# Set the working directory inside the container
WORKDIR /usr/src/app

# Copy package.json and package-lock.json to the container
COPY package*.json ./

# Install dependencies
RUN npm install --production

# Copy the rest of the application code
COPY . .

FROM node:${NODE_VERSION} as runner

WORKDIR /usr/src/app

COPY --from=builder /usr/src/app /usr/src/app

# Expose port 5000
EXPOSE 5000

# Command to run the Node.js application
CMD ["npm", "start"]

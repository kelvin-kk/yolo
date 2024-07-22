ARG NODE_VERSION=19.0.0-alpine3.16

FROM node:${NODE_VERSION} as builder

# Set the working directory inside the container
WORKDIR /usr/src/app

ENV NODE_OPTIONS=--openssl-legacy-provider

# Copy package.json and package-lock.json to the container
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install --production

# Copy the rest of the application code
COPY . .

RUN npm run build

FROM node:${NODE_VERSION} as runner

WORKDIR /usr/src/app

ENV NODE_OPTIONS=--openssl-legacy-provider

COPY --from=builder /usr/src/app/package.json ./
COPY --from=builder /usr/src/app/build ./build
COPY --from=builder /usr/src/app/node_modules ./node_modules

# Expose port 
EXPOSE 3000

# Command to run the Node.js application
CMD ["npm", "start"]
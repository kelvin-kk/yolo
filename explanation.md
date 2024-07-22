# YOLO IP2 E-COMMERCE WEBSITE
![image](/images/yolo_website.png)

# Overview
This is a README file for an e-Commerce website that doubles-up as a dashboard where you can load retail products on to the site.


# Base Image
This application has been built with React for the frontend and Node.js with Express for the backend therefore the below base image is best suited

+ `NODE_VERSION`=`19.0.0-alpine3.16`


# Dockerfile Directives
```
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

# Expose port
EXPOSE 5000

# Command to run the Node.js application
CMD ["npm", "start"]

```

# Docker Compose Networking
All containers are connected to the yolo-ip2-network bridge network
```
services:
  backend:
    networks:
      - yolo-ip2-network
    ports:
      - "5000:5000"

  frontend:
    image: kelvin09/yolo-client:v1.0.0
    networks:
      - yolo-ip2-network  
    ports:
      - "3000:3000"

networks:
  yolo-ip2-network:
    driver: bridge
```

# Docker-Compose volume definition 
```
    volumes:
      - ./client:/usr/src/app
      - /usr/src/app/node_modules
```

# Building the docker image
```
sudo docker build -t kelvin09/yolo-backend:v1.0.0 . --push

sudo docker build -t kelvin09/yolo-client:v1.0.0 . --push
```

# Running the images
```
docker-compose up -d
```

#   Images / Screenshots

### Docker Containers
![image](/images/docker_containers.png)

### Docker Images
![image](/images/docker_images.png)

### Docker Hub
![image](/images/dockerhub.png)

#### Docker Hub Backend
![image](/images/docker_hub_backend.png)

#### Docker Hub Frontend
![image](/images/docker_hub_client.png)

### Added Products
![image](/images/products.png)








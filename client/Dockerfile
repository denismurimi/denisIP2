# Use the official Node.js Alpine base image
FROM node:alpine3.18

# Set the working directory in the container
RUN mkdir -p /application/client
WORKDIR /application/client

# Copy the package.json files to the working directory
COPY package*.json /application/client

# Install the application dependencies
RUN npm install --silent

# Copy the remaining application files to the working directory
COPY . /application/client

# Command to run the app when the container starts
CMD ["npm", "start"]

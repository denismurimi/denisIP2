# Use the official Node.js Alpine base image
FROM node:alpine3.18

# Set the working directory in the container
RUN mkdir -p /srv/app/admin-client
WORKDIR /srv/app/admin-client

# Copy the package.json files to the working directory
COPY package*.json ./

# Install the application dependencies
RUN npm install --silent

# Copy the remaining application files to the working directory
COPY . .

# Command to run the app when the container starts
CMD ["npm", "start"]

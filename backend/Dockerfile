# Use the official Node.js Alpine base image
FROM node:alpine3.18

# Set the working directory in the container
WORKDIR /srv/app/admin-server

# Copy the package.json and package-lock.json (if they exist) files to the working directory
COPY package*.json ./

# Install the application dependencies
RUN npm install --silent

# Copy the remaining application files to the working directory
COPY . .

# Command to run the application when the container starts
CMD ["npm", "start"]

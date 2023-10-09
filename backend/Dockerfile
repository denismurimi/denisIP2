#Using a node alpine image
FROM node:alpine3.18

# setting the working directory
RUN mkdir -p /application/server
WORKDIR /application/server

# Copying the package.json file to the working directory
COPY package*.json /application/server

# Installing the dependencies
RUN npm install --silent

# Copying the resr of the files to the working directory
COPY . /application/server

# Running the app
CMD ["npm", "start"]

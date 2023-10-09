Choice of the base image:

The base image chosen in this Dockerfile is node:alpine3.18. This means that the Docker image will be built on top of the Alpine Linux distribution and will include Node.js as the runtime environment. Alpine Linux is known for its small image size, making it a popular choice for minimizing the image size and improving container startup time.

Dockerfile directives used in the creation and running of each container:

FROM node:alpine3.18: Specifies the base image as Node.js on Alpine Linux.
RUN mkdir -p /application/client: Creates a directory named /application/client inside the container.
WORKDIR /application/client: Sets the working directory to /application/client. All subsequent commands will be executed in this directory.
COPY package*.json /application/client: Copies the package.json and package-lock.json files (if they exist) from the host machine to the /application/client directory in the container. This is typically done before running npm install to take advantage of Docker layer caching for dependencies.
RUN npm install --silent: Installs Node.js dependencies from the package.json file using npm install. The --silent flag is used to suppress the output for a cleaner build log.
COPY . /application/client: Copies the rest of the application source code and files from the host machine to the /application/client directory in the container.
CMD ["npm", "start"]: Specifies the default command to run when a container is started. In this case, it runs npm start, which is typically used to start a Node.js application.

Docker Compose Networking:

Backend Service:

expose is used to expose port 5000 inside the container. It doesn't publish the port to the host, but it allows other services in the same network to access this port.
ports maps port 6000 on the host to port 5000 in the container. This means that you can access the backend service from the host machine on port 6000, and traffic will be directed to port 5000 inside the container.
networks specifies that the "backend" service is part of the "yolo-network" bridge network. This allows the "backend" service to communicate with other services in the same network using service names as hostnames (e.g., "client" can reach "backend" at "http://backend:5000").
Client Service:

expose is used to expose port 3000 inside the container. Like with the backend, it doesn't publish the port to the host but allows other services in the same network to access this port.
ports maps port 3000 on the host to port 3000 in the container. This means you can access the client service from the host machine on port 3000, and traffic will be directed to port 3000 inside the container.
networks also specifies that the "client" service is part of the "yolo-network" bridge network, allowing it to communicate with other services in the same network.
Docker Compose Volume Definition and Usage:

Backend Service:

volumes maps the local ./backend/src directory on the host to /application/server/src in the container. This is a volume mount that allows the container to access the source code from the host. Changes made in the host's ./backend/src directory will be reflected in the container's /application/server/src directory.
Client Service:

volumes maps two local directories on the host to directories in the container:
./client/src is mapped to /application/client/src. This allows the container to access the client application source code from the host.
./client/public is mapped to /application/client/public. This allows the container to access the client's public directory from the host.



Git workflow used to achieve the task.
Fork a Git Repository:
Start by forking a Git repository on a hosting platform like GitHub, GitLab, or Bitbucket. Initialize a Git repository for your project locally if you haven't already.

Clone the Repository:
Clone the repository to my local development environment using the git clone command.
Develop and Push:
Developed and Pushed my work to the remote repository.


Application did run successfully


Screenshots added on the root folder



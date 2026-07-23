FROM node:20.20.2-alpine3.22 AS builder
# creates /app and set the directory to /app
WORKDIR /app
COPY package.json .
COPY *.js .
# node_modules, dependencies
RUN npm install 

FROM node:20.20.2-alpine3.22
WORKDIR /app
EXPOSE 8080
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"

# Create a system group and a system user without a password
# running container with non-root user, If your Node.js application runs as root inside the container and an attacker finds a 
# vulnerability (like a Remote Code Execution in your code or dependencies), they gain root privileges inside the container. In some 
# container escape scenarios, this can allow an attacker to gain root control over the host server itself.
# addgroup -S appgroup && adduser -S -G appgroup  appuser 
RUN addgroup -S roboshop && adduser -S -G roboshop  roboshop 

# changing the file ownership of the /app directory from root to roboshop.
# Docker defaults to running all commands as the root user, those copied files belong to root. The roboshop user does not own them yet.
# If you don't run chown first, roboshop will try to run server.js against files owned by root. If your Node app needs to write log 
# files, create temporary files, or update anything inside /app, it will crash with a Permission Denied (EACCES) error.

# Because only root has the power to change ownership of files, root runs this command to give full ownership of /app to roboshop
RUN chown -R roboshop:roboshop /app
COPY --from=builder /app /app

#You switch from the root user to the roboshop user for all future commands and container runtime.
USER roboshop

#Without a CMD instruction, Docker will build the image, but when you try to run it using docker run, Docker won't know what to 
#execute and the container will immediately exit.
CMD ["node", "server.js"]

# FROM node:20
# # this creates /app and move there    
# WORKDIR /app
# COPY package.json .
# COPY *.js .
# EXPOSE 8080
# RUN npm install
# ENV MONGO="true" \
#     MONGO_URL="mongodb://mongodb:27017/catalogue"
# CMD ["node", "server.js"]
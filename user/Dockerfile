FROM node:20.20.2-alpine3.22 AS builder
# creates /app and set the directory to /app
WORKDIR /app
COPY package.json .
COPY *.js .
# node_modules
RUN npm install 

FROM node:20.20.2-alpine3.22
EXPOSE 8080
WORKDIR /app
RUN addgroup -S roboshop && adduser -S -G roboshop roboshop && \
    chown -R roboshop:roboshop /app
COPY --from=builder /app /app
USER roboshop
CMD ["node", "server.js"]




# FROM node:20

# WORKDIR /app 

# # copying package.json into . (current directory /app)
# COPY package.json . 
# COPY *.js .

# RUN npm install
# EXPOSE 8080

# # ExecStart=/bin/node /app/server.js
# # In a Systemd service file, ExecStart specifies the exact command that runs to start the service.
# CMD ["node", "server.js"]
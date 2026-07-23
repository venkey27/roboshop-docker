FROM node:20.20.2-alpine3.22 AS builder
# creates /app and set the directory to /app
WORKDIR /app
COPY package.json .
COPY *.js .
# node_modules, dependencies
RUN npm install 

FROM node:20.20.2-alpine3.22
WORKDIR /app
COPY --from=builder /app /app
EXPOSE 8080
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"

# Create a system group and a system user without a password
# addgroup -S appgroup && adduser -S -G appgroup  appuser 
RUN addgroup -S roboshop && adduser -S -G roboshop  roboshop 

# giving ownership for /app is roboshop
RUN chown -R roboshop:roboshop /app
USER roboshop
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
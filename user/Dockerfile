FROM node:20

WORKDIR /app 

# copying package.json into . (current directory /app)
COPY package.json . 
COPY *.js .

RUN npm install
EXPOSE 8080

# ExecStart=/bin/node /app/server.js
# In a Systemd service file, ExecStart specifies the exact command that runs to start the service.
CMD ["node", "server.js"]
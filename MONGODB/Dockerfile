FROM mongo:7.0

#copying .js files in local to /docker-entrypoint-initdb.d/ location
# then mongodb, When a container is started for the first time it will execute files with 
# extensions .sh and .js (master-data.js) in /docker-entrypoint-initdb.d/ location, so data will be loaded
COPY *.js /docker-entrypoint-initdb.d/
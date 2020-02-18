# what is the base image we are using
FROM node:latest

# define some environment variables
ENV DB_HOST=nwdb
ENV DB_PORT=3306
ENV DB_USER=root
ENV DB_PASSWORD=changeit
ENV APP_PORT=3000
ENV APP_ROOT=/app

# create the $APP_ROOT directory
# go inside the directory
WORKDIR ${APP_ROOT}

# Copy app sources from local
# into ${APP_ROOT}
ADD main.js .
ADD package-lock.json .
ADD package.json .
ADD public public
ADD views views
ADD config config

# install dependencies
# this will use package.json
RUN npm install

# configure healthchecks
HEALTHCHECK --interval=30s --timeout=30s --start-period=5s --retries=3 CMD curl -s -f http://localhost:${APP_PORT}/health > /dev/null || exit 1

# what port is the application using
EXPOSE ${APP_PORT}

# how to run the program
ENTRYPOINT [ "node", "main.js" ]

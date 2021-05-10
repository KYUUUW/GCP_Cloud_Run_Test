# GCP Cloud Run practice

## Source

* `process.env.PORT` environment - The port your HTTP server should listen on.

## Docker

`Dockerfile`

```docker
# Use the official lightweight Node.js 14 image.
# https://hub.docker.com/_/node
FROM node:14-slim

# Create and change to the app directory.
WORKDIR /usr/src/app

# Copy application dependency manifests to the container image.
# A wildcard is used to ensure copying both package.json AND package-lock.json (when available).
# Copying this first prevents re-running npm install on every code change.
COPY package*.json ./

# Install production dependencies.
# If you add a package-lock.json, speed your build by switching to 'npm ci'.
# RUN npm ci --only=production
RUN npm install --only=production

# Copy local code to the container image.
COPY . ./

# Run the web service on container startup.
CMD [ "node", "index.js" ]
```

`.dockerignore`

```
Dockerfile
.dockerignore
node_modules
npm-debug.log
```

`docker build . -t <docker_user>/<image_name>`

`docker run -db <out_port>:<inner_port> <docker_user>/<image_name>`

`docker push -t <docker_user>/<image_name>`

`docker.io/<docker_user>|library/<image_name>:latest`

## gcloud

`gcloud config set project <project_name>`

`gcloud builds submit --tag [gcr.io/<path>/<image_name>](http://gcr.io/snappy-premise-231900/helloworld)`

GCR 에서 URL 확인

`gcloud run deploy --image <URL> --platform managed`
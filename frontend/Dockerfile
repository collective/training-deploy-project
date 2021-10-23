FROM node:14-slim as base
FROM base as builder

# Create app directory
WORKDIR /usr/src/app

RUN apt-get update \
    && buildDeps="python3 build-essential" \
    && apt-get install -y --no-install-recommends $buildDeps\
    && rm -rf /var/lib/apt/lists/*

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package.json yarn.lock  ./
RUN yarn install --prod

# Bundle app source
COPY . .

RUN yarn build

FROM base

LABEL maintainer="Plone Community" \
      org.label-schema.name="plone" \
      org.label-schema.description="Plone 6 frontend site." \
      org.label-schema.vendor="Plone Community" \
      org.label-schema.docker.cmd="docker run -d -p 3000:3000 plone/project:latest"

WORKDIR /usr/src

COPY --from=builder /usr/src/app .

WORKDIR /usr/src/app

EXPOSE 3000

CMD ["yarn", "start:prod"]

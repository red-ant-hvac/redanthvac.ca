# syntax=docker/dockerfile:1.4

FROM node:lts AS development

ENV CI=true
ENV PORT=14514

WORKDIR /code
RUN npm install react-router-dom
COPY package.json /code/package.json
COPY package-lock.json /code/package-lock.json
RUN npm ci
COPY . /code

CMD [ "npm", "start" ]

FROM development AS builder

RUN npm run build

# FROM development as dev-envs
# RUN <<EOF
# apt-get update
# apt-get install -y --no-install-recommends git
# EOF

# RUN <<EOF
# useradd -s /bin/bash -m vscode
# groupadd docker
# usermod -aG docker vscode
# EOF
# # install Docker tools (cli, buildx, compose)
# COPY --from=gloursdocker/docker / /
# CMD [ "npm", "start" ]

# FROM nginx:1.13-alpine

# COPY --from=builder /code/build /usr/share/nginx/html

# install bash and attach to container
RUN <<EOF
apt-get update
apt-get install -y --no-install-recommends bash
EOF

# after docker compose up, attach to container by running
# docker exec -it <container_id> bash
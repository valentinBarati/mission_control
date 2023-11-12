#CMD ["tail", "-f", "/dev/null"]
FROM node:lts-alpine

RUN apk --no-cache update && apk add wget
RUN apk --no-cache add git \
    mc \
    openssh

WORKDIR /home/app

EXPOSE 80

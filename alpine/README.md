## Usage
Use like you would any other base image:
```
FROM wanlay:alpine
RUN apk add --no-cache mysql-client
ENTRYPOINT ["mysql"]
```
This example has a virtual image size of only 36.5MB. Compare that to our good friend Ubuntu:
```
FROM ubuntu:16.04
RUN apt-get update \
    && apt-get install -y --no-install-recommends mysql-client \
    && rm -rf /var/lib/apt/lists/*
ENTRYPOINT ["mysql"]
```
This yields us a virtual image size of about 184MB image.

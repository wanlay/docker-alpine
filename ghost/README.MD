# Dockerfile
[Dockerfile](https://github.com/wanlay/dockerfile/blob/master/ghost/Dockerfile)
# How to use this image
This will start a Ghost instance listening on the default Ghost port of 2368.
`$ docker run -d --name some-ghost wanlay/ghost`
# SQLite Database
This Docker image for Ghost uses SQLite. There is nothing special to configure.
# Docker Volume
`/ghost/content`
# Environment
## deploy address
default:  ADDRESS=https://my-ghost-blog.com  
example: `-e ADDRESS=https://my-ghost-blog.com`
## ISSO    
default: ENABLE_ISSO=False  
         ISSO_HOST=isso.domain.tld  
         ISSO_AVATAR=false  
         ISSO_VOTE=false 
## DISQUS
default: ENABLE_DISQUS=False 
         DISQUS_SHORTNAME=shortname
# docker-compose
```yaml
version: "2"
services:
  blog:
    image: wanlay/ghost:latest
    restart: on-failure:10
    ports:
      - "2368:2368"    # 
    volumes:
      - ghost-volume:/ghost/content
    environment:
      - ADDRESS=http://10.0.0.0:2368   #this port is changed with ports
volumes:
    ghost-volume:
```
# netmicroservices


https://hub.docker.com/

Start a mongo server instance
- $ docker run --name some-mongo -d mongo:tag
- docker run -d -p 27017:27017 --name shopping-mongo mongo
- docker logs -f shopping-mongo
- docker exec -it shopping-mongo /bin/bash

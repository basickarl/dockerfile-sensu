# dockerfile-sensu

#####Ubuntu 14.04 Sensu Dockerfiles
These Dockerfiles should work out of the box after building and running the images created.

#### sensu-core
Doesn't do anything on it's own. This Dockerfile is required to be built as the other Dockerfiles use the image. Build this first before building any of the Dockerfiles below.

####sensu-server
Installs and configures `Redis`, `RabbitMQ` and `Uchiwa`. No client checks on the server. 

####sensu-server-client 
Installs and configures `Redis`, `RabbitMQ` and `Uchiwa`. Client checks on the server.

To build this file you must build [sensu-server](#sensu-server) first as it uses it for building.

### Bugs

Plz tell me.

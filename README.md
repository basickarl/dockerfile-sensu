# dockerfile-sensu

#####Ubuntu 14.04 Sensu Dockerfiles
These Dockerfiles should work out of the box after building and running the images created.

All Dockerfiles come with example configurations and the created images are started with `supervisor`. 

Find the official Sensu documentation useless? Take a look at the Dockerfiles with the configuration files and you'll understand more.

### Core Dockerfile

#### sensu-core
Installs `Sensu core`. Doesn't do anything on it's own. This Dockerfile is required to be built as the other Dockerfiles use the image. Build this first before building any of the Dockerfiles below.

### Server Dockerfiles

####sensu-server
Installs and configures `Redis`, `RabbitMQ` and `Uchiwa`. No client checks on the server. 

To build this file you must build [sensu-core](#sensu-core) first as it uses it for building.

####sensu-server-client 
Installs and configures `Redis`, `RabbitMQ` and `Uchiwa`. Client checks on the server.

To build this file you must build [sensu-server](#sensu-server) first as it uses it for building.

####sensu-server-client-c-disk-h-slack
Installs and configures `Redis`, `RabbitMQ` and `Uchiwa`. Client checks on the server. Has a `disk-usage` check script and [slack handler plugin](https://github.com/sensu-plugins/sensu-plugins-slack) installed, configured and working with each other. Be sure to edit the `handler_config_slack.json` file! Also its `keepalive` is subscribed to the slack handler.

To build this file you must build [sensu-server](#sensu-server) first as it uses it for building.

### Client Dockerfiles

####sensu-client
Plain vanilla sensu client. Use this together with [sensu-server](#sensu-server) or [sensu-server-client-c-disk-h-slack](#sensu-server-client-c-disk-h-slack).

To build this file you must build [sensu-core](#sensu-core) first as it uses it for building.

####sensu-client-c-disk-h-slack
Has a `disk-usage` check script installed and its `keepalive` is subscribed to the slack handler. Use this together with [sensu-server-client-c-disk-h-slack](#sensu-server-client-c-disk-h-slack). 

(Tip: If both [sensu-client-c-disk-h-slack](#sensu-client-c-disk-h-slack) and [sensu-server-client-c-disk-h-slack](#sensu-server-client-c-disk-h-slack) are running on the same Docker use [sensu-server-client-h-slack](#sensu-server-client-h-slack) instead as it's pretty pointless having two disk checks on the same server resources)

To build this file you must build [sensu-core](#sensu-core) first as it uses it for building.

####sensu-client-h-slack
Its `keepalive` is subscribed to the slack handler. Use this together with [sensu-server-client-c-disk-h-slack](#sensu-server-client-c-disk-h-slack).

To build this file you must build [sensu-core](#sensu-core) first as it uses it for building.

### Building & Running
I normally use the following as an example, edit as you please.

`docker build -t basickarl/sensu-server-client-c-disk-h-slack ~/dockerfile-sensu/sensu-server-client-c-disk-h-slack`

`docker run -d --name sensu-server -h sensu-server basickarl/sensu-server-client-c-disk-h-slack`

### Bugs

Plz tell me.

FROM 	basickarl/sensu-core

MAINTAINER Karl Morrison <karl@basickarl.io>

# setup rabbitmq config file
COPY	./files/rabbitmq.config /etc/rabbitmq/rabbitmq.config

# setup sensu config files
COPY	./files/rabbitmq.json /etc/sensu/conf.d/rabbitmq.json
COPY	./files/redis.json /etc/sensu/conf.d/redis.json
COPY	./files/api.json /etc/sensu/conf.d/api.json

# install erlang
# install rabbitmq
# enable rabbitmq service on boot
# install redis
# enable redis service on boot
# ensure configuration files are owned by sensu
# enable sensu server & api on boot
# install uchiwa
# enable uchiwa service on boot
# cleanup
RUN 	sudo wget http://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb && \
		sudo dpkg -i erlang-solutions_1.0_all.deb && \
		sudo apt-get update && \
		sudo apt-get -y install erlang-nox=1:18.2 && \

		sudo wget http://www.rabbitmq.com/releases/rabbitmq-server/v3.6.0/rabbitmq-server_3.6.0-1_all.deb && \
		sudo dpkg -i rabbitmq-server_3.6.0-1_all.deb && \

		sudo update-rc.d rabbitmq-server defaults && \

		sudo apt-get -y install redis-server && \

		sudo update-rc.d redis-server defaults && \

		sudo chown -R sensu:sensu /etc/sensu && \

		sudo update-rc.d sensu-server defaults && \
		sudo update-rc.d sensu-api defaults && \

		sudo apt-get install -y uchiwa && \

		sudo update-rc.d uchiwa defaults && \

		sudo apt-get autoremove && \
		sudo apt-get clean

# setup uchiwa config file (must be afterwards uchiwa is installed)
COPY	./files/uchiwa.json /etc/sensu/uchiwa.json

# expose rabbitmq port
EXPOSE	5672

# expose redis port
EXPOSE	6379

# expose sensu api port
EXPOSE	4567

# expose uchiwa port
EXPOSE	3000

# setup supervisord config files
COPY 	./files/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

CMD		["/usr/bin/supervisord"]

# TAIL log files
# sudo tail -f /var/log/sensu/sensu-server.log
# sudo tail -f /var/log/sensu/sensu-api.log

# The following commands do not work in Dockerfiles, so COPYing the rabbitmq.config file is used
#sudo /etc/init.d/rabbitmq-server start && \
#sudo rabbitmqctl add_vhost /sensu && \
#sudo rabbitmqctl add_user sensu secret && \
#sudo rabbitmqctl set_permissions -p /sensu sensu ".*" ".*" ".*" && \

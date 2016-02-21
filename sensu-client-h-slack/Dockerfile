FROM 	basickarl/sensu-core

MAINTAINER Karl Morrison <karl@basickarl.io>

# setup sensu config files
COPY	./files/rabbitmq.json /etc/sensu/conf.d/rabbitmq.json

# setup sensu check files
COPY	./files/client.json /etc/sensu/conf.d/client.json

# enable sensu client service on boot
RUN 	sudo update-rc.d sensu-client defaults

# setup supervisord config files
COPY 	./files/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

CMD		["/usr/bin/supervisord"]

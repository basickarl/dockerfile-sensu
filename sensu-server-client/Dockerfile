FROM 	basickarl/sensu-server

MAINTAINER Karl Morrison <karl@basickarl.io>

# setup sensu config files
COPY	./files/client.json /etc/sensu/conf.d/client.json

# enable sensu client service on boot
RUN 	sudo update-rc.d sensu-client defaults

# setup supervisord config files
COPY 	./files/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

CMD		["/usr/bin/supervisord"]

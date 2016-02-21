FROM 	basickarl/sensu-server

MAINTAINER Karl Morrison <karl@basickarl.io>

# setup sensu config files
COPY	./files/client.json /etc/sensu/conf.d/client.json

# setup sensu check files
COPY	./files/check_disk.json /etc/sensu/conf.d/check_disk.json

# setup sensu handler files
COPY	./files/handler_config_slack.json /etc/sensu/conf.d/handler_config_slack.json

# install checks
# enable sensu client service on boot
# cleanup
RUN 	sudo sensu-install -p disk-checks && \
		sudo sensu-install -p slack && \

		sudo update-rc.d sensu-client defaults && \

		sudo apt-get autoremove && \
		sudo apt-get clean

# setup supervisord config files
COPY 	./files/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

CMD		["/usr/bin/supervisord"]

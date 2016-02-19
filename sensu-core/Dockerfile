FROM 	ubuntu:14.04

MAINTAINER Karl Morrison <basickarl@gmail.com>

# install prerequisites
# install sensu core repositories
# install sensu core
RUN 	sudo apt-get update && sudo apt-get -y upgrade && \
		sudo apt-get -y install wget supervisor && \

		wget -q http://repositories.sensuapp.org/apt/pubkey.gpg -O- | sudo apt-key add - && \
		echo "deb     http://repositories.sensuapp.org/apt sensu main" | sudo tee /etc/apt/sources.list.d/sensu.list && \

		sudo apt-get update && \
		sudo apt-get install sensu

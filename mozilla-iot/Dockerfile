FROM arm32v7/node:stretch

RUN echo "deb http://ftp.debian.org/debian stretch-backports main" >> /etc/apt/sources.list && \
	apt-get update && \
	apt-get install -y --no-install-recommends \
		build-essential \
		certbot \
		cron \
		git \
		libffi-dev \
		libnanomsg-dev \
		libnanomsg4 \
		libopenzwave1.5 \
		libopenzwave1.5-dev \
		python \
		python-pip \
		python-setuptools \
		python2.7-dev \
		python3 \
		python3-pip \
		python3-setuptools \
		python3-dev \
		runit \
		sudo \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
	echo "0 */12 * * * root /home/node/mozilla-iot/gateway/tools/renew-certificates.sh" > /etc/cron.d/renew-certs && \
	pip2 install git+https://github.com/mozilla-iot/gateway-addon-python#egg=gateway_addon && \
	pip3 install git+https://github.com/mozilla-iot/gateway-addon-python#egg=gateway_addon && \
	pip3 install git+https://github.com/mycroftai/adapt#egg=adapt-parser && \
	npm install -g yarn && \
	usermod -a -G sudo node && \
	touch /etc/inittab && \
	echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER node
RUN cd /home/node && \
	mkdir mozilla-iot && \
	cd mozilla-iot && \
	git clone https://github.com/mozilla-iot/intent-parser && \
	git clone https://github.com/mozilla-iot/gateway && \
	cd gateway && \
	yarn

USER root
RUN git clone https://github.com/mozilla-iot/gateway-docker.git /tmp/gateway-docker && \
	mv /tmp/gateway-docker/service /etc/service && \
	rm -rf /tmp/gateway-docker

ENV TZ America/Toronto
RUN echo $TZ > /etc/timezone && dpkg-reconfigure tzdata

ENTRYPOINT ["/usr/bin/runsvdir", "/etc/service"]


FROM arm32v7/node:stretch

ENV TZ America/Toronto
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update && apt-get install -y --no-install-recommends \
	build-essential \
	libusb-1.0-0-dev \
	libudev-dev \
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
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN git clone https://github.com/mozilla-iot/gateway /usr/src/gateway \
	&& chown -R node:node /usr/src/gateway

VOLUME /home/node/.mozilla-iot

RUN chown -R node:node /home/node/.mozilla-iot

USER node

WORKDIR /usr/src/gateway

RUN npm install

ENTRYPOINT ["npm", "start"]


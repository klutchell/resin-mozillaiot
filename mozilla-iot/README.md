# resin-mozilla-iot

[mozilla-iot](https://iot.mozilla.org/) service for [resin.io](https://resin.io/) stacks.

## Getting Started

* https://docs.resin.io/learn/getting-started
* https://hacks.mozilla.org/2018/02/how-to-build-your-own-private-smart-home-with-a-raspberry-pi-and-mozillas-things-gateway/

## Deployment

```yaml
# example docker-compose.yml
version: '2.1'

volumes:

  mozilla-iot-data:
  ssh-data:

services:

  mozilla-iot:
    build: ./mozilla-iot
    ports:
      - '192.168.86.12:80:8080'
      - '192.168.86.12:443:4443'
    volumes:
      - 'mozilla-iot-data:/home/node/.mozilla-iot'
```

## Usage

_tbd_

## Author

Kyle Harding <kylemharding@gmail.com>

## License

_tbd_

## Acknowledgments

* https://github.com/mozilla-iot/gateway-docker

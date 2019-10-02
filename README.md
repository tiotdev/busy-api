# TravelFeed notifications

Websocket notification server for TravelFeed, forked from [busyorg/busy-api](https://github.com/busyorg/busy-api)

# Production

```
docker-compose build
docker-compose up
```

or

## 1. Run redis

With persistent storage

```
docker run --name redis-notify -d --restart unless-stopped redis:alpine redis-server --appendonly yes
```

## 2.

Pull from docker hub and run behind nginx proxy (see [travelfeed-io/travelfeed-io](https://github.com/travelfeed-io/travelfeed-io) for details)

```
docker run -d \
--name tfnotify \
    --env "VIRTUAL_HOST=notify.travelfeed.io" \
    --env "VIRTUAL_PORT=5000" \
    --env "LETSENCRYPT_HOST=notify.travelfeed.io" \
    --env "LETSENCRYPT_EMAIL=your@e.mail" \
      --link redis-notify:redis  \
       --restart unless-stopped \
travelfeed/tfnotify:latest
```

### Development

```sh
# install dependencies
yarn
# run redis form docker
docker run --name redis-notify -d -p 6379:6379 redis:alpine redis-server --appendonly yes
# start notification service
yarn start
```

### Using the WS server

Get notifications:

```
{"id":0,"jsonrpc":"2.0","method":"get_notifications","params":["jpphoto"]}
```

### Testing WS

The websocket server is available at `http://localhost:4000`

For local testing, use [Smart Websocket Client](https://chrome.google.com/webstore/detail/smart-websocket-client/omalebghpgejjiaoknljcfmglgbpocdp/related?utm_source=chrome-app-launcher-info-dialog)

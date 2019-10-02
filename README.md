# TravelFeed notifications

Websocket notification server for TravelFeed, forked from [busyorg/busy-api](https://github.com/busyorg/busy-api)

### Setting up with docker

```sh
# install dependencies
yarn
# run redis form docker
docker pull redis:4-alpine
# create volume for persistent storage
docker volume create snf
docker run --name redis -p 6379:6379 -d -v snf:/data redis:4-alpine
# set env var
# unsecure required for localhost
yarn start
```

### Using the WS server

get notifications

```
{"id":0,"jsonrpc":"2.0","method":"get_notifications","params":["jpphoto"]}
```

### Testing WS

The websocket server is available at `http://localhost:4000`

For local testing, use [Smart Websocket Client](https://chrome.google.com/webstore/detail/smart-websocket-client/omalebghpgejjiaoknljcfmglgbpocdp/related?utm_source=chrome-app-launcher-info-dialog)

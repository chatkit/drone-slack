# drone-slack

[![Build Status](https://travis-ci.org/chatkit/drone-slack.svg?branch=master)](https://travis-ci.org/chatkit/drone-slack)

Drone plugin for sending Slack notifications. For the usage information and a
listing of the available options please take a look at [the docs](DOCS.md).

Note: this is the fork of the official Drone slack plugin. It changes the default output of the notification to slack to be better formatted.

## Build

Build the binary with the following commands:

```
go build
go test
```

## Docker

Build the docker image with the following commands:

```
CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -a -tags netgo
docker build -t plugins/slack .
```

Please note incorrectly building the image for the correct x64 linux and with
GCO disabled will result in an error when running the Docker image:

```
docker: Error response from daemon: Container command
'/bin/drone-slack' not found or does not exist..
```

## Usage

Execute from the working directory:

```
docker run --rm \
  -e SLACK_WEBHOOK=https://hooks.slack.com/services/... \
  -e PLUGIN_CHANNEL=channel \
  -e PLUGIN_USERNAME=drone \
  -e PLUGIN_TEMPLATE="This message will be displayed at the top" \
  -e DRONE_REPO_OWNER=octocat \
  -e DRONE_REPO_NAME=hello-world \
  -e DRONE_COMMIT_SHA=7fd1a60b01f91b314f59955a4e4d4e80d8edf11d \
  -e DRONE_COMMIT_BRANCH=master \
  -e DRONE_COMMIT_AUTHOR=octocat \
  -e DRONE_COMMIT_LINK=http://github.com/octocat/hello-world/commits/HASH \
  -e DRONE_COMMIT_MESSAGE="This is the commit message" \
  -e DRONE_BUILD_NUMBER=1 \
  -e DRONE_BUILD_STATUS=success \
  -e DRONE_BUILD_LINK=http://github.com/octocat/hello-world \
  -e DRONE_TAG=1.0.0 \
  chatkitinc/drone-slack
```

## Output

![output](output.png)


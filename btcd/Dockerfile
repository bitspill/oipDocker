FROM golang:1-alpine as build

RUN apk add --no-cache git

RUN git clone https://github.com/btcsuite/btcd/ /go/src/github.com/btcsuite/btcd/
WORKDIR /go/src/github.com/btcsuite/btcd/

RUN GO111MODULE=on go install -v . ./cmd/...

FROM alpine:latest

COPY --from=build /go/bin/ /btcd/bin/
COPY ./btcd.conf /btcd/btcd.conf


EXPOSE 8336 8337
VOLUME ["/root/.btcd/"]
ENTRYPOINT ["/btcd/bin/btcd", "--configfile=/btcd/btcd.conf"]

FROM golang:1-alpine as build

RUN apk add --no-cache git curl

ARG DEP_VERSION="0.5.0"

RUN curl -L -s https://github.com/golang/dep/releases/download/v${DEP_VERSION}/dep-linux-amd64 \
        -o /go/bin/dep && chmod +x /go/bin/dep

RUN go get -u github.com/gobuffalo/packr/v2/packr2
RUN git clone https://github.com/oipwg/oip /go/src/github.com/oipwg/oip
WORKDIR /go/src/github.com/oipwg/oip
RUN dep ensure -v
WORKDIR /go/src/github.com/oipwg/oip/cmd/oipd
RUN packr2 -v

RUN go build -ldflags \
        "-X github.com/oipwg/oip/version.GitCommitHash=$(git rev-parse --short HEAD) \
        -X github.com/oipwg/oip/version.BuildDate=$(date +'%Y.%m.%d.%H%M%S') \
        -X github.com/oipwg/oip/version.BuiltBy=Docker \
        -X 'github.com/oipwg/oip/version.GoVersion=$(go version)' \
        -s -w" -o oipd github.com/oipwg/oip/cmd/oipd
RUN cp oipd /go/bin/oipd

FROM alpine:latest

COPY --from=build /go/bin/oipd /oip/bin/oipd
COPY ./config.yml /oip/config.yml

EXPOSE 1606
ENV LOG=*
ENTRYPOINT ["/oip/bin/oipd", "--appdir=/oip"]
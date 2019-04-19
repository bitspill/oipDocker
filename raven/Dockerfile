FROM alpine as build

RUN apk add --no-cache alpine-sdk boost-dev openssl-dev libevent-dev autoconf automake libtool

RUN git clone https://github.com/RavenProject/Ravencoin /rvn/Ravencoin
WORKDIR /rvn/Ravencoin

RUN ./autogen.sh
RUN ./configure --enable-static --disable-shared --disable-wallet --without-gui --without-miniupnpc
RUN make check -j 6

FROM alpine:latest

COPY --from=build /rvn/Ravencoin/ravend /usr/bin/ravend
COPY --from=build /rvn/Ravencoin/raven-cli /usr/bin/raven-cli

# RUN apk add --no-cache openssl libevent boost-filesystem boost-system boost-chrono boost-program_options boost-thread

EXPOSE 8767 8766
VOLUME ["/rvn/datadir"]
ENTRYPOINT ["/usr/bin/ravend", "-datadir=/rvn/datadir"]

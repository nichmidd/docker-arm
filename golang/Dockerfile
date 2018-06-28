FROM alpine:latest

RUN apk add --no-cache ca-certificates

ENV GOLANG_VERSION 1.10
ENV GOLANG_SRC_URL https://golang.org/dl/go$GOLANG_VERSION.src.tar.gz

RUN set -ex \
        && apk add --no-cache --virtual .build-deps \
                bash \
                gcc \
                musl-dev \
                openssl \
                go \
        \
        && export GOROOT_BOOTSTRAP="$(go env GOROOT)" \
        \
        && wget -q "$GOLANG_SRC_URL" -O golang.tar.gz \
        && tar -C /usr/local -xzf golang.tar.gz \
        && rm golang.tar.gz \
        && cd /usr/local/go/src \
        && ./make.bash \
        \
        && apk del .build-deps

ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"
WORKDIR $GOPATH

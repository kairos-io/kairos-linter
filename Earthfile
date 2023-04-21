VERSION 0.7
FROM alpine

# renovate: datasource=docker depName=golang
ARG GO_VERSION=1.20
ARG GOLINT_VERSION=1.52.2

yamllint:
    FROM cytopia/yamllint
    COPY . .
    ARG DIRS
    ENV LIST_OF_DIRS="$DIRS"
    IF [ "$LIST_OF_DIRS" = "" ]
        ENV LIST_OF_DIRS="./"
    END
    RUN yamllint "$LIST_OF_DIRS"

golint:
    ARG GO_VERSION
    FROM golang:$GO_VERSION
    ARG GOLINT_VERSION
    RUN wget -O- -nv https://raw.githubusercontent.com/golangci/golangci-lint/master/install.sh | sh -s v$GOLINT_VERSION
    WORKDIR /build
    COPY . .
    RUN golangci-lint run

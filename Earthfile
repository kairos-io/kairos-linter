VERSION 0.7
FROM alpine

# renovate: datasource=docker depName=golang
ARG GO_VERSION=1.20
ARG GOLINT_VERSION=1.52.2
# renovate: datasource=docker depName=hadolint/hadolint versioning=docker
ARG HADOLINT_VERSION=2.12.0-alpine

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

hadolint:
    ARG HADOLINT_VERSION
    ARG DIR
    FROM hadolint/hadolint:$HADOLINT_VERSION
    ENV IMAGES_DIR="$DIR"
    IF [ "IMAGES_DIR" = "" ]
        ENV IMAGES_DIR="images"
    END
    COPY $IMAGES_DIR .
    RUN ls
    RUN find . -name "Dockerfile*" -print | xargs -r -n1 hadolint

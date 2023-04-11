VERSION 0.7
FROM alpine

yamllint:
    FROM cytopia/yamllint
    COPY . .
    ARG DIRS
    ENV LIST_OF_DIRS="$DIRS"
    IF [ "$LIST_OF_DIRS" = "" ]
        ENV LIST_OF_DIRS="./"
    END
    RUN yamllint "$LIST_OF_DIRS"

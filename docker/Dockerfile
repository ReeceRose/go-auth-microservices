
# Generic Dockerfile for all things Golang.
# Check Makefile for how to run

# Note, need to specify amd64 as arm64 cannot fetch upx package
FROM --platform=amd64 golang:1.17.6-alpine3.15 AS builder
ARG SERVICE

WORKDIR /app
COPY . .
RUN apk update \
  && apk add make \
  && apk add upx \
  && apk add git \
  && make $SERVICE \
  && mv build/$SERVICE /service

FROM scratch
COPY --from=builder /service /
EXPOSE 443
ENTRYPOINT ["/service"]

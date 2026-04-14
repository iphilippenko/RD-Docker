# Optimization: Minimal base alpine usage; separate stage for deps instalation, improves caching layers if both go.mod and go.sum weren't changed
FROM golang:1.23-alpine AS deps
LABEL authors="irinashevcenko"

WORKDIR /src

COPY go.mod go.sum ./
RUN go mod download

FROM golang:1.23-alpine AS build
WORKDIR /src

COPY --from=deps /go/pkg /go/pkg
COPY . .

# Building static binary
RUN CGO_ENABLED=0 go build -o app main.go


# Optimization: Minimal base alpine usage; usage only compiled binary in runtime image
FROM alpine:3.20

WORKDIR /src

# Copy only built binary here
COPY --from=build /src/app .

RUN addgroup -S myappgroup && adduser -S myappuser -G myappgroup
USER myappuser

EXPOSE 8080

CMD ["./app"]


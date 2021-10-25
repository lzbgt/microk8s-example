FROM golang:1.16-alpine

ENV GOPROXY=https://goproxy.io,direct
WORKDIR /
COPY go.mod ./
COPY go.sum ./
RUN go mod download
COPY *.go ./
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app .

FROM alpine:latest  
RUN apk --no-cache add ca-certificates
WORKDIR /
COPY --from=0 /app ./
EXPOSE 8080
CMD [ "/app" ]
FROM golang:1.22-alpine AS builder
WORKDIR /app
COPY go.mod ./
COPY . .
RUN go mod download && go mod tidy
RUN CGO_ENABLED=0 GOOS=linux go build -o auth-app .

FROM alpine:latest
WORKDIR /app
RUN apk --no-cache add ca-certificates
COPY --from=builder /app/auth-app .
EXPOSE 8080
CMD ["./auth-app"]

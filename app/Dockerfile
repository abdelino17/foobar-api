# Build stage
FROM golang:1.13-alpine as builder

WORKDIR /app

COPY go.* ./
RUN go mod download

COPY . ./

RUN CGO_ENABLED=0 go build -a --trimpath --installsuffix cgo --ldflags="-s" -o whoami

# Run stage
FROM gcr.io/distroless/base-debian10

# COPY --from=builder /app/cert/*.pem /cert/

COPY --from=builder /app/whoami /app/whoami

ENTRYPOINT ["/app/whoami"]
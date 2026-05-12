# STEP 1: Build Stage (Heavy lifting)
FROM golang:1.26-alpine AS builder
WORKDIR /app
COPY . .
RUN go mod download
# Build a static binary to ensure it runs on any Linux
RUN CGO_ENABLED=0 GOOS=linux go build -ldflags="-s -w" -o server cmd/api/main.go

# STEP 2: Final Run Stage (Lightweight)
FROM alpine:latest
WORKDIR /root/
# Copy only the compiled binary from the builder
COPY --from=builder /app/server .
# Copy the .env for connectivity (Database/Redis)
COPY --from=builder /app/.env . 

EXPOSE 8080
CMD ["./server"]
# Stage 1: Build with GraalVM
FROM ghcr.io/graalvm/native-image-community:23 AS builder

WORKDIR /app

COPY . .

RUN ./mvnw -Pnative -DskipTests package

# Stage 2: Minimal runtime image
FROM alpine

RUN apk add --no-cache libc6-compat

WORKDIR /app

COPY --from=builder /app/target/gateway-service .

EXPOSE 8080

CMD ["./gateway-service"]
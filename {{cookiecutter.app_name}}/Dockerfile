# Start from the latest golang base image
FROM {{cookiecutter.docker_build_image}}:{{cookiecutter.docker_build_image_version}} AS builder

LABEL app="build-{{cookiecutter.app_name}}"

# Add Maintainer Info
LABEL maintainer="{{cookiecutter.full_name}} <{{cookiecutter.email_address}}>"

# Copy the source from the current directory to the Working Directory inside the container
COPY . .

#RUN rm -rf third_party  README.MD scripts

RUN go mod tidy

# Download all dependencies. Dependencies will be cached if the go.mod and go.sum files are not changed
RUN go mod download

# Create appuser.
RUN echo "nobody:x:65534:65534:Nobody:/:" > /etc_passwd

# Build the Go app
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -a -installsuffix cgo -ldflags="-w -s" -o main ./main.go

### Certs
FROM {{cookiecutter.docker_certs_image}} as certs
RUN apk --update add ca-certificates

# Final Stage
FROM {{cookiecutter.docker_image}}

ARG GIT_COMMIT
ARG VERSION
LABEL GIT_COMMIT=$GIT_COMMIT
LABEL VERSION=$VERSION

WORKDIR /root/

COPY --from=builder /etc_passwd /etc/passwd
COPY --from=certs /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/ca-certificates.crt
# Copy the Pre-built binary file from the previous stage
COPY --from=builder /app/main /

# Use an unprivileged user.
USER nobody

# Command to run the executable
ENTRYPOINT [ "/main"]

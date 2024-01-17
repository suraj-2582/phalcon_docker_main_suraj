FROM ubuntu:20.04

# Set non-interactive mode during the build
ENV DEBIAN_FRONTEND=noninteractive

# Install NGINX and nginx-extras
RUN apt-get update && \
    apt-get install -y nginx nginx-extras && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*



# Expose the ports
EXPOSE 80 443

# Start NGINX in the foreground
CMD ["nginx", "-g", "daemon off;"]


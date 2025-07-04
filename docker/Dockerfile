FROM debian:bookworm-slim

# Install required packages
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    curl \
    ca-certificates \
    bash \
    jq \
    file \
    procps && \
    rm -rf /var/lib/apt/lists/*

# Set environment variables
ENV REPO="Qteam-official/ICMPTunnel"
ENV GITHUB_API="https://api.github.com/repos/$REPO/releases/latest"
ENV BINARY_NAME="ICMPTunnel"
ENV INSTALL_PATH="/usr/local/bin/$BINARY_NAME"

# Create working directory
WORKDIR /app

# Download and install ICMPTunnel binary
RUN URL=$(curl -s $GITHUB_API | jq -r '.assets[] | select(.name | contains("ICMPTunnel")) | .browser_download_url') && \
    if [ -z "$URL" ] || [ "$URL" = "null" ]; then \
        URL=$(curl -s $GITHUB_API | grep -o '"browser_download_url": *"[^"]*"' | grep "$BINARY_NAME" | cut -d'"' -f4); \
    fi && \
    curl -L -o "$INSTALL_PATH" "$URL" && \
    chmod +x "$INSTALL_PATH"

# Create entrypoint script
RUN echo '#!/bin/bash' > /entrypoint.sh && \
    echo 'exec "$@"' >> /entrypoint.sh && \
    chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]

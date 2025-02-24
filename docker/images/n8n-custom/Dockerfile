FROM n8nio/n8n:1.79.3

# Switch to root to install packages
USER root

# Install FFmpeg using Alpine package manager
RUN apk update && \
    apk add --no-cache ffmpeg && \
    mkdir -p /home/node/tmp && \
    chown node:node /home/node/tmp && \
    chmod 777 /home/node/tmp

# Debug: Print FFmpeg location and version
RUN which ffmpeg && \
    ffmpeg -version && \
    echo "FFmpeg installation verified"

# Ensure FFmpeg is in PATH and accessible
RUN ln -sf $(which ffmpeg) /usr/local/bin/ffmpeg && \
    echo "PATH=$PATH" && \
    ls -la /usr/local/bin/ffmpeg

# Set environment variable for temp directory path
ENV N8N_TEMP_DIR=/home/node/tmp

# Debug: Verify permissions as node user
USER node
RUN ffmpeg -version || echo "Failed to run ffmpeg as node user"

# Additional debug: Print PATH and check FFmpeg accessibility
RUN echo "Current PATH: $PATH" && \
    which ffmpeg || echo "ffmpeg not in PATH"

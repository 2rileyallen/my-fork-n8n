FROM n8nio/n8n:1.79.3

# Switch to root to install packages
USER root

# Install FFmpeg using Alpine package manager
RUN apk update && \
    apk add --no-cache ffmpeg && \
    mkdir -p /home/node/tmp && \
    chown node:node /home/node/tmp && \
    chmod 777 /home/node/tmp

# Create and set permissions for .n8n directory
RUN mkdir -p /home/node/.n8n && \
    chown -R node:node /home/node/.n8n && \
    chmod -R 700 /home/node/.n8n

# Debug: Print FFmpeg location and version
RUN which ffmpeg && \
    ffmpeg -version && \
    echo "FFmpeg installation verified"

# Ensure FFmpeg is in PATH and accessible
RUN ln -sf $(which ffmpeg) /usr/local/bin/ffmpeg && \
    echo "PATH=$PATH" && \
    ls -la /usr/local/bin/ffmpeg

# Set environment variables
ENV N8N_TEMP_DIR=/home/node/tmp
ENV N8N_USER_FOLDER=/home/node/.n8n
ENV PORT=5678
ENV N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=false

# Switch to node user for security
USER node

# Debug: Verify setup
RUN ffmpeg -version || echo "Failed to run ffmpeg as node user" && \
    echo "Current PATH: $PATH" && \
    which ffmpeg || echo "ffmpeg not in PATH" && \
    ls -la /home/node/.n8n || echo "Cannot access .n8n directory"

FROM n8nio/n8n:latest

# Switch to root to install packages
USER root

# Install FFmpeg and create temp directory
RUN apt-get update && \
    apt-get install -y ffmpeg && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    mkdir -p /home/node/tmp && \
    chown node:node /home/node/tmp && \
    chmod 777 /home/node/tmp

# Ensure FFmpeg is in PATH
RUN which ffmpeg && \
    ln -sf $(which ffmpeg) /usr/local/bin/ffmpeg

# Set environment variable for temp directory path
ENV N8N_TEMP_DIR=/home/node/tmp

# Switch back to node user
USER node

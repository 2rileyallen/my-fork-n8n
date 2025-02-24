FROM n8nio/n8n:1.79.3

# Switch to root to install packages
USER root

# Install FFmpeg using Alpine package manager
RUN apk update && \
    apk add --no-cache ffmpeg

# Create necessary directories
RUN mkdir -p /mnt/n8n/workflows && \
    mkdir -p /mnt/n8n/temp && \
    chown -R node:node /mnt/n8n && \
    chmod -R 755 /mnt/n8n

# Ensure FFmpeg is in PATH
RUN ln -sf $(which ffmpeg) /usr/local/bin/ffmpeg

# Set environment variables
ENV N8N_DATA_FOLDER=/mnt/n8n/workflows
ENV N8N_TEMP_DIR=/mnt/n8n/temp
ENV PORT=5678
ENV N8N_PROTOCOL=https
ENV N8N_HOST=api.thetunecanvas.com
ENV WEBHOOK_URL=https://api.thetunecanvas.com/
ENV N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=false

# Switch to node user for security
USER node

# Create symbolic link for backwards compatibility
RUN mkdir -p /home/node/.n8n && \
    ln -sf /mnt/n8n/workflows/* /home/node/.n8n/ || true

# Debug: Verify setup
RUN echo "Verifying directories and permissions:" && \
    ls -la /mnt/n8n/workflows || echo "Cannot access workflows directory" && \
    ls -la /mnt/n8n/temp || echo "Cannot access temp directory" && \
    echo "FFmpeg version:" && \
    ffmpeg -version

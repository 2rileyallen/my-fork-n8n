FROM n8nio/n8n:1.79.3

# Switch to root to install packages
USER root

# Install FFmpeg using Alpine package manager
RUN apk update && \
    apk add --no-cache ffmpeg

# Create the base data directory and set permissions
RUN mkdir -p /mnt/n8n && \
    chown -R node:node /mnt/n8n && \
    chmod -R 755 /mnt/n8n

# Ensure FFmpeg is in PATH
RUN ln -sf $(which ffmpeg) /usr/local/bin/ffmpeg

# Set environment variables
ENV N8N_DATA_FOLDER=/mnt/n8n
ENV N8N_TEMP_DIR=/mnt/n8n/temp
ENV PORT=5678
ENV N8N_PROTOCOL=https
ENV N8N_HOST=api.thetunecanvas.com
ENV WEBHOOK_URL=https://api.thetunecanvas.com/
ENV N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=false

# Debug: Verify setup
RUN echo "Verifying directories and permissions:" && \
    ls -la /mnt/n8n || echo "Cannot access /mnt/n8n"
		

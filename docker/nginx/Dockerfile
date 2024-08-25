# docker/nginx/Dockerfile
FROM nginx:alpine

# Copy custom Nginx configuration
COPY /docker/nginx/nginx.conf /etc/nginx/conf.d/default.conf

# Create directory for static files
RUN mkdir -p /var/www/html/public

# Optional: Copy static files if needed
COPY /src/public /var/www/html/public

# Set proper permissions for nginx user
RUN chown -R nginx:nginx /var/www/html && \
    chmod -R 755 /var/www/html
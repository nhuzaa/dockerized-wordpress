# Builder stage - prepare files and set permissions
FROM wordpress:latest as builder

# Create wp-content directory structure
RUN mkdir -p /var/www/html/wp-content/plugins \
    && mkdir -p /var/www/html/wp-content/themes \
    && mkdir -p /var/www/html/wp-content/uploads

# Copy and prepare wp-content
RUN mkdir -p wp-content
COPY wp-content/ /var/www/html/wp-content/

# Copy and prepare wp-config.php
COPY wp-config.php /tmp/wp-config.php

# Set proper permissions in builder stage
RUN chown -R www-data:www-data /var/www/html \
    && chmod -R 755 /var/www/html/wp-content \
    && find /var/www/html -type d -exec chmod 755 {} \; \
    && find /var/www/html -type f -exec chmod 644 {} \;

# Runtime stage - lean final image
FROM wordpress:latest

# Copy custom PHP configuration
COPY php.ini /usr/local/etc/php/conf.d/custom.ini

# Copy prepared wp-content from builder
COPY --from=builder --chown=www-data:www-data /var/www/html/wp-content/ /var/www/html/wp-content/

# Copy wp-config.php conditionally
COPY --from=builder /tmp/wp-config.php /tmp/wp-config.php
RUN if [ ! -f /var/www/html/wp-config.php ]; then \
        cp /tmp/wp-config.php /var/www/html/wp-config.php; \
    fi && rm -f /tmp/wp-config.php

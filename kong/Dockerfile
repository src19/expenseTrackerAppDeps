# Start from the official Kong image
FROM kong:latest

# Switch to root to set up directories and copy plugins
USER root

# Create necessary directories for declarative config and plugins
RUN mkdir -p /usr/local/kong/declarative /usr/local/share/lua/5.1/kong/plugins/custom-auth

# Copy the local config and custom plugins to the container
COPY ./config/kong.yml /usr/local/kong/declarative/kong.yml
COPY ./custom-plugins/custom-auth /usr/local/share/lua/5.1/kong/plugins/custom-auth

# Set appropriate permissions for the config and plugins
RUN chmod -R 755 /usr/local/kong/declarative /usr/local/share/lua/5.1/kong/plugins/custom-auth

# Switch back to kong user
USER kong

# Set environment variables from Docker Compose
ENV KONG_DATABASE=off \
    KONG_DECLARATIVE_CONFIG=/usr/local/kong/declarative/kong.yml \
    KONG_PROXY_ACCESS_LOG=/dev/stdout \
    KONG_ADMIN_ACCESS_LOG=/dev/stdout \
    KONG_PROXY_ERROR_LOG=/dev/stderr \
    KONG_ADMIN_ERROR_LOG=/dev/stderr \
    KONG_ADMIN_LISTEN="0.0.0.0:8001, 0.0.0.0:8444 ssl" \
    KONG_LOG_LEVEL=debug \
    KONG_PLUGINS=custom-auth \
    KONG_LUA_PACKAGE_PATH="/usr/local/share/lua/5.1/?.lua;;"

# Expose the necessary ports
EXPOSE 8000 8443 8001 8444

# Start Kong
CMD ["kong", "start"]

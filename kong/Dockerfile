# Start from the official Kong image
FROM kong:latest

USER root

# Install curl
RUN apt-get update && apt-get install -y curl && apt-get clean

# Create necessary directories
RUN mkdir -p /usr/local/kong/declarative /usr/local/share/lua/5.1/kong/plugins/custom-auth

# Copy custom plugin files (you'll need to have these files in a 'custom-plugins' directory)
COPY custom-plugins/custom-auth/handler.lua /usr/local/share/lua/5.1/kong/plugins/custom-auth/handler.lua
COPY custom-plugins/custom-auth/schema.lua /usr/local/share/lua/5.1/kong/plugins/custom-auth/schema.lua

# Set permissions
RUN chown -R kong:kong /usr/local/kong/declarative /usr/local/share/lua/5.1/kong/plugins/custom-auth

# Set environment variables
ENV KONG_DATABASE=off
ENV KONG_DECLARATIVE_CONFIG=/usr/local/kong/declarative/kong.yml
ENV KONG_PROXY_ACCESS_LOG=/dev/stdout
ENV KONG_ADMIN_ACCESS_LOG=/dev/stdout
ENV KONG_PROXY_ERROR_LOG=/dev/stderr
ENV KONG_ADMIN_ERROR_LOG=/dev/stderr
ENV KONG_ADMIN_LISTEN="0.0.0.0:8001, 0.0.0.0:8444 ssl"
ENV KONG_LOG_LEVEL=debug
ENV KONG_PLUGINS="bundled,custom-auth"
ENV KONG_LUA_PACKAGE_PATH="/usr/local/share/lua/5.1/?.lua;;"

# Switch back to the kong user
USER kong

# Expose ports
EXPOSE 8000 8443 8001 8444

# Set the entry point
ENTRYPOINT ["kong"]

# Set the default command
CMD ["docker-entrypoint.sh", "kong", "docker-start"]
FROM kong:latest

# Copy configuration files
COPY ./config /usr/local/kong/declarative
COPY ./custom-plugins /usr/local/share/lua/5.1/kong/plugins

# Set environment variables
ENV KONG_DATABASE="off"
ENV KONG_DECLARATIVE_CONFIG="/usr/local/kong/declarative/kong.yml"
ENV KONG_PROXY_ACCESS_LOG="/dev/stdout"
ENV KONG_ADMIN_ACCESS_LOG="/dev/stdout"
ENV KONG_PROXY_ERROR_LOG="/dev/stderr"
ENV KONG_ADMIN_ERROR_LOG="/dev/stderr"
ENV KONG_ADMIN_LISTEN="0.0.0.0:8001, 0.0.0.0:8444 ssl"
ENV KONG_LOG_LEVEL="debug"
ENV KONG_PLUGINS="custom-auth"
ENV KONG_LUA_PACKAGE_PATH="/usr/local/share/lua/5.1/?.lua;;"


EXPOSE 8000 8001 8443 8444
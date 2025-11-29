FROM postgres:15-alpine

# Install additional tools
RUN apk add --no-cache curl

# Copy initialization scripts
COPY schema.sql /docker-entrypoint-initdb.d/01-schema.sql
COPY init.sh /docker-entrypoint-initdb.d/02-init.sh

# Set permissions
RUN chmod +x /docker-entrypoint-initdb.d/*.sh

# Healthcheck
HEALTHCHECK --interval=30s --timeout=3s --retries=3 \
    CMD pg_isready -U ${POSTGRES_USER:-postgres} || exit 1

EXPOSE 5432

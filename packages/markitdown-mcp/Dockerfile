FROM python:3.13-slim-bullseye

ENV DEBIAN_FRONTEND=noninteractive
ENV EXIFTOOL_PATH=/usr/bin/exiftool
ENV FFMPEG_PATH=/usr/bin/ffmpeg
ENV MARKITDOWN_ENABLE_PLUGINS=True

# Runtime deps (add more plugins here if needed)
RUN apt-get update && apt-get install -y --no-install-recommends \
    ffmpeg \
    exiftool && \
    rm -rf /var/lib/apt/lists/*

COPY . /app
RUN pip --no-cache-dir install /app

WORKDIR /workdir

# Document the port used by the HTTP server
EXPOSE 8080

# Default USERID/GROUPID (non-root)
ARG USERID=nobody
ARG GROUPID=nogroup
USER $USERID:$GROUPID

# Keep the CLI as entrypoint, set server defaults via CMD
ENTRYPOINT ["markitdown-mcp"]
CMD ["--host", "0.0.0.0", "--port", "8080", "--http"]

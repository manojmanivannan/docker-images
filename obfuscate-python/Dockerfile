# Build a virtualenv using the appropriate Debian release
# * Install python3-venv for the built-in Python3 venv module (not installed by default)
# * Install gcc libpython3-dev to compile C Python modules
# * In the virtualenv: Update pip setuputils and wheel to support building new packages
FROM debian:11-slim AS build
RUN apt-get update && \
    apt-get install --no-install-suggests --no-install-recommends --yes python3-venv gcc libpython3-dev python3-dev && \
    python3 -m venv /venv && \
    /venv/bin/pip install --upgrade pip setuptools wheel cython
COPY . /app
WORKDIR /app
RUN /venv/bin/cython --embed -o /app/main.c /app/main.py
RUN gcc -o /app/main /app/main.c -I$(python3.9-config --includes) -L$(python3.9-config --prefix)/lib -lpython3.9

# FROM alpine as release
# RUN apk add --no-cache bash
# COPY --from=build /app/main /app/main

# Copy the virtualenv into a distroless image
FROM gcr.io/distroless/python3-debian11
# COPY --from=build /venv /venv
COPY --from=build /app/main /app/main
COPY --from=build /usr/lib/x86_64-linux-gnu/libpython* /app/lib/

# # set environment variables
ENV LD_LIBRARY_PATH=/app/lib
ENTRYPOINT ["/app/main"]

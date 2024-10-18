# Build a virtualenv using the appropriate Debian release
# * Install python3-venv for the built-in Python3 venv module (not installed by default)
# * Install gcc libpython3-dev to compile C Python modules
# * In the virtualenv: Update pip setuputils and wheel to support building new packages
FROM debian:11-slim AS build
COPY requirements.txt /requirements.txt
RUN apt-get update && \
    apt-get install --no-install-suggests --no-install-recommends --yes python3-venv gcc libpython3-dev python3-dev && \
    python3 -m venv /venv && \
    /venv/bin/pip install --upgrade pip setuptools wheel cython



FROM build AS build-venv
COPY main.py /app/main.py
RUN /venv/bin/pip install --disable-pip-version-check -r /requirements.txt && \
    /venv/bin/cython --embed -o /app/main.c /app/main.py && \
    gcc -o /app/main /app/main.c -I$(python3-config --includes) -L$(python3-config --prefix)/lib -lpython3.9

# Copy the binary and python dependency into a distroless image
FROM gcr.io/distroless/python3-debian11
COPY --from=build-venv /venv/lib/python*/site-packages /venv/lib/python/site-packages
COPY --from=build-venv /app/main /app/main
COPY --from=build-venv /usr/lib/x86_64-linux-gnu/libpython* /app/lib/

# set environment variables
ENV LD_LIBRARY_PATH=/app/lib
ENV PYTHONPATH="/venv/lib/python/site-packages"

ENTRYPOINT ["/app/main"]

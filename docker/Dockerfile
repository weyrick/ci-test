FROM debian:bullseye-slim AS cppbuild

ENV BUILD_DEPS "g++ cmake make git pkgconf ca-certificates"

RUN \
    apt-get update && \
    apt-get install --yes --force-yes --no-install-recommends ${BUILD_DEPS}

COPY . /src/

WORKDIR /tmp/build

RUN \
    PKG_CONFIG_PATH=/local/lib/pkgconfig cmake -DCMAKE_BUILD_TYPE=Release /src && \
    make all -j 2

FROM debian:bullseye-slim AS runtime

ENV RUNTIME_DEPS "curl ca-certificates"

RUN \
    apt-get update && \
    apt-get install --yes --force-yes --no-install-recommends ${RUNTIME_DEPS}

COPY --from=cppbuild /tmp/build/ci_test /usr/local/sbin/ci_test

ENTRYPOINT [ "ci_test" ]


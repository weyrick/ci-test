FROM debian:bullseye-slim AS cppbuild

ENV BUILD_DEPS "g++ cmake make git pkgconf ca-certificates"

RUN \
    PKG_CONFIG_PATH=/local/lib/pkgconfig cmake -DCMAKE_BUILD_TYPE=Release /src && \
    make all test -j 4

FROM debian:bullseye-slim AS runtime

ENV RUNTIME_DEPS "curl ca-certificates"

COPY --from=cppbuild /tmp/build/ci_test /usr/local/sbin/ci_test

ENTRYPOINT [ "ci_test" ]


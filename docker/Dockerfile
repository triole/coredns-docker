FROM alpine:latest

COPY ./bin/* /usr/bin/

HEALTHCHECK --interval=60s --timeout=5s --retries=3 \
    CMD pgrep coredns

CMD ["/usr/bin/coredns", "--conf", "/vol/conf/Corefile"]

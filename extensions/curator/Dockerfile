FROM choelea/curator:5.8.1

COPY entrypoint.sh /

WORKDIR /usr/share/curator
COPY config ./config

ENTRYPOINT ["/entrypoint.sh"]

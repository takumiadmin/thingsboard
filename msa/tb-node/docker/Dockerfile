FROM openjdk:17-jre-slim

# Install deps
RUN apt-get update && \
    apt-get install -y --no-install-recommends ca-certificates && \
    rm -rf /var/lib/apt/lists/*

# Copy files
COPY thingsboard.deb /tmp/thingsboard.deb
COPY start-tb-node.sh /tmp/start-tb-node.sh
COPY logback.xml /tmp/logback.xml

# Install .deb
RUN dpkg -i /tmp/thingsboard.deb || apt-get install -f -y && \
    rm /tmp/thingsboard.deb && \
    mv /tmp/start-tb-node.sh /usr/bin/start-tb-node.sh && \
    chmod +x /usr/bin/start-tb-node.sh && \
    mv /tmp/logback.xml /usr/share/thingsboard/conf/logback.xml && \
    chown -R thingsboard:thingsboard /usr/share/thingsboard /var/log/thingsboard

USER thingsboard
CMD ["/usr/bin/start-tb-node.sh"]

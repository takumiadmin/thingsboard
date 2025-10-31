FROM openjdk:17-jre-slim

# Install dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends wget ca-certificates && \
    rm -rf /var/lib/apt/lists/*

# Create user
RUN groupadd -r thingsboard && useradd -r -g thingsboard thingsboard

# Copy JAR from Maven build
COPY target/tb-node-*.jar /usr/share/thingsboard/bin/thingsboard.jar
COPY application/src/main/resources/thingsboard.yml /usr/share/thingsboard/conf/thingsboard.yml
COPY application/src/main/resources/logback.xml /usr/share/thingsboard/conf/logback.xml

# Create dirs
RUN mkdir -p /usr/share/thingsboard/data \
    && mkdir -p /var/log/thingsboard \
    && chown -R thingsboard:thingsboard /usr/share/thingsboard \
    && chown -R thingsboard:thingsboard /var/log/thingsboard

# Expose ports
EXPOSE 8080 1883 8883 5683-5688/udp

USER thingsboard
WORKDIR /usr/share/thingsboard

CMD ["java", "-Xmx1500m", "-Xms512m", "-Dlogging.config=/usr/share/thingsboard/conf/logback.xml", "-jar", "/usr/share/thingsboard/bin/thingsboard.jar"]

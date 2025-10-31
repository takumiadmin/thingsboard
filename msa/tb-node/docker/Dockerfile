#
# Copyright © 2016-2025 The Thingsboard Authors
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

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

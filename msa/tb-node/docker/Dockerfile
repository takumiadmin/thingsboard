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

# --- Stage 1: Build custom UI (optional, safe to keep even if no UI changes) ---
FROM node:20 AS ui-builder
WORKDIR /app
COPY ui-ngx/ ./ui-ngx/
WORKDIR /app/ui-ngx
RUN npm install --legacy-peer-deps && npm run build -- --output-path=dist

# --- Stage 2: Final image from official stable ThingsBoard CE ---
FROM thingsboard/tb-postgres:4.2.1

# Copy your built custom UI into the ThingsBoard UI directory
COPY --from=ui-builder /app/ui-ngx/dist/ /usr/share/thingsboard/ui/

# Permissions just in case
RUN chmod -R 755 /usr/share/thingsboard

ENTRYPOINT ["/usr/share/thingsboard/bin/docker-entrypoint.sh"]

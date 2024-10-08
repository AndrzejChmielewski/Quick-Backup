# Copyright 2020 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     https://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
FROM gitlab/gitlab-ee:latest

# Install libarchive
RUN apt-get update && apt-get install -y libarchive-dev

# Generate SSH keys and copy them into the image
RUN mkdir -p /etc/gitlab/ssh && \
    ssh-keygen -t rsa -b 4096 -f /etc/gitlab/ssh/ssh_host_rsa_key -N '' && \
    cp /etc/gitlab/ssh/ssh_host_rsa_key /etc/ssh/ssh_host_rsa_key && \
    cp /etc/gitlab/ssh/ssh_host_rsa_key.pub /etc/ssh/ssh_host_rsa_key.pub

# Define data volumes
VOLUME /etc/gitlab
VOLUME /var/opt/gitlab
VOLUME /var/log/gitlab

# Expose web & ssh ports
EXPOSE 80
EXPOSE 443
EXPOSE 22


FROM europe-west4-docker.pkg.dev/internet-ctf/custom-images/kctf-source
## Create necessary directories and fix permissions
#RUN mkdir -p /var/opt/gitlab /var/log/gitlab && \
#    chown -R git:git /etc/gitlab /var/opt/gitlab /var/log/gitlab
#
## Copy wrapper and fix-permissions scripts
#COPY wrapper /usr/local/bin/
#COPY fix-permissions.sh /usr/local/bin/fix-permissions.sh
#RUN chmod +x /usr/local/bin/wrapper /usr/local/bin/fix-permissions.sh
## Ensure the GitLab reconfigure command is run at startup
#ENTRYPOINT ["/usr/local/bin/wrapper"]
#CMD ["gitlab-ctl", "reconfigure"]
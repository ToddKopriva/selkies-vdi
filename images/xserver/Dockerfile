# Copyright 2019 Google LLC
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

FROM ubuntu:19.10

# Use GCE apt servers
ARG GCE_ZONE=us-west1
RUN cp /etc/apt/sources.list /etc/apt/sources.list.orig && \
    sed -i "s/archive.ubuntu.com/${GCE_ZONE}.gce.archive.ubuntu.com/g" /etc/apt/sources.list

# Install base dependencies
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
        xserver-xorg-core \
        x11-xserver-utils \
        xserver-xorg-input-evdev \
        xserver-xorg-input-libinput \
        xserver-xorg-input-kbd \
        xinput \
        evtest \
        x11vnc \
        socat \
        libxrandr-dev \
        pciutils && \
    rm -rf /var/lib/apt/lists/

# Export library path for NVIDIA libs
ENV LD_LIBRARY_PATH /usr/local/nvidia/lib64

# Set the DISPLAY variable.
ENV DISPLAY :0

# Set the PATH
ENV PATH ${PATH}:/usr/local/nvidia/bin

COPY xorg.conf /etc/X11/xorg.conf
COPY entrypoint.sh /entrypoint.sh
RUN chmod +x entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
FROM kibana:5

RUN apt-get update && \
    apt-get install -y \
    curl \
    jq \
    netcat \
    && rm -rf /var/lib/apt/lists/*

# Add Containerpilot and set its configuration
ENV CONTAINERPILOT_VER 2.5.1
ENV CONTAINERPILOT file:///etc/containerpilot.json

RUN export CONTAINERPILOT_CHECKSUM=b56a9aff365fd9526cd0948325f91a367a3f84a1 \
    && wget -O /tmp/containerpilot.tar.gz \
         "https://github.com/joyent/containerpilot/releases/download/${CONTAINERPILOT_VER}/containerpilot-${CONTAINERPILOT_VER}.tar.gz" \
    && echo "${CONTAINERPILOT_CHECKSUM}  /tmp/containerpilot.tar.gz" | sha1sum -c \
    && tar zxf /tmp/containerpilot.tar.gz -C /usr/local/bin \
    && rm /tmp/containerpilot.tar.gz

# Add our configuration files and scripts
COPY /etc/containerpilot.json /etc
COPY /bin/manage.sh /usr/local/bin

WORKDIR /usr/share/kibana

COPY config ./config

EXPOSE 5601

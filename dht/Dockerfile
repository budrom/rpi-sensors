FROM resin/rpi-raspbian:jessie

RUN apt-get update && apt-get remove python && apt-get autoremove && apt-get install -y \
    python3 \
    python3-urllib3 \
    python3-dev \
    python3-pip \
    python3-virtualenv \
    --no-install-recommends && \
    rm -rf /var/lib/apt/lists/* && \
    ln -s /usr/bin/python3 /usr/bin/python && \
    pip3 install pyserial elasticsearch && \
    apt-get remove python3-dev python3-pip && \
    apt-get -y autoremove && apt-get clean && rm -rf /tmp/*

RUN apt-get update && apt-get install -y \
    git-core \
    build-essential \
    gcc \
    python3-dev \
    python3-pip \
    --no-install-recommends && \
    rm -rf /var/lib/apt/lists/* && \
    cd /tmp/ && git clone git://git.drogon.net/wiringPi && \
    cd wiringPi && ./build && \
    pip3 install wiringpi2 && \
    cd /tmp/ && git clone https://github.com/adafruit/Adafruit_Python_DHT.git && \
    cd Adafruit_Python_DHT && python setup.py install && \
    cd / && apt-get remove git-core build-essential python3-dev python3-pip && \
    apt-get -y autoremove && apt-get clean && rm -rf /tmp/*

COPY reader.py /
ENTRYPOINT ["python", "reader.py"]

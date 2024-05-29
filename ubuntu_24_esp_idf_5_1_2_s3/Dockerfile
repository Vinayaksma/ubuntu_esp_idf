# Use a base image with Ubuntu 24.04
FROM ubuntu:24.04
# Set noninteractive mode during package installations
ARG DEBIAN_FRONTEND noninteractive
# Install dependencies
RUN apt-get update && \
    apt-get install -y \
    git \
        wget \
        flex \
        bison \
        gperf \
        python3 \
        python3-pip \
        python3-venv \
        cmake \
        ninja-build \
        ccache \
        libffi-dev \
        libssl-dev \
        dfu-util \
        libusb-1.0-0 \
        curl \
        jq

RUN pip3 install jinja2
WORKDIR /esp
RUN git clone -b v5.1.2 --recursive https://github.com/espressif/esp-idf.git
ENV IDF_PATH /esp/esp-idf
ENV PATH $PATH:$IDF_PATH/tools
# RUN esp-idf/install.sh esp32s3
RUN /bin/bash -c "$IDF_PATH/install.sh esp32s3"
# RUN /bin/bash -c "source $IDF_PATH/export.sh"
RUN echo 'alias get_idf=". $IDF_PATH/export.sh"' >> /root/.bashrc
RUN echo "ESP-IDF Docker image based on v5.1.2 successfully built!"
COPY entrypoint.sh entrypoint.sh
RUN chmod +x /esp/entrypoint.sh
ENTRYPOINT [ "/esp/entrypoint.sh" ]
WORKDIR /
CMD [ "/bin/bash" ]

# Set the default command to launch bash
# CMD ["/bin/bash", "-c", "source $IDF_PATH/export.sh"]
ARG BASE_CONTAINER=jupyter/minimal-notebook
FROM $BASE_CONTAINER

LABEL maintainer="NCHC"

USER root

RUN apt-get update && apt-get install -yq wget --no-install-recommends \
    software-properties-common \
    gnupg2 \
    apt-utils \
    build-essential \
    python-dev \
    libmysqlclient-dev \
    libssl-dev \
    && wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list' \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
    google-chrome-stable \
    && rm -rf /var/lib/apt/lists/* \
#    && apt-get purge --auto-remove -y curl \
    && rm -rf /src/*.deb

COPY requirements.txt /tmp/
COPY chromedriver /usr/bin/
COPY $PWD/jupyter_notebook_config.py /etc/jupyter/jupyter_notebook_config.py
RUN chmod +x /usr/bin/chromedriver
RUN pip3 install -r /tmp/requirements.txt

USER $NB_UID

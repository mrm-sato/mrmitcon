FROM ubuntu:20.04

ARG apt_get_server=ftp.jaist.ac.jp/pub/Linux
ARG username=mrmitu
ARG useruid=202305
ARG usergid=${useruid}

WORKDIR /opt
#タイムゾーンの設定
ENV TZ=Asia/Tokyo
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
#aptでの取得
RUN \
    sed -i s@archive.ubuntu.com@${apt_get_server}@g /etc/apt/sources.list && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
    python3.9 \
    python3-pip \
    curl \
    git \
    wget \
    sudo \
    tzdata \
    nodejs \
    npm
#インストールのクリーン
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN pip install --no-cache-dir \
    JPype1 \
    jupyter \
    jupyterlab\
    pandas \
    numpy \
    seaborn \
    scipy \
    scikit-learn \
    matplotlib \
    plotly \
    requests \
    beautifulsoup4 \
    Pillow \
    pyNetLogo \
    SALib \
    opencv-python

RUN \
    groupadd --gid ${usergid} ${username} && \
    useradd -s /bin/bash --uid ${useruid} --gid ${usergid} -m ${username} && \
    echo ${username} ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/${username} && \
    chmod 0440 /etc/sudoers.d/${username} 


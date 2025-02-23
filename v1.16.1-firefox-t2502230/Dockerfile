FROM kasmweb/firefox:1.16.1
ARG DEBIAN_FRONTEND=noninteractive

USER root
RUN set -eux; echo "配置源"; \
    rm -f /etc/localtime; \
    ln -snf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo "Asia/Shanghai" > /etc/timezone; \
    sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list; \
    sed -i 's/security.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list; \
    apt-get update; apt-get install -y --no-install-recommends ca-certificates netbase curl wget sudo; \
    sed -i 's/http:/https:/g' /etc/apt/sources.list; \
    apt-get clean; \
    rm -rf /var/lib/apt/lists/*;

RUN set -eux; \
    echo "删除已有语言设置"; \
    rm -f /etc/default/locale; \
    rm -rf /var/lib/locales/supported.d/*; \
    echo "设置语言包"; \
    apt-get update; \
    apt-get install -y --no-install-recommends locales fonts-wqy-zenhei fonts-wqy-microhei fonts-noto-cjk fcitx-libpinyin ibus-pinyin; \
    locale-gen zh_CN.UTF-8 en_US.UTF-8; \
    echo 'LANG=zh_CN.UTF-8' > /etc/default/locale; \
    echo 'LC_ALL=zh_CN.UTF-8' >> /etc/default/locale; \
    echo 'LANGUAGE="zh_CN:zh:en_US:en"' >> /etc/default/locale; \
    update-locale LANG=zh_CN.UTF-8 LC_ALL=zh_CN.UTF-8 LANGUAGE="zh_CN:zh:en_US:en"; \
    apt-get clean; \
    rm -rf /var/lib/apt/lists/*

RUN set -eux; echo "常用软件包"; \
    apt-get update; \
    apt-get install -y --no-install-recommends \
    virt-manager icedtea-netx \
    cron openssh-server rsyslog \
    jq bc tmux socat zip unzip vim git tree sshpass psmisc bash-completion \
    iproute2 iputils-ping net-tools telnet nfs-common; \
    apt-get clean; \
    rm -rf /var/lib/apt/lists/*

RUN set -eux; echo "设置 sudo 权限"; \
    echo "kasm-user ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/kasm-user;

ENV LANG=zh_CN.UTF-8
ENV LANGUAGE=zh_CN.UTF-8:en_US
ENV LC_ALL=zh_CN.UTF-8
USER kasm-user

LABEL org.opencontainers.image.source=https://github.com/lwmacct/250223-kasmweb
LABEL org.opencontainers.image.description="kasmweb/firefox:1.16.1"
LABEL org.opencontainers.image.licenses=MIT

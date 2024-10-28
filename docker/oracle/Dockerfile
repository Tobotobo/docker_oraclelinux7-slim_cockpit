FROM oraclelinux:7-slim

COPY ./ol7_developer_EPEL.repo /etc/yum.repos.d/
RUN yum reinstall -y \
        glibc-common \
    && yum install -y \
        supervisor \
        nano \
        cockpit \
        openssh-clients

# ロケール及びタイムゾーンを日本に設定
RUN localedef -f UTF-8 -i ja_JP ja_JP.UTF-8 \
    && localedef -f UTF-8 -i ja_JP ja.UTF-8 \
    && echo 'LANG=ja_JP.UTF-8' > /etc/locale.conf \
    && ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime
ENV LANG="ja_JP.UTF-8" \
    LANGUAGE="ja_JP:ja" \
    LC_ALL="ja_JP.UTF-8" \
    TZ="Asia/Tokyo"

# Supervisor
COPY supervisord.conf /etc/supervisor/
RUN mkdir -p /var/run/supervisor /var/log/supervisor \
    && chmod -R 755 /var/run/supervisor /var/log/supervisor

# dbus
RUN mkdir -p /var/run/dbus

RUN echo "root:root" | chpasswd

EXPOSE 9090
CMD ["/usr/bin/supervisord", "-n", "-c", "/etc/supervisor/supervisord.conf"]

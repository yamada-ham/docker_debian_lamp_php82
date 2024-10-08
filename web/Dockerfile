FROM debian:11-slim

RUN apt update

# 回答求められたらデフォルト
ENV DEBIAN_FRONTEND=noninteractive

RUN apt -y install wget curl vim lsof sudo tree cron supervisor vsftpd git default-mysql-server postgresql-client redis-server

# PHP
RUN apt update && apt install -y lsb-release apt-transport-https ca-certificates wget gnupg
RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
RUN echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
RUN apt update
RUN apt install -y php8.2
# デフォルトの php のバージョン
RUN update-alternatives --set php /usr/bin/php8.2

# php package
RUN apt install -y php8.2-mysql php8.2-mbstring php8.2-gd php8.2-xml php8.2-xmlrpc php8.2-curl php8.2-zip php8.2-intl php8.2-bcmath php8.2-soap php8.2-ldap php8.2-apcu

RUN touch /var/log/php_errors.log && chmod 777 /var/log/php_errors.log

# Apache
RUN apt -y install apache2 libapache2-mod-php8.2

# composer
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer

# phpMyAdmin
# RUN curl -OL https://files.phpmyadmin.net/phpMyAdmin/5.2.1/phpMyAdmin-5.2.1-all-languages.tar.gz && \
# tar xzvf phpMyAdmin-5.2.1-all-languages.tar.gz && \
# mv phpMyAdmin-5.2.1-all-languages phpMyAdmin && \
# rm -rf phpMyAdmin-5.2.1-all-languages.tar.gz && \
# mv ./phpMyAdmin /usr/share/

# Node.js Angular
RUN curl -sL https://deb.nodesource.com/setup_22.x | bash - && \
    apt install -y nodejs && \
    npm install -g @angular/cli

# ftp 準備
RUN mkdir -p /etc/vsftpd && touch /etc/vsftpd/user_list && mkdir -p /etc/vsftpd/user_conf && touch /etc/vsftpd/chroot_list && mkdir -p /var/run/vsftpd/empty

# ftpユーザー作成
RUN useradd -m -d /home/ftp-user ftp-user && echo "ftp-user:tnTat7q5" | chpasswd

# 日本時間
ENV TZ=Asia/Tokyo
# 言語設定 UTF-8を使えるようにする
ENV LC_ALL C.UTF-8

COPY cmd.sh /cmd.sh
CMD ["sh" , "/cmd.sh"]
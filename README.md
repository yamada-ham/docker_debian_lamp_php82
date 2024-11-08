# コンテナ型LAMP環境

## システム環境
```
PHP8.2
MySQL8
Apache
Composer
Node.js ver18.x
FTP
Ngrok
```


## メモ
```
./web/html にアプリケーションを設置する

# バーチャルホスト設定ファイル
web/volumes/apache2/sites-available/v_host.conf
web/volumes/apache2/ports.conf

# phpMyAdmin 設定ファイル設置
web/volumes/apache2/sites-available/phpMyAdmin.conf

# phpMyAdminのホストをDockerのDBに設定 $cfg['Servers'][$i]['host'] = 'db';
web/volumes/phpMyAdmin/config.inc.php


# apache設定変更の反映
$ a2ensite v_host.conf
$ service apache2 reload
```
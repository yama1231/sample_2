
カレンダー
・フレームワークなし
・index.phpのみの記載

他：
ルーティングは、dockerのweb用のコンテナ内で設定されている。
変更する場合は、webコンテナ内にログイン後、以下のコマンドを実行する。
例）　sed -i 's/DirectoryIndex index.html index.php/DirectoryIndex index.php index.html/' /etc/apache2/conf-available/docker-php.conf 
//docker-php.confの内容を書き換える（左から右に変更するため、右側に反映したいファイルを記載する）　DirectoryIndex index.html index.php　-> DirectoryIndex index.php index.html/
service apache2 restart
//反映のため、Apache再起動

経緯：
dir.conf(※１)にDirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm　とあるが、
docker-php.conf(※２)にDirectoryIndex disabledとあり、その後にDirectoryIndex index.php index.htmlと記述してあるため、現状index.phpの内容が最初の表示対象となっている。

各ディレクトリ：
※１　/etc/apache2/mods-enabled/dir.conf
※２　/etc/apache2/conf-available/docker-php.conf 

追記：
dockerfileでルーティングの変更が可能らしいので、一旦ここまでにする。

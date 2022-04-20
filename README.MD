# Version
PHP 7.4.27<br>
nginx 1.20.2<br>
mysql 8.0.27

# Usage
動画にまとめているので詳しくは[こちら](https://youtu.be/A5BUus6S-sk)をご覧ください


1. リポジトリをクローンする。<br>
    SSH
    ```
    git clone git@github.com:nabecima/laravel_on_win.git
    ```
    HTTPS
    ```
    git clone https://github.com/nabecima/laravel_on_win.git
    ```

1. 受講生から共有されたプロジェクトをクローンしたディレクトリ配下に移動させ、プロジェクト名(フォルダ名)を`backend`に変更する

    ![change_foldername](https://user-images.githubusercontent.com/66292801/164203245-bbbc4d40-fd9a-4363-9192-3c01f9f6e820.gif)
1. Laravelのプロジェクトファイルに`.env`がない場合、カレントディレクトリがlaravel_on_m1macの状態で以下のコマンドを実行し、`.env.example`をコピーして`.env`を作成する
    ```
    cp backend/.env.example backend/.env
    ```
1. `node_modules`を削除
1. `docker-compose.yml`と同じ階層にある.envの`DB_NAME`をプロジェクトで使用するDB名にする(backend内の.envにDB名が記載されています)
1. backendディレクトリ内の.envを編集

    ![project_env](https://user-images.githubusercontent.com/66292801/147135560-e033e3af-4c25-4d32-9bfb-63b135047368.png)
3. コンテナをバックグラウンドで起動
    ```
    docker compose up -d --build
    ```
1. コンテナが起動しているか確認(STATUSがrunningになっていればOK)
    ```
    docker compose ps
    ```
    ![service_status](https://user-images.githubusercontent.com/66292801/147135163-03781fc8-2d65-4a94-a445-7fea003121cc.png)

1. パッケージをインストール(PHP)
    ```
    docker compose exec app composer install
    ```
1. アプリケーションキーを作成
    ```
    docker compose exec app php artisan key:generate
    ```
3. .envの内容を反映
    ```
    docker compose exec app php artisan config:cache
    ```

1. パッケージをインストール(Node.js)
    ```
    docker compose exec app npm install
    ```
1. マイグレーションファイルを適用する
    ```
    docker compose exec app php artisan migrate
    ```
1. 動作確認

    [アプリのプレビュー(localhost:8000)](http://localhost:8000/)
    
    [phpMyAdmin(localhost:8080)](http://localhost:8080/)
    
    phpMyAdminはコンテナ起動後30秒以上経過してから開くようにしてください。<br>
    もしそれ以前に開いた場合はある程度時間が経ってからページを再読み込みしてください。
1. エラーなどの確認作業が終了したらコンテナを破棄する
    ```
    docker compose down
    ```
基本的には上記コマンドを入力すればプレビューできます。<br>
その他コマンドを入力する必要がある場合は`docker compose exec app`以降に実行したいコマンドを入れて実行してください。


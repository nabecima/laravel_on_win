# Version
PHP 7.4.27<br>
nginx 1.20.2<br>
mysql 8.0.27

# Usage
1. リポジトリをクローンする。<br>
    SSH
    ```
    git clone git@github.com:nabecima/laravel_on_m1mac.git
    ```
    HTTPS
    ```
    git clone https://github.com/nabecima/laravel_on_m1mac.git
    ```

3. 受講生から共有されたプロジェクトをクローンしたディレクトリ配下に移動させる(.zipはNG)
4. プロジェクト名(フォルダ名)を`backend`にリネーム
5. `node_modules`を削除
6. docker-compose.ymlと同じ階層にある.envの`DB_NAME`をプロジェクトで使用するDB名にする
7. コンテナをバックグラウンドで起動

    ```
    docker compose up -d
    ```

8. コンテナが起動しているか確認(STATUSがrunningになっていればOK)

    ```
    docker compose ps
    ```
    ![service_status](https://user-images.githubusercontent.com/66292801/147135163-03781fc8-2d65-4a94-a445-7fea003121cc.png)

9. backendディレクトリ内の.envを編集

    ![project_env](https://user-images.githubusercontent.com/66292801/147135560-e033e3af-4c25-4d32-9bfb-63b135047368.png)

10. .envの内容を反映

    ```
    docker compose exec app php artisan config:cache
    ```

11. パッケージをインストール

    ```
    docker compose exec app npm install
    ```

12. マイグレーションファイルを適用する

    ```
    docker compose exec app php artisan migrate
    ```

13. エラーなどの確認作業が終了したらコンテナを破棄する

    ```
    docker compose down
    ```

基本的には上記コマンドを入力すればプレビューできます。<br>
その他コマンドを入力する必要がある場合は`docker compose exec app`以降に実行したいコマンドを入れて実行してください。

[アプリのプレビュー(localhost:8080)](http://localhost:8000/)

[phpMyAdmin(localhost:8080)](http://localhost:8080/)<br>
phpMyAdminはコンテナ起動後30秒以上経過してから開くようにしてください。<br>
もしそれ以前に開いた場合はある程度時間が経ってからページを再読み込みしてください。


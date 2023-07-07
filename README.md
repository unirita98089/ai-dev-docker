# Docker Compose Setup for Sample App

このREADMEは、MySQL、Backend(PHPを用いたアプリケーション)、およびFrontend(Node.jsを用いたアプリケーション)の3つのサービスを含むDocker Composeセットアップの使用と管理に関する情報を提供します。  
(Written by ChatGPT-4)

## サービス

### 1. MySQL Database (`db`)

- MySQL 8.0を使用します。
- ポート3309でリッスンします（Dockerコンテナ内のポート3306にマップ）。
- 環境変数で、rootパスワードとデータベース名を設定します。
- ボリューム`dbdata`と`logs`を使用して、データとログを永続化します。

### 2. Backend (`backend`)

- PHPベースのアプリケーションで、このプロジェクトのルートディレクトリからビルドされます。
- ポート8000でリッスンします。
- MySQLデータベースサービス(`db`)に依存します。
- 作業ディレクトリは `/var/www/html` で、このディレクトリは `../ai-dev-backend` にマップされています。

### 3. Frontend (`frontend`)

- Node.js (バージョン14) ベースのアプリケーションです。
- ポート3001でリッスンします（Dockerコンテナ内のポート3000にマップ）。
- 作業ディレクトリは `/app` で、このディレクトリは `../ai-dev-frontend` にマップされています。
- `NODE_ENV` 環境変数は `development` に設定されています。

## 使い方

1. 最初に、Dockerがインストールされていることを確認してください。詳細は[Dockerの公式ドキュメント](https://docs.docker.com/get-docker/)を参照してください。

2. 次に、このリポジトリをクローンします：

    ```
    git clone git@github.com:unirita98089/ai-dev-docker.git
    ```
   
3. 同じ階層に、フロントエンド、バックエンドのリポジトリもクローンします：

    ```
    git clone git@github.com:unirita98089/ai-dev-frontend.git
    ```
    ```
    git clone git@github.com:unirita98089/ai-dev-backend.git
    ```
   以下のディレクトリ構成になっていることを確認してください  
    ```
    .  
    ├── ai-dev-backend  
    ├── ai-dev-docker  
    └── ai-dev-frontend  
    ```


4. リポジトリのディレクトリに移動します：

    ```
    cd ai-dev-docker
    ```

5. 最後に、以下のコマンドでDocker Composeを実行します：

    ```
    docker-compose up -d
    ```

これにより、すべてのサービスがバックグラウンドで起動します。

6. 必要に応じて、以下のコマンドでコンテナのログを確認します：

    ```
    docker-compose logs -f
    ```

7. すべてのコンテナを停止するには、以下のコマンドを実行します：

    ```
    docker-compose down
    ```

## 注意事項

- デフォルトで設定されているMySQLのrootパスワードはセキュリティ上の理由から変更することを強くお勧めします。パスワードを変更するには、`docker-compose.yml`ファイル内の `MYSQL_ROOT_PASSWORD` 環境変数を更新します。
- 同様に、開発環境での使用を目的としたDocker Composeセットアップなので、プロダクション環境での使用前にセキュリティ設定を適切にレビューして調整してください。
- バックエンドとフロントエンドのボリュームはプロジェクトディレクトリからの相対パスに基づいています。それらのサービスが異なるディレクトリにある場合は、適切にパスを更新してください。

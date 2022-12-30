# Docker 環境で Go の検証環境を構築

## 技術スタック

* Go 1.18

## 構築

1. クローン
   * `git clone https://github.com/ysato-theyou/PoC-go-docker.git`
2. ビルド
   * `docker build -t ysofficellc/go-aws-eks:1.0.0 .`
3. コンテナ立ち上げ（テスト）
    * `docker run --rm -p 8080:80 ysofficellc/go-aws-eks:1.0.0`
4. 疎通テスト
   * curl で http://localhost:8080 へアクセス
    ```shell
     curl localhost:8080
    Hello, World!
    ```

## Docker Hub へ登録

登録済み Docker Hub アカウントへログインしている状態で、イメージを push する

1. イメージプッシュ
   - `docker push ysofficellc/go-aws-eks:v2`

## AWS EKS へデプロイ

### クラスター作成

- `eksctl create cluster --name=go-kube-cluster --nodes=2 --node-type=t2.micro`

### Kubernetes へ kubectl を用いてデプロイする

1. Deployments 投入
   - `kubectl apply -f kubernetes/deployment.yaml`
2. Service 投入
   - `kubectl apply -f kubernetes/service.yaml`
3. 動作確認
   - `kubectl get nodes`
   - `kubectl get pods`
   - `kubectl get services`
     - 参考
        ```shell
        ```
         ![image](https://user-images.githubusercontent.com/108514223/210063233-c4711c78-01a4-45b9-9541-fae70e731778.png)

## 参考資料
* [Build your Go image](https://matsuand.github.io/docs.docker.jp.onthefly/language/golang/build-images/)
* [dockerを使ってgoの環境構築](https://zenn.dev/tomi/articles/2020-10-14-go-docker)
* [Create a Docker container with golang 1.18 web server](https://medium.com/@felipelimao/create-a-docker-container-with-golang-1-18-web-server-7222b1ef824f)
* [Deploy a Laravel App to Amazon EKS in 5 minutes](https://gbengaoni.com/blog/Deploy-a-Laravel-App-to-Amazon-EKS-in-5-minutes-a94a41436157)

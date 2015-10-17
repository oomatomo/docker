
# Install

## for Mac

```
brew install docker
brew cask install docker-machine docker-compose
```


## docker-machine

https://docs.docker.com/machine/#osx-and-linux

dockerを利用する土台用の仮想環境を構築する
(boot2dockerではじめに作成した環境と同じ)
boot2docker init
boot2docker ssh で接続した環境

```
docker-machine create -d virtualbox --virtualbox-disk-size "20000" --virtualbox-memory "2048" dev
```

```
eval "$(docker-machine env dev)"
docker ps
docker-machine ip dev
```

## docker compose

複数のDockerを起動させる

```
# 一括でbuildする
docker-compose build
# 一括で起動する docker run と同じ -dでバックグラウンドでの起動
docker-compose up
docker-compose up -d
# 一括で削除
docker-compose rm
```

## dockerにアクセスする方法

```
# dockerを動かしているサーバにアクセス
docker-machine ssh dev
tce-load -wil util-linux
# アクセスしたいコンテナIDを設定すればおk
sudo nsenter --target $(docker inspect --format '{{.State.Pid}}' アクセスしたいコンテナID) --mount --uts --ipc --net --pid
# 例
sudo nsenter --target $(docker inspect --format '{{.State.Pid}}' 2f1688b9fbe9) --mount --uts --ipc --net --pid
```

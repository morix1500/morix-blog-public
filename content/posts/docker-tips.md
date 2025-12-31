---
title: "Dockerの便利なTips"
date: 2024-12-30
description: "Dockerを使う上で知っておくと便利なTipsを紹介します。"
tags:
  - Docker
  - インフラ
---

## はじめに

日常的にDockerを使う中で知っておくと便利なTipsを紹介します。

## 1. 不要なイメージの削除

```bash
# 使用していないイメージを削除
docker image prune -a

# 使用していないボリュームも含めて削除
docker system prune -a --volumes
```

## 2. コンテナのログを確認

```bash
# リアルタイムでログを追跡
docker logs -f container_name

# 最新100行のみ表示
docker logs --tail 100 container_name
```

## 3. マルチステージビルド

Dockerfileを効率化するためのマルチステージビルドの例：

```dockerfile
# ビルドステージ
FROM golang:1.21 AS builder
WORKDIR /app
COPY . .
RUN go build -o main .

# 実行ステージ
FROM alpine:latest
COPY --from=builder /app/main /main
CMD ["/main"]
```

## 参考リンク

Docker公式ドキュメントも参考にしてください。

{{< blog-card "https://docs.docker.com/get-started/" >}}

{{< blog-card "https://zenn.dev/suzuki_hoge/books/2022-03-docker-practice-8ae36c33424b59" >}}

## まとめ

これらのTipsを活用して、効率的なDocker開発を行いましょう。

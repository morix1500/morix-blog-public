---
title: "Goのエラーハンドリング入門"
date: 2024-12-29
description: "Go言語におけるエラーハンドリングの基本的な書き方を解説します。"
tags:
  - Go
  - プログラミング
---

## はじめに

Go言語ではエラーハンドリングが独特な書き方になっています。この記事では基本的なパターンを紹介します。

## 基本的なエラーハンドリング

```go
func readFile(path string) ([]byte, error) {
    data, err := os.ReadFile(path)
    if err != nil {
        return nil, fmt.Errorf("failed to read file: %w", err)
    }
    return data, nil
}
```

## エラーのラップ

Go 1.13以降では`%w`を使ってエラーをラップできます：

```go
if err != nil {
    return fmt.Errorf("operation failed: %w", err)
}
```

## errors.Is と errors.As

```go
// エラーの種類を確認
if errors.Is(err, os.ErrNotExist) {
    fmt.Println("ファイルが存在しません")
}

// エラーの型を取得
var pathErr *os.PathError
if errors.As(err, &pathErr) {
    fmt.Println("パス:", pathErr.Path)
}
```

## カスタムエラー型

```go
type ValidationError struct {
    Field   string
    Message string
}

func (e *ValidationError) Error() string {
    return fmt.Sprintf("%s: %s", e.Field, e.Message)
}
```

## まとめ

Goのエラーハンドリングは明示的で分かりやすい設計になっています。適切にエラーを処理することで、堅牢なアプリケーションを構築できます。

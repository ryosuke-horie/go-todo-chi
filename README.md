# TodoリストAPIをテーマにしたGo, chi, xo, sqlのキャッチアップ

## スタック

- **chi**
  - [GitHubリポジトリ](https://github.com/go-chi/chi)
  - GoでHTTPサービスを構築するための軽量に構成可能なルーター らしい
    - REST APIサービスの作成に役に立つ
    - プロジェクト構造、保守性、標準のhttpハンドラ、生産性、大規模システムを多数の小さな部品に分解することを考慮した設計をうたう。
  - インストール
    - `go get -u github.com/go-chi/chi`

- **xo**
  - [GitHubリポジトリ](https://github.com/xo/xo)
  - SQL DB用のGoコードを生成するCLIツール
  - DBスキーマやカスタムクエリに基づいて寛容的なコードを生成するもの
    - SQLクエリに基づいた型安全なGo関数を生成
    - テーブル対応の構造体の自動生成
    - CRUD操作の自動生成
    - カスタムクエリの自動生成
  - （ただの感想）
    - 自動生成されるコードの品質が気になる。
    - 今までLaravelのEloquentを使って書いてきたものに比べてコードの見通しや使い勝手が気になる。

## chiでHello World

### 1. Goのインストールを確認
```bash
go version
# go version go1.23.2 linux/amd64
```

### 2. Goモジュールの初期化
```bash
go mod init todo-go-chi
```

### 3. chiのインストール
```bash
go get -u github.com/go-chi/chi/v5
```

### 4. Hollo Worldのコーディング
[参考元](https://github.com/go-chi/chi/blob/master/_examples/hello-world/main.go)

```go
package main

import (
	"net/http"

	"github.com/go-chi/chi/v5"
)

func main() {
	// ルーターを作成
	r := chi.NewRouter()

	// /で受け付けるハンドラーを登録
	r.Get("/", func(w http.ResponseWriter, r *http.Request) {
		w.Write([]byte("hello chi"))
	})

	// ポート3333でサーバーを起動
	http.ListenAndServe(":3333",r)
}
```

### 5. サーバーの起動
```bash
go run main.go
```
`http://localhost:3333/`にアクセスして`hello chi`が表示されることを確認した。

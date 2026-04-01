# Getting Started

## インストール

```bash
go get github.com/kqnade/vrcgo
```

## クイックスタート

### 基本認証

ユーザー名とパスワードでVRChatにログインします。2要素認証にも対応しています。

```go
package main

import (
    "context"
    "fmt"
    "log"

    "github.com/kqnade/vrcgo/shared"
    "github.com/kqnade/vrcgo/vrcapi"
)

func main() {
    client, err := vrcapi.NewClient()
    if err != nil {
        log.Fatal(err)
    }

    err = client.Authenticate(context.Background(), shared.AuthConfig{
        Username: "your-username",
        Password: "your-password",
    })
    if err != nil {
        log.Fatal(err)
    }

    user, err := client.GetCurrentUser(context.Background())
    if err != nil {
        log.Fatal(err)
    }

    fmt.Printf("Logged in as: %s\n", user.DisplayName)
}
```

### 2要素認証 (2FA)

```go
err = client.Authenticate(context.Background(), shared.AuthConfig{
    Username: "your-username",
    Password: "your-password",
    TOTPCode: "123456", // 認証アプリのコード
})
```

### Cookie認証

一度ログインしてCookieを保存しておけば、次回以降は再認証なしで利用できます。

```go
client, _ := vrcapi.NewClient()

// Cookieを保存
client.Authenticate(ctx, config)
client.SaveCookies("cookies.json")

// 次回: Cookieを読み込んで認証
if err := client.LoadCookies("cookies.json"); err != nil {
    log.Fatal(err)
}

user, err := client.GetCurrentUser(context.Background())
```

### クライアントオプション

```go
client, err := vrcapi.NewClient(
    vrcapi.WithUserAgent("my-app/1.0"),
    vrcapi.WithTimeout(30 * time.Second),
    vrcapi.WithProxy("http://proxy.example.com:8080"),
)
```

## WebSocketでリアルタイムイベントを受信

```go
import (
    "github.com/kqnade/vrcgo/shared"
    "github.com/kqnade/vrcgo/vrcapi"
    "github.com/kqnade/vrcgo/vrcws"
)

// 先にREST APIクライアントで認証が必要
ws, err := vrcws.New(context.Background(), client)
if err != nil {
    log.Fatal(err)
}
defer ws.Close()

// フレンドがオンラインになったとき
ws.OnFriendOnline(func(e shared.FriendOnlineEvent) {
    fmt.Printf("%s がオンラインになりました\n", e.UserID)
})

// 通知を受信
ws.OnNotification(func(n shared.NotificationEvent) {
    fmt.Printf("通知: %s\n", n.Message)
})

// すべてのイベントをキャッチ
ws.On("*", func(e shared.Event) {
    fmt.Printf("イベント: %s\n", e.Type)
})

// 接続を維持
ws.Wait()
```

## エラーハンドリング

`shared` パッケージのヘルパー関数でエラー種別を判定できます。

```go
err := client.Authenticate(ctx, config)
if err != nil {
    apiErr, ok := err.(*shared.APIError)
    if !ok {
        log.Fatal(err)
    }
    switch {
    case apiErr.IsAuthenticationError():
        fmt.Println("認証情報が正しくありません")
    case apiErr.IsRateLimitError():
        fmt.Println("レート制限に達しました")
    case apiErr.IsNotFoundError():
        fmt.Println("リソースが見つかりません")
    default:
        fmt.Printf("APIエラー: %v\n", err)
    }
}
```

## 重要事項

::: warning 注意
- これはコミュニティ主導のプロジェクトであり、VRChat公式サポートはありません
- Photonサーバーへの直接アクセスは禁止されています
- APIのレート制限を遵守してください
- VRChatの[利用規約](https://hello.vrchat.com/legal)に従ってください
:::

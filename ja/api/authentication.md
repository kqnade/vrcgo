# 認証 (Authentication)

## 概要

`vrcapi` パッケージは Cookieベースのセッション管理と2要素認証をサポートします。

## メソッド

### `Authenticate(ctx, config)`

ユーザー名とパスワードでVRChatにログインします。2FA (TOTP) が必要な場合は `TOTPCode` を指定してください。

```go
err := client.Authenticate(ctx, shared.AuthConfig{
    Username: "your-username",
    Password: "your-password",
    TOTPCode: "123456", // 2FA不要なら省略可
})
```

**パラメータ**

| フィールド | 型 | 説明 |
|-----------|------|------|
| `Username` | `string` | VRChatのユーザー名 |
| `Password` | `string` | パスワード |
| `TOTPCode` | `string` | TOTPコード（2FA有効時のみ必要） |

**エラー**

- 認証情報が不正な場合: `*shared.APIError` (401)
- 2FAコードが必要なのに未指定の場合: `error`
- 2FAコードが不正な場合: `error`

---

### `GetCurrentUser(ctx)`

現在ログイン中のユーザー情報を取得します。

```go
user, err := client.GetCurrentUser(ctx)
if err != nil {
    log.Fatal(err)
}
fmt.Println(user.DisplayName)
```

**戻り値**: `(*shared.CurrentUser, error)`

---

### `Logout(ctx)`

現在のセッションをログアウトします。

```go
err := client.Logout(ctx)
```

---

### `SaveCookies(path)`

現在のセッションCookieをJSON形式でファイルに保存します。

```go
err := client.SaveCookies("cookies.json")
```

---

### `LoadCookies(path)`

保存済みCookieファイルを読み込み、再認証なしでセッションを復元します。

```go
err := client.LoadCookies("cookies.json")
if err != nil {
    // Cookieが無効または期限切れ → 再認証が必要
}
```

## クライアント生成オプション

`vrcapi.NewClient()` にオプションを渡すことでHTTPクライアントの動作をカスタマイズできます。

```go
client, err := vrcapi.NewClient(
    vrcapi.WithUserAgent("my-app/1.0 contact@example.com"),
    vrcapi.WithTimeout(30 * time.Second),
    vrcapi.WithProxy("http://proxy.example.com:8080"),
)
```

| オプション | 説明 |
|-----------|------|
| `WithUserAgent(ua)` | User-Agentヘッダーを設定します |
| `WithTimeout(d)` | HTTPリクエストのタイムアウトを設定します |
| `WithProxy(url)` | プロキシサーバーを設定します |

::: tip
VRChatのAPIポリシーでは、識別可能なUser-Agentの設定が推奨されています。  
例: `"MyApp/1.0 my-contact@example.com"`
:::

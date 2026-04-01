# システム (System)

## メソッド

### `GetConfig(ctx)`

VRChatのシステム設定を取得します。APIの設定値や利用規約バージョンなどが含まれます。

```go
config, err := client.GetConfig(ctx)
```

---

### `GetSystemTime(ctx)`

サーバーの現在時刻を取得します。

```go
t, err := client.GetSystemTime(ctx)
fmt.Println(t)
```

---

### `GetInfoPushes(ctx)`

VRChatからのシステム情報プッシュを取得します。

```go
pushes, err := client.GetInfoPushes(ctx)
```

---

### `GetCurrentOnlineUsers(ctx)`

現在オンライン中のユーザー総数を取得します。

```go
count, err := client.GetCurrentOnlineUsers(ctx)
fmt.Printf("オンラインユーザー数: %d\n", count)
```

---

### `GetHealth(ctx)`

APIのヘルス状態を確認します。

```go
health, err := client.GetHealth(ctx)
fmt.Printf("OK: %v, ServerName: %s\n", health.OK, health.ServerName)
```

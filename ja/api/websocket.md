# WebSocket

VRChatのパイプラインサーバーへのWebSocket接続を管理し、リアルタイムイベントを受信します。

## セットアップ

```go
import (
    "context"
    "github.com/kqnade/vrcgo/vrcws"
    "github.com/kqnade/vrcgo/shared"
)

// REST APIクライアントで事前に認証が必要
ws, err := vrcws.New(context.Background(), client)
if err != nil {
    log.Fatal(err)
}
defer ws.Close()

// ハンドラー登録後、接続を維持
ws.Wait()
```

## イベントハンドラー

### `On(eventType, handler)`

任意のイベント型にハンドラーを登録します。ワイルドカード `"*"` で全イベントをキャッチできます。

```go
ws.On("friend-online", func(e shared.Event) {
    fmt.Printf("Raw event: %s\n", e.Content)
})

ws.On("*", func(e shared.Event) {
    fmt.Printf("Any event: %s\n", e.Type)
})
```

### `OnNotification(handler)`

通知イベントを受信します。

```go
ws.OnNotification(func(n shared.NotificationEvent) {
    fmt.Printf("通知 [%s]: %s\n", n.Type, n.Message)
})
```

### `OnFriendOnline(handler)`

フレンドがオンラインになったとき。

```go
ws.OnFriendOnline(func(e shared.FriendOnlineEvent) {
    fmt.Printf("%s がオンラインになりました (場所: %s)\n", e.UserID, e.Location)
})
```

### `OnFriendOffline(handler)`

フレンドがオフラインになったとき。

```go
ws.OnFriendOffline(func(e shared.FriendOfflineEvent) {
    fmt.Printf("%s がオフラインになりました\n", e.UserID)
})
```

### `OnFriendLocation(handler)`

フレンドのロケーションが変わったとき。

```go
ws.OnFriendLocation(func(e shared.FriendLocationEvent) {
    fmt.Printf("%s が %s に移動しました\n", e.UserID, e.Location)
})
```

### `OnFriendActive(handler)`

フレンドがアクティブになったとき（ゲームを起動したなど）。

```go
ws.OnFriendActive(func(e shared.FriendActiveEvent) {
    fmt.Printf("%s がアクティブになりました\n", e.UserID)
})
```

### `OnFriendAdd(handler)` / `OnFriendDelete(handler)`

フレンドが追加・削除されたとき。

```go
ws.OnFriendAdd(func(e shared.FriendAddEvent) {
    fmt.Printf("%s とフレンドになりました\n", e.UserID)
})

ws.OnFriendDelete(func(e shared.FriendDeleteEvent) {
    fmt.Printf("%s とのフレンドが解消されました\n", e.UserID)
})
```

### `OnUserUpdate(handler)`

自分のユーザー情報が更新されたとき。

```go
ws.OnUserUpdate(func(e shared.UserUpdateEvent) {
    fmt.Printf("ユーザー情報が更新されました\n")
})
```

## 対応イベント一覧

| イベント型 | ハンドラー | 説明 |
|-----------|----------|------|
| `notification` | `OnNotification` | 通知 |
| `friend-online` | `OnFriendOnline` | フレンドがオンラインに |
| `friend-offline` | `OnFriendOffline` | フレンドがオフラインに |
| `friend-active` | `OnFriendActive` | フレンドがアクティブに |
| `friend-location` | `OnFriendLocation` | フレンドのロケーション変更 |
| `friend-add` | `OnFriendAdd` | フレンド追加 |
| `friend-delete` | `OnFriendDelete` | フレンド削除 |
| `friend-update` | ― | フレンド情報更新 |
| `user-update` | `OnUserUpdate` | 自分のユーザー情報更新 |
| `user-location` | ― | 自分のロケーション変更 |
| `notification-v2` | ― | 通知V2 |
| `notification-v2-update` | ― | 通知V2更新 |
| `notification-v2-delete` | ― | 通知V2削除 |
| `group-joined` | ― | グループ参加 |
| `group-left` | ― | グループ脱退 |
| `group-member-updated` | ― | グループメンバー更新 |
| `group-role-updated` | ― | グループロール更新 |

## 自動再接続

接続が切断された場合、WebSocketクライアントは自動的に再接続を試みます。

- 初回再接続遅延: **5秒**
- 最大遅延: **60秒**
- バックオフ倍率: **2倍**（指数バックオフ）

```go
// 再接続をキャンセルしたい場合は ctx をキャンセルする
ctx, cancel := context.WithCancel(context.Background())
ws, _ := vrcws.New(ctx, client)

// 切断して再接続しない
cancel()
ws.Wait()
```

## その他のメソッド

### `Close()`

WebSocket接続を閉じます。

```go
ws.Close()
```

### `Wait()`

接続が終了するまでブロックします。メインゴルーチンで呼び出すことで、プログラムを接続維持状態に保てます。

```go
ws.Wait()
```

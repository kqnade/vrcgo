# フレンド (Friends)

## メソッド

### `GetFriends(ctx, opts)`

フレンドリストを取得します。

```go
friends, err := client.GetFriends(ctx, shared.GetFriendsOptions{
    Offset:  0,
    N:       100,
    Offline: false, // trueにするとオフラインフレンドも取得
})
```

**戻り値**: `([]shared.Friend, error)`

---

### `GetFriendStatus(ctx, userId)`

指定ユーザーとのフレンド状態を取得します。

```go
status, err := client.GetFriendStatus(ctx, "usr_...")
fmt.Println(status.IsFriend)
fmt.Println(status.OutgoingRequest) // 送信済みリクエストあり
fmt.Println(status.IncomingRequest) // 受信済みリクエストあり
```

---

### `SendFriendRequest(ctx, userId)`

フレンドリクエストを送信します。

```go
notification, err := client.SendFriendRequest(ctx, "usr_...")
```

---

### `DeleteFriend(ctx, userId)`

フレンドを削除します。

```go
err := client.DeleteFriend(ctx, "usr_...")
```

---

### `AcceptFriendRequest(ctx, notificationId)`

受信したフレンドリクエストを承認します。

```go
err := client.AcceptFriendRequest(ctx, "not_...")
```

---

### `DeclineFriendRequest(ctx, notificationId)`

受信したフレンドリクエストを拒否します。

```go
err := client.DeclineFriendRequest(ctx, "not_...")
```

---

### `GetOnlineFriends(ctx)`

現在オンラインのフレンドを取得します。

```go
friends, err := client.GetOnlineFriends(ctx)
for _, f := range friends {
    fmt.Printf("%s - %s\n", f.DisplayName, f.Location)
}
```

---

### `GetOfflineFriends(ctx)`

現在オフラインのフレンドを取得します。

```go
friends, err := client.GetOfflineFriends(ctx)
```

## 型定義

### `shared.Friend`

| フィールド | 型 | 説明 |
|-----------|------|------|
| `ID` | `string` | ユーザーID |
| `DisplayName` | `string` | 表示名 |
| `Status` | `string` | ステータス |
| `Location` | `string` | 現在のロケーション |
| `IsFriend` | `bool` | フレンドかどうか |

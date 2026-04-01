# 通知 (Notifications)

::: tip
`details` フィールドはVRChat APIが文字列またはオブジェクトのどちらで返す場合もあります。  
`shared.NotificationDetails` 型がどちらも透過的に処理します。
:::

## メソッド

### `GetNotifications(ctx, opts)`

通知リストを取得します。

```go
notifications, err := client.GetNotifications(ctx, shared.GetNotificationsOptions{
    Type:   "all",
    Sent:   false,
    N:      100,
    After:  "2024-01-01T00:00:00.000Z",
})
```

**戻り値**: `([]shared.Notification, error)`

---

### `MarkNotificationAsRead(ctx, notificationId)`

通知を既読にします。

```go
notification, err := client.MarkNotificationAsRead(ctx, "not_...")
```

---

### `DeleteNotification(ctx, notificationId)`

通知を削除します。

```go
notification, err := client.DeleteNotification(ctx, "not_...")
```

---

### `ClearAllNotifications(ctx)`

すべての通知をクリアします。

```go
err := client.ClearAllNotifications(ctx)
```

---

### `SendNotification(ctx, req)`

通知を送信します。

```go
err := client.SendNotification(ctx, shared.SendNotificationRequest{
    UserID:  "usr_...",
    Type:    "message",
    Message: "Hello!",
})
```

---

### `SendInvite(ctx, userId, req)`

インスタンスへの招待を送信します。

```go
err := client.SendInvite(ctx, "usr_...", shared.SendInviteRequest{
    InstanceLocation: "wrld_...:12345~private(...)",
    MessageSlot:      0,
})
```

---

### `RespondToInvite(ctx, notificationId, req)`

招待に応答します。

```go
err := client.RespondToInvite(ctx, "not_...", shared.RespondToInviteRequest{
    ResponseSlot: 0,
})
```

---

### `RequestInvite(ctx, userId, instanceLocation)`

招待をリクエストします。

```go
err := client.RequestInvite(ctx, "usr_...", "wrld_...:12345")
```

## 型定義

### `shared.Notification`

| フィールド | 型 | 説明 |
|-----------|------|------|
| `ID` | `string` | 通知ID |
| `Type` | `string` | 通知種別 (`invite`, `friendRequest` など) |
| `Message` | `string` | メッセージ内容 |
| `SenderUserID` | `string` | 送信者のユーザーID |
| `SenderUsername` | `string` | 送信者のユーザー名 |
| `Details` | `NotificationDetails` | 詳細情報（種別によって内容が異なる） |
| `Created` | `string` | 作成日時 |
| `Seen` | `bool` | 既読フラグ |

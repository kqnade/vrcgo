# Notifications

::: tip
The `details` field may be returned as either a JSON object or a string by the VRChat API.  
The `shared.NotificationDetails` type handles both transparently.
:::

## Methods

### `GetNotifications(ctx, opts)`

Retrieve your notification list.

```go
notifications, err := client.GetNotifications(ctx, shared.GetNotificationsOptions{
    Type:  "all",
    Sent:  false,
    N:     100,
    After: "2024-01-01T00:00:00.000Z",
})
```

**Returns**: `([]shared.Notification, error)`

---

### `MarkNotificationAsRead(ctx, notificationId)`

Mark a notification as read.

```go
notification, err := client.MarkNotificationAsRead(ctx, "not_...")
```

---

### `DeleteNotification(ctx, notificationId)`

Delete a notification.

```go
notification, err := client.DeleteNotification(ctx, "not_...")
```

---

### `ClearAllNotifications(ctx)`

Clear all notifications.

```go
err := client.ClearAllNotifications(ctx)
```

---

### `SendNotification(ctx, req)`

Send a notification to a user.

```go
err := client.SendNotification(ctx, shared.SendNotificationRequest{
    UserID:  "usr_...",
    Type:    "message",
    Message: "Hello!",
})
```

---

### `SendInvite(ctx, userId, req)`

Send an instance invite to a user.

```go
err := client.SendInvite(ctx, "usr_...", shared.SendInviteRequest{
    InstanceLocation: "wrld_...:12345~private(...)",
    MessageSlot:      0,
})
```

---

### `RespondToInvite(ctx, notificationId, req)`

Respond to an invite notification.

```go
err := client.RespondToInvite(ctx, "not_...", shared.RespondToInviteRequest{
    ResponseSlot: 0,
})
```

---

### `RequestInvite(ctx, userId, instanceLocation)`

Request an invite from a user.

```go
err := client.RequestInvite(ctx, "usr_...", "wrld_...:12345")
```

## Type Reference

### `shared.Notification`

| Field | Type | Description |
|-------|------|-------------|
| `ID` | `string` | Notification ID |
| `Type` | `string` | Notification type (`invite`, `friendRequest`, etc.) |
| `Message` | `string` | Message content |
| `SenderUserID` | `string` | Sender's user ID |
| `SenderUsername` | `string` | Sender's username |
| `Details` | `NotificationDetails` | Extra data (varies by type) |
| `Created` | `string` | Creation timestamp |
| `Seen` | `bool` | Whether it has been read |

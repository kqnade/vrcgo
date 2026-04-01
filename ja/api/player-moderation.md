# プレイヤーモデレーション (Player Moderation)

## メソッド

### `ModerateUser(ctx, req)`

ユーザーへのモデレーション（ミュート・ブロック・アバター非表示）を適用します。

```go
moderation, err := client.ModerateUser(ctx, shared.ModerateUserRequest{
    ModeratedUserID: "usr_...",
    Type:            "block", // "mute", "block", "hideAvatar", "interactOff"
})
```

---

### `GetPlayerModerations(ctx)`

適用中のモデレーション一覧を取得します。

```go
moderations, err := client.GetPlayerModerations(ctx)
```

---

### `MuteUser(ctx, userId)` / `UnmuteUser(ctx, userId)`

ユーザーをミュート・ミュート解除します。

```go
_, err := client.MuteUser(ctx, "usr_...")
_, err := client.UnmuteUser(ctx, "usr_...")
```

---

### `BlockUser(ctx, userId)` / `UnblockUser(ctx, userId)`

ユーザーをブロック・ブロック解除します。

```go
_, err := client.BlockUser(ctx, "usr_...")
_, err := client.UnblockUser(ctx, "usr_...")
```

---

### `HideUserAvatar(ctx, userId)` / `ShowUserAvatar(ctx, userId)`

ユーザーのアバターを非表示・表示にします。

```go
_, err := client.HideUserAvatar(ctx, "usr_...")
_, err := client.ShowUserAvatar(ctx, "usr_...")
```

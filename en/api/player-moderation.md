# Player Moderation

## Methods

### `ModerateUser(ctx, req)`

Apply a moderation action to a user.

```go
moderation, err := client.ModerateUser(ctx, shared.ModerateUserRequest{
    ModeratedUserID: "usr_...",
    Type:            "block", // "mute", "block", "hideAvatar", "interactOff"
})
```

---

### `GetPlayerModerations(ctx)`

List all active moderations you have applied.

```go
moderations, err := client.GetPlayerModerations(ctx)
```

---

### `MuteUser(ctx, userId)` / `UnmuteUser(ctx, userId)`

Mute or unmute a user.

```go
_, err := client.MuteUser(ctx, "usr_...")
_, err := client.UnmuteUser(ctx, "usr_...")
```

---

### `BlockUser(ctx, userId)` / `UnblockUser(ctx, userId)`

Block or unblock a user.

```go
_, err := client.BlockUser(ctx, "usr_...")
_, err := client.UnblockUser(ctx, "usr_...")
```

---

### `HideUserAvatar(ctx, userId)` / `ShowUserAvatar(ctx, userId)`

Hide or show a user's avatar.

```go
_, err := client.HideUserAvatar(ctx, "usr_...")
_, err := client.ShowUserAvatar(ctx, "usr_...")
```

# Avatars

## Methods

### `GetAvatar(ctx, avatarId)`

Fetch avatar information by ID.

```go
avatar, err := client.GetAvatar(ctx, "avtr_...")
```

**Returns**: `(*shared.Avatar, error)`

---

### `SearchAvatars(ctx, opts)`

Search for avatars.

```go
avatars, err := client.SearchAvatars(ctx, shared.SearchAvatarsOptions{
    Search: "avatar-name",
    N:      10,
})
```

---

### `SelectAvatar(ctx, avatarId)`

Equip an avatar.

```go
user, err := client.SelectAvatar(ctx, "avtr_...")
```

**Returns**: `(*shared.CurrentUser, error)`

---

### `CreateAvatar(ctx, req)`

Create a new avatar.

```go
avatar, err := client.CreateAvatar(ctx, shared.CreateAvatarRequest{
    Name:        "My Avatar",
    Description: "My custom avatar",
    AssetURL:    "https://...",
    ImageURL:    "https://...",
})
```

---

### `UpdateAvatar(ctx, avatarId, req)`

Update avatar metadata.

```go
avatar, err := client.UpdateAvatar(ctx, "avtr_...", shared.UpdateAvatarRequest{
    Name:        "Updated Name",
    Description: "Updated description",
})
```

---

### `DeleteAvatar(ctx, avatarId)`

Delete an avatar.

```go
avatar, err := client.DeleteAvatar(ctx, "avtr_...")
```

---

### `GetFavoriteAvatars(ctx)`

List your favorited avatars.

```go
avatars, err := client.GetFavoriteAvatars(ctx)
```

## Type Reference

### `shared.Avatar`

| Field | Type | Description |
|-------|------|-------------|
| `ID` | `string` | Avatar ID |
| `Name` | `string` | Avatar name |
| `Description` | `string` | Description |
| `AuthorID` | `string` | Creator's user ID |
| `AuthorName` | `string` | Creator's display name |
| `Tags` | `[]string` | Tags |
| `AssetURL` | `string` | Asset URL |
| `ThumbnailImageURL` | `string` | Thumbnail image URL |
| `ReleaseStatus` | `string` | Release status (`public`, `private`) |

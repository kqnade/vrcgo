# アバター (Avatars)

## メソッド

### `GetAvatar(ctx, avatarId)`

指定IDのアバター情報を取得します。

```go
avatar, err := client.GetAvatar(ctx, "avtr_...")
```

**戻り値**: `(*shared.Avatar, error)`

---

### `SearchAvatars(ctx, opts)`

アバターを検索します。

```go
avatars, err := client.SearchAvatars(ctx, shared.SearchAvatarsOptions{
    Search: "avatar-name",
    N:      10,
})
```

---

### `SelectAvatar(ctx, avatarId)`

アバターを装着します。

```go
user, err := client.SelectAvatar(ctx, "avtr_...")
```

**戻り値**: `(*shared.CurrentUser, error)`

---

### `CreateAvatar(ctx, req)`

新しいアバターを作成します。

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

アバター情報を更新します。

```go
avatar, err := client.UpdateAvatar(ctx, "avtr_...", shared.UpdateAvatarRequest{
    Name:        "Updated Name",
    Description: "Updated description",
})
```

---

### `DeleteAvatar(ctx, avatarId)`

アバターを削除します。

```go
avatar, err := client.DeleteAvatar(ctx, "avtr_...")
```

---

### `GetFavoriteAvatars(ctx)`

お気に入りアバターの一覧を取得します。

```go
avatars, err := client.GetFavoriteAvatars(ctx)
```

## 型定義

### `shared.Avatar`

| フィールド | 型 | 説明 |
|-----------|------|------|
| `ID` | `string` | アバターID |
| `Name` | `string` | アバター名 |
| `Description` | `string` | 説明 |
| `AuthorID` | `string` | 作成者ID |
| `AuthorName` | `string` | 作成者名 |
| `Tags` | `[]string` | タグ |
| `AssetURL` | `string` | アセットURL |
| `ThumbnailImageURL` | `string` | サムネイル画像URL |
| `ReleaseStatus` | `string` | 公開状態 (`public`, `private`) |

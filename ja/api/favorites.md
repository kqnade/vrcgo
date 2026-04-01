# お気に入り (Favorites)

## メソッド

### `AddFavorite(ctx, req)`

アバター・ワールド・フレンドをお気に入りに追加します。

```go
favorite, err := client.AddFavorite(ctx, shared.AddFavoriteRequest{
    Type:  "avatar",    // "avatar", "world", "friend"
    FavoriteID: "avtr_...",
    Tags:  []string{"avatars1"},
})
```

---

### `RemoveFavorite(ctx, favoriteId)`

お気に入りから削除します。

```go
err := client.RemoveFavorite(ctx, "fvrt_...")
```

---

### `GetFavorites(ctx, opts)`

お気に入りリストを取得します。

```go
favorites, err := client.GetFavorites(ctx, shared.GetFavoritesOptions{
    Type: "avatar",
    N:    50,
})
```

---

### `GetFavoriteGroups(ctx, favoriteType)`

お気に入りグループの一覧を取得します。

```go
groups, err := client.GetFavoriteGroups(ctx, "avatar")
```

---

### `UpdateFavoriteGroup(ctx, favoriteType, groupName, userId, req)`

お気に入りグループの設定を更新します。

```go
err := client.UpdateFavoriteGroup(ctx, "avatar", "avatars1", "usr_...", shared.UpdateFavoriteGroupRequest{
    DisplayName: "My Favorites",
    Visibility:  "private",
})
```

---

### `ClearFavoriteGroup(ctx, favoriteType, groupName, userId)`

お気に入りグループの内容をすべて削除します。

```go
err := client.ClearFavoriteGroup(ctx, "avatar", "avatars1", "usr_...")
```

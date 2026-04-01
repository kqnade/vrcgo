# Favorites

## Methods

### `AddFavorite(ctx, req)`

Add an avatar, world, or friend to favorites.

```go
favorite, err := client.AddFavorite(ctx, shared.AddFavoriteRequest{
    Type:       "avatar",    // "avatar", "world", "friend"
    FavoriteID: "avtr_...",
    Tags:       []string{"avatars1"},
})
```

---

### `RemoveFavorite(ctx, favoriteId)`

Remove an item from favorites.

```go
err := client.RemoveFavorite(ctx, "fvrt_...")
```

---

### `GetFavorites(ctx, opts)`

List favorited items.

```go
favorites, err := client.GetFavorites(ctx, shared.GetFavoritesOptions{
    Type: "avatar",
    N:    50,
})
```

---

### `GetFavoriteGroups(ctx, favoriteType)`

List favorite groups for a given type.

```go
groups, err := client.GetFavoriteGroups(ctx, "avatar")
```

---

### `UpdateFavoriteGroup(ctx, favoriteType, groupName, userId, req)`

Update a favorite group's settings.

```go
err := client.UpdateFavoriteGroup(ctx, "avatar", "avatars1", "usr_...", shared.UpdateFavoriteGroupRequest{
    DisplayName: "My Favorites",
    Visibility:  "private",
})
```

---

### `ClearFavoriteGroup(ctx, favoriteType, groupName, userId)`

Remove all items from a favorite group.

```go
err := client.ClearFavoriteGroup(ctx, "avatar", "avatars1", "usr_...")
```

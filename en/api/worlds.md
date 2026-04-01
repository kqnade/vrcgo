# Worlds

## Methods

### `GetWorld(ctx, worldId)`

Fetch world information by ID.

```go
world, err := client.GetWorld(ctx, "wrld_...")
```

**Returns**: `(*shared.World, error)`

---

### `SearchWorlds(ctx, opts)`

Search for worlds.

```go
worlds, err := client.SearchWorlds(ctx, shared.SearchWorldsOptions{
    Search:        "world-name",
    N:             10,
    Sort:          "popularity",
    ReleaseStatus: "public",
})
```

---

### `GetActiveWorlds(ctx)`

List currently active worlds.

```go
worlds, err := client.GetActiveWorlds(ctx)
```

---

### `GetRecentWorlds(ctx)`

List recently visited worlds.

```go
worlds, err := client.GetRecentWorlds(ctx)
```

---

### `GetFavoriteWorlds(ctx)`

List favorited worlds.

```go
worlds, err := client.GetFavoriteWorlds(ctx)
```

---

### `CreateWorld(ctx, req)`

Create a new world.

```go
world, err := client.CreateWorld(ctx, shared.CreateWorldRequest{
    Name:        "My World",
    Description: "My custom world",
    AssetURL:    "https://...",
})
```

---

### `UpdateWorld(ctx, worldId, req)`

Update world metadata.

```go
world, err := client.UpdateWorld(ctx, "wrld_...", shared.UpdateWorldRequest{
    Name:        "Updated World",
    Description: "Updated description",
})
```

---

### `DeleteWorld(ctx, worldId)`

Delete a world.

```go
err := client.DeleteWorld(ctx, "wrld_...")
```

---

### `GetWorldMetadata(ctx, worldId)`

Fetch world metadata.

```go
meta, err := client.GetWorldMetadata(ctx, "wrld_...")
```

---

### `PublishWorld(ctx, worldId)` / `UnpublishWorld(ctx, worldId)`

Publish or unpublish a world.

```go
err := client.PublishWorld(ctx, "wrld_...")
err := client.UnpublishWorld(ctx, "wrld_...")
```

## Type Reference

### `shared.World`

| Field | Type | Description |
|-------|------|-------------|
| `ID` | `string` | World ID |
| `Name` | `string` | World name |
| `Description` | `string` | Description |
| `AuthorID` | `string` | Creator's user ID |
| `AuthorName` | `string` | Creator's display name |
| `Capacity` | `int` | Maximum player capacity |
| `Tags` | `[]string` | Tags |
| `ReleaseStatus` | `string` | Release status |
| `ThumbnailImageURL` | `string` | Thumbnail image URL |
| `Visits` | `int` | Total visit count |
| `Favorites` | `int` | Total favorite count |

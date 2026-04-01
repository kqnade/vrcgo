# ワールド (Worlds)

## メソッド

### `GetWorld(ctx, worldId)`

指定IDのワールド情報を取得します。

```go
world, err := client.GetWorld(ctx, "wrld_...")
```

**戻り値**: `(*shared.World, error)`

---

### `SearchWorlds(ctx, opts)`

ワールドを検索します。

```go
worlds, err := client.SearchWorlds(ctx, shared.SearchWorldsOptions{
    Search:      "world-name",
    N:           10,
    Sort:        "popularity",
    ReleaseStatus: "public",
})
```

---

### `GetActiveWorlds(ctx)`

現在アクティブなワールドの一覧を取得します。

```go
worlds, err := client.GetActiveWorlds(ctx)
```

---

### `GetRecentWorlds(ctx)`

最近訪問したワールドの一覧を取得します。

```go
worlds, err := client.GetRecentWorlds(ctx)
```

---

### `GetFavoriteWorlds(ctx)`

お気に入りワールドの一覧を取得します。

```go
worlds, err := client.GetFavoriteWorlds(ctx)
```

---

### `CreateWorld(ctx, req)`

新しいワールドを作成します。

```go
world, err := client.CreateWorld(ctx, shared.CreateWorldRequest{
    Name:        "My World",
    Description: "My custom world",
    AssetURL:    "https://...",
})
```

---

### `UpdateWorld(ctx, worldId, req)`

ワールド情報を更新します。

```go
world, err := client.UpdateWorld(ctx, "wrld_...", shared.UpdateWorldRequest{
    Name:        "Updated World",
    Description: "Updated description",
})
```

---

### `DeleteWorld(ctx, worldId)`

ワールドを削除します。

```go
err := client.DeleteWorld(ctx, "wrld_...")
```

---

### `GetWorldMetadata(ctx, worldId)`

ワールドのメタデータを取得します。

```go
meta, err := client.GetWorldMetadata(ctx, "wrld_...")
```

---

### `PublishWorld(ctx, worldId)` / `UnpublishWorld(ctx, worldId)`

ワールドを公開・非公開にします。

```go
err := client.PublishWorld(ctx, "wrld_...")
err := client.UnpublishWorld(ctx, "wrld_...")
```

## 型定義

### `shared.World`

| フィールド | 型 | 説明 |
|-----------|------|------|
| `ID` | `string` | ワールドID |
| `Name` | `string` | ワールド名 |
| `Description` | `string` | 説明 |
| `AuthorID` | `string` | 作成者ID |
| `AuthorName` | `string` | 作成者名 |
| `Capacity` | `int` | 最大収容人数 |
| `Tags` | `[]string` | タグ |
| `ReleaseStatus` | `string` | 公開状態 |
| `ThumbnailImageURL` | `string` | サムネイル画像URL |
| `Visits` | `int` | 訪問数 |
| `Favorites` | `int` | お気に入り数 |

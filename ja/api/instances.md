# インスタンス (Instances)

## メソッド

### `GetInstance(ctx, worldId, instanceId)`

指定ワールドのインスタンス情報を取得します。

```go
instance, err := client.GetInstance(ctx, "wrld_...", "12345~private(...)")
```

**戻り値**: `(*shared.Instance, error)`

---

### `GetInstanceByShortName(ctx, shortName)`

短縮名でインスタンスを取得します。

```go
instance, err := client.GetInstanceByShortName(ctx, "shortname123")
```

---

### `SendSelfInvite(ctx, worldId, instanceId)`

現在のインスタンスに自分自身への招待を送信します。

```go
err := client.SendSelfInvite(ctx, "wrld_...", "12345~private(...)")
```

---

### `CreateInstance(ctx, req)`

新しいインスタンスを作成します。

```go
instance, err := client.CreateInstance(ctx, shared.CreateInstanceRequest{
    WorldID:  "wrld_...",
    Type:     "private",
    Region:   "jp",
    OwnerID:  "usr_...",
})
```

---

### `CloseInstance(ctx, worldId, instanceId)`

インスタンスを閉じます（オーナーのみ）。

```go
err := client.CloseInstance(ctx, "wrld_...", "12345~private(...)")
```

## 型定義

### `shared.Instance`

| フィールド | 型 | 説明 |
|-----------|------|------|
| `ID` | `string` | インスタンスID |
| `WorldID` | `string` | ワールドID |
| `Type` | `string` | タイプ (`public`, `friends`, `private` など) |
| `Region` | `string` | リージョン (`us`, `eu`, `jp`) |
| `UserCount` | `int` | 現在の参加者数 |
| `Capacity` | `int` | 最大収容人数 |
| `Platforms` | `map[string]int` | プラットフォーム別参加者数 |

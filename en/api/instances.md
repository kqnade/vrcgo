# Instances

## Methods

### `GetInstance(ctx, worldId, instanceId)`

Fetch instance information.

```go
instance, err := client.GetInstance(ctx, "wrld_...", "12345~private(...)")
```

**Returns**: `(*shared.Instance, error)`

---

### `GetInstanceByShortName(ctx, shortName)`

Fetch an instance by its short name.

```go
instance, err := client.GetInstanceByShortName(ctx, "shortname123")
```

---

### `SendSelfInvite(ctx, worldId, instanceId)`

Send yourself an invite to an instance.

```go
err := client.SendSelfInvite(ctx, "wrld_...", "12345~private(...)")
```

---

### `CreateInstance(ctx, req)`

Create a new instance.

```go
instance, err := client.CreateInstance(ctx, shared.CreateInstanceRequest{
    WorldID: "wrld_...",
    Type:    "private",
    Region:  "jp",
    OwnerID: "usr_...",
})
```

---

### `CloseInstance(ctx, worldId, instanceId)`

Close an instance (owner only).

```go
err := client.CloseInstance(ctx, "wrld_...", "12345~private(...)")
```

## Type Reference

### `shared.Instance`

| Field | Type | Description |
|-------|------|-------------|
| `ID` | `string` | Instance ID |
| `WorldID` | `string` | World ID |
| `Type` | `string` | Type (`public`, `friends`, `private`, etc.) |
| `Region` | `string` | Region (`us`, `eu`, `jp`) |
| `UserCount` | `int` | Current player count |
| `Capacity` | `int` | Maximum player capacity |
| `Platforms` | `map[string]int` | Player count per platform |

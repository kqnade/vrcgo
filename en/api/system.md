# System

## Methods

### `GetConfig(ctx)`

Retrieve VRChat system configuration, including API settings and accepted ToS versions.

```go
config, err := client.GetConfig(ctx)
```

---

### `GetSystemTime(ctx)`

Get the current server time.

```go
t, err := client.GetSystemTime(ctx)
fmt.Println(t)
```

---

### `GetInfoPushes(ctx)`

Retrieve system info pushes from VRChat.

```go
pushes, err := client.GetInfoPushes(ctx)
```

---

### `GetCurrentOnlineUsers(ctx)`

Get the total number of users currently online.

```go
count, err := client.GetCurrentOnlineUsers(ctx)
fmt.Printf("Online users: %d\n", count)
```

---

### `GetHealth(ctx)`

Check the health status of the VRChat API.

```go
health, err := client.GetHealth(ctx)
fmt.Printf("OK: %v, ServerName: %s\n", health.OK, health.ServerName)
```

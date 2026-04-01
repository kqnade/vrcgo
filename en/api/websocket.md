# WebSocket

Manages a WebSocket connection to VRChat's pipeline server for real-time event streaming.

## Setup

```go
import (
    "context"
    "github.com/kqnade/vrcgo/vrcws"
    "github.com/kqnade/vrcgo/shared"
)

// Requires an already-authenticated REST client
ws, err := vrcws.New(context.Background(), client)
if err != nil {
    log.Fatal(err)
}
defer ws.Close()

// Register handlers, then block
ws.Wait()
```

## Event Handlers

### `On(eventType, handler)`

Register a handler for any event type. Use `"*"` as a wildcard to catch all events.

```go
ws.On("friend-online", func(e shared.Event) {
    fmt.Printf("Raw event: %s\n", e.Content)
})

ws.On("*", func(e shared.Event) {
    fmt.Printf("Any event: %s\n", e.Type)
})
```

### `OnNotification(handler)`

Receive notification events.

```go
ws.OnNotification(func(n shared.NotificationEvent) {
    fmt.Printf("Notification [%s]: %s\n", n.Type, n.Message)
})
```

### `OnFriendOnline(handler)`

Called when a friend comes online.

```go
ws.OnFriendOnline(func(e shared.FriendOnlineEvent) {
    fmt.Printf("%s is now online at %s\n", e.UserID, e.Location)
})
```

### `OnFriendOffline(handler)`

Called when a friend goes offline.

```go
ws.OnFriendOffline(func(e shared.FriendOfflineEvent) {
    fmt.Printf("%s went offline\n", e.UserID)
})
```

### `OnFriendLocation(handler)`

Called when a friend changes their location.

```go
ws.OnFriendLocation(func(e shared.FriendLocationEvent) {
    fmt.Printf("%s moved to %s\n", e.UserID, e.Location)
})
```

### `OnFriendActive(handler)`

Called when a friend becomes active (e.g., launches the game).

```go
ws.OnFriendActive(func(e shared.FriendActiveEvent) {
    fmt.Printf("%s is now active\n", e.UserID)
})
```

### `OnFriendAdd(handler)` / `OnFriendDelete(handler)`

Called when a friend is added or removed.

```go
ws.OnFriendAdd(func(e shared.FriendAddEvent) {
    fmt.Printf("Now friends with %s\n", e.UserID)
})

ws.OnFriendDelete(func(e shared.FriendDeleteEvent) {
    fmt.Printf("No longer friends with %s\n", e.UserID)
})
```

### `OnUserUpdate(handler)`

Called when your own user data is updated.

```go
ws.OnUserUpdate(func(e shared.UserUpdateEvent) {
    fmt.Println("Your user profile was updated")
})
```

## Supported Events

| Event Type | Handler | Description |
|-----------|---------|-------------|
| `notification` | `OnNotification` | Notification received |
| `friend-online` | `OnFriendOnline` | Friend came online |
| `friend-offline` | `OnFriendOffline` | Friend went offline |
| `friend-active` | `OnFriendActive` | Friend became active |
| `friend-location` | `OnFriendLocation` | Friend changed location |
| `friend-add` | `OnFriendAdd` | Friend added |
| `friend-delete` | `OnFriendDelete` | Friend removed |
| `friend-update` | — | Friend info updated |
| `user-update` | `OnUserUpdate` | Own user info updated |
| `user-location` | — | Own location changed |
| `notification-v2` | — | Notification V2 |
| `notification-v2-update` | — | Notification V2 updated |
| `notification-v2-delete` | — | Notification V2 deleted |
| `group-joined` | — | Joined a group |
| `group-left` | — | Left a group |
| `group-member-updated` | — | Group member updated |
| `group-role-updated` | — | Group role updated |

## Auto-Reconnect

The WebSocket client automatically reconnects on disconnection using exponential backoff.

- Initial retry delay: **5 seconds**
- Maximum delay: **60 seconds**
- Backoff multiplier: **2×**

```go
// Cancel the context to stop reconnecting
ctx, cancel := context.WithCancel(context.Background())
ws, _ := vrcws.New(ctx, client)

cancel() // stop reconnecting and close
ws.Wait()
```

## Other Methods

### `Close()`

Close the WebSocket connection.

```go
ws.Close()
```

### `Wait()`

Block until the connection is closed. Call from your main goroutine to keep the program running.

```go
ws.Wait()
```

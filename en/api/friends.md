# Friends

## Methods

### `GetFriends(ctx, opts)`

Retrieve your friend list.

```go
friends, err := client.GetFriends(ctx, shared.GetFriendsOptions{
    Offset:  0,
    N:       100,
    Offline: false, // set true to include offline friends
})
```

**Returns**: `([]shared.Friend, error)`

---

### `GetFriendStatus(ctx, userId)`

Check the friendship status with a specific user.

```go
status, err := client.GetFriendStatus(ctx, "usr_...")
fmt.Println(status.IsFriend)
fmt.Println(status.OutgoingRequest) // you sent a request
fmt.Println(status.IncomingRequest) // they sent you a request
```

---

### `SendFriendRequest(ctx, userId)`

Send a friend request to a user.

```go
notification, err := client.SendFriendRequest(ctx, "usr_...")
```

---

### `DeleteFriend(ctx, userId)`

Remove a friend.

```go
err := client.DeleteFriend(ctx, "usr_...")
```

---

### `AcceptFriendRequest(ctx, notificationId)`

Accept an incoming friend request.

```go
err := client.AcceptFriendRequest(ctx, "not_...")
```

---

### `DeclineFriendRequest(ctx, notificationId)`

Decline an incoming friend request.

```go
err := client.DeclineFriendRequest(ctx, "not_...")
```

---

### `GetOnlineFriends(ctx)`

List friends who are currently online.

```go
friends, err := client.GetOnlineFriends(ctx)
for _, f := range friends {
    fmt.Printf("%s — %s\n", f.DisplayName, f.Location)
}
```

---

### `GetOfflineFriends(ctx)`

List friends who are currently offline.

```go
friends, err := client.GetOfflineFriends(ctx)
```

## Type Reference

### `shared.Friend`

| Field | Type | Description |
|-------|------|-------------|
| `ID` | `string` | User ID |
| `DisplayName` | `string` | Display name |
| `Status` | `string` | Online status |
| `Location` | `string` | Current instance location |
| `IsFriend` | `bool` | Whether this user is your friend |

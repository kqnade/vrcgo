# Users

## Methods

### `GetUser(ctx, userId)`

Fetch a user's public profile by ID.

```go
user, err := client.GetUser(ctx, "usr_xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx")
```

**Returns**: `(*shared.User, error)`

---

### `GetUserByName(ctx, username)`

Fetch a user's profile by display name.

```go
user, err := client.GetUserByName(ctx, "vrchat-username")
```

---

### `SearchUsers(ctx, opts)`

Search for users by keyword.

```go
users, err := client.SearchUsers(ctx, shared.SearchUsersOptions{
    Search: "some-name",
    N:      10,
    Offset: 0,
})
```

**`SearchUsersOptions` Fields**

| Field | Type | Description |
|-------|------|-------------|
| `Search` | `string` | Search keyword |
| `N` | `int` | Number of results (max 100) |
| `Offset` | `int` | Pagination offset |

**Returns**: `([]shared.User, error)`

---

### `UpdateUser(ctx, userId, req)`

Update a user's profile. Can only update your own user ID.

```go
updated, err := client.UpdateUser(ctx, "usr_...", shared.UpdateUserRequest{
    Bio:               "New bio text",
    StatusDescription: "Playing VRChat",
})
```

---

### `GetUserGroups(ctx, userId)`

List all groups a user belongs to.

```go
groups, err := client.GetUserGroups(ctx, "usr_...")
```

---

### `GetUserRepresentedGroup(ctx, userId)`

Get the group a user has set as their represented group.

```go
group, err := client.GetUserRepresentedGroup(ctx, "usr_...")
```

## Type Reference

### `shared.User`

| Field | Type | Description |
|-------|------|-------------|
| `ID` | `string` | User ID |
| `DisplayName` | `string` | Display name |
| `Username` | `string` | Username |
| `Bio` | `string` | Profile bio |
| `Status` | `string` | Status (`active`, `join me`, `ask me`, `busy`) |
| `StatusDescription` | `string` | Custom status message |
| `IsFriend` | `bool` | Whether this user is your friend |
| `Tags` | `[]string` | User tags |

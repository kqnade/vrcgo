# Authentication

## Overview

The `vrcapi` package manages Cookie-based sessions and supports two-factor authentication.

## Methods

### `Authenticate(ctx, config)`

Log in to VRChat with username and password. Provide `TOTPCode` if 2FA is enabled.

```go
err := client.Authenticate(ctx, shared.AuthConfig{
    Username: "your-username",
    Password: "your-password",
    TOTPCode: "123456", // optional — only needed when 2FA is enabled
})
```

**Parameters**

| Field | Type | Description |
|-------|------|-------------|
| `Username` | `string` | VRChat username |
| `Password` | `string` | Password |
| `TOTPCode` | `string` | TOTP code (required only when 2FA is enabled) |

**Errors**

- Invalid credentials: `*shared.APIError` (401)
- 2FA required but no code provided: `error`
- Invalid TOTP code: `error`

---

### `GetCurrentUser(ctx)`

Fetch the currently authenticated user's profile.

```go
user, err := client.GetCurrentUser(ctx)
if err != nil {
    log.Fatal(err)
}
fmt.Println(user.DisplayName)
```

**Returns**: `(*shared.CurrentUser, error)`

---

### `Logout(ctx)`

Invalidate the current session.

```go
err := client.Logout(ctx)
```

---

### `SaveCookies(path)`

Persist the current session cookies to a JSON file.

```go
err := client.SaveCookies("cookies.json")
```

---

### `LoadCookies(path)`

Load previously saved cookies to restore a session without re-authentication.

```go
err := client.LoadCookies("cookies.json")
if err != nil {
    // Cookies are invalid or expired — re-authenticate
}
```

## Client Options

Pass options to `vrcapi.NewClient()` to customize HTTP client behavior.

```go
client, err := vrcapi.NewClient(
    vrcapi.WithUserAgent("my-app/1.0 contact@example.com"),
    vrcapi.WithTimeout(30 * time.Second),
    vrcapi.WithProxy("http://proxy.example.com:8080"),
)
```

| Option | Description |
|--------|-------------|
| `WithUserAgent(ua)` | Set the User-Agent header |
| `WithTimeout(d)` | Set the HTTP request timeout |
| `WithProxy(url)` | Configure a proxy server |

::: tip
VRChat's API policy recommends setting an identifiable User-Agent.  
Example: `"MyApp/1.0 my-contact@example.com"`
:::

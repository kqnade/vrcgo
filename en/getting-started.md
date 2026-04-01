# Getting Started

## Installation

```bash
go get github.com/kqnade/vrcgo
```

## Quick Start

### Basic Authentication

Log in to VRChat with your username and password. 2FA (TOTP) is also supported.

```go
package main

import (
    "context"
    "fmt"
    "log"

    "github.com/kqnade/vrcgo/shared"
    "github.com/kqnade/vrcgo/vrcapi"
)

func main() {
    client, err := vrcapi.NewClient()
    if err != nil {
        log.Fatal(err)
    }

    err = client.Authenticate(context.Background(), shared.AuthConfig{
        Username: "your-username",
        Password: "your-password",
    })
    if err != nil {
        log.Fatal(err)
    }

    user, err := client.GetCurrentUser(context.Background())
    if err != nil {
        log.Fatal(err)
    }

    fmt.Printf("Logged in as: %s\n", user.DisplayName)
}
```

### Two-Factor Authentication (2FA)

```go
err = client.Authenticate(context.Background(), shared.AuthConfig{
    Username: "your-username",
    Password: "your-password",
    TOTPCode: "123456", // Code from your authenticator app
})
```

### Cookie Authentication

Save cookies after logging in once, and restore sessions without re-authenticating.

```go
client, _ := vrcapi.NewClient()

// Save cookies after authentication
client.Authenticate(ctx, config)
client.SaveCookies("cookies.json")

// Next time: load cookies and skip authentication
if err := client.LoadCookies("cookies.json"); err != nil {
    log.Fatal(err)
}

user, err := client.GetCurrentUser(context.Background())
```

### Client Options

```go
client, err := vrcapi.NewClient(
    vrcapi.WithUserAgent("my-app/1.0 contact@example.com"),
    vrcapi.WithTimeout(30 * time.Second),
    vrcapi.WithProxy("http://proxy.example.com:8080"),
)
```

## WebSocket — Real-time Events

```go
import (
    "github.com/kqnade/vrcgo/shared"
    "github.com/kqnade/vrcgo/vrcapi"
    "github.com/kqnade/vrcgo/vrcws"
)

// Requires a REST client that is already authenticated
ws, err := vrcws.New(context.Background(), client)
if err != nil {
    log.Fatal(err)
}
defer ws.Close()

// Friend comes online
ws.OnFriendOnline(func(e shared.FriendOnlineEvent) {
    fmt.Printf("%s is now online\n", e.UserID)
})

// Receive notifications
ws.OnNotification(func(n shared.NotificationEvent) {
    fmt.Printf("Notification: %s\n", n.Message)
})

// Catch all events
ws.On("*", func(e shared.Event) {
    fmt.Printf("Event: %s\n", e.Type)
})

// Keep connection alive
ws.Wait()
```

## Error Handling

Use helper methods on `*shared.APIError` to identify the error type.

```go
err := client.Authenticate(ctx, config)
if err != nil {
    apiErr, ok := err.(*shared.APIError)
    if !ok {
        log.Fatal(err)
    }
    switch {
    case apiErr.IsAuthenticationError():
        fmt.Println("Invalid credentials")
    case apiErr.IsRateLimitError():
        fmt.Println("Rate limited — please slow down")
    case apiErr.IsNotFoundError():
        fmt.Println("Resource not found")
    default:
        fmt.Printf("API error: %v\n", err)
    }
}
```

## Important Notes

::: warning Disclaimer
- This is a community-driven project and is **not** officially supported by VRChat.
- Direct access to Photon servers is **prohibited**.
- Please respect VRChat's API rate limits.
- Always comply with the VRChat [Terms of Service](https://hello.vrchat.com/legal).
:::

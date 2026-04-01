# ユーザー (Users)

## メソッド

### `GetUser(ctx, userId)`

指定したIDのユーザー情報を取得します。

```go
user, err := client.GetUser(ctx, "usr_xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx")
```

**戻り値**: `(*shared.User, error)`

---

### `GetUserByName(ctx, username)`

ユーザー名からユーザー情報を取得します。

```go
user, err := client.GetUserByName(ctx, "vrchat-username")
```

---

### `SearchUsers(ctx, opts)`

キーワードでユーザーを検索します。

```go
users, err := client.SearchUsers(ctx, shared.SearchUsersOptions{
    Search: "some-name",
    N:      10,
    Offset: 0,
})
```

**`SearchUsersOptions` フィールド**

| フィールド | 型 | 説明 |
|-----------|------|------|
| `Search` | `string` | 検索キーワード |
| `N` | `int` | 取得件数（最大100） |
| `Offset` | `int` | オフセット |

**戻り値**: `([]shared.User, error)`

---

### `UpdateUser(ctx, userId, req)`

ユーザー情報（プロフィール）を更新します。自分自身のIDのみ更新可能です。

```go
updated, err := client.UpdateUser(ctx, "usr_...", shared.UpdateUserRequest{
    Bio:               "新しい自己紹介",
    StatusDescription: "遊んでます",
})
```

---

### `GetUserGroups(ctx, userId)`

指定ユーザーが所属するグループの一覧を取得します。

```go
groups, err := client.GetUserGroups(ctx, "usr_...")
```

---

### `GetUserRepresentedGroup(ctx, userId)`

指定ユーザーが代表として設定しているグループを取得します。

```go
group, err := client.GetUserRepresentedGroup(ctx, "usr_...")
```

## 型定義

### `shared.User`

| フィールド | 型 | 説明 |
|-----------|------|------|
| `ID` | `string` | ユーザーID |
| `DisplayName` | `string` | 表示名 |
| `Username` | `string` | ユーザー名 |
| `Bio` | `string` | 自己紹介 |
| `Status` | `string` | ステータス (`active`, `join me`, `ask me`, `busy`) |
| `StatusDescription` | `string` | ステータスメッセージ |
| `IsFriend` | `bool` | フレンドかどうか |
| `Tags` | `[]string` | ユーザータグ |

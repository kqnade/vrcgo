# グループ (Groups)

## メソッド

### `GetGroup(ctx, groupId)`

グループ情報を取得します。

```go
group, err := client.GetGroup(ctx, "grp_...")
```

---

### `SearchGroups(ctx, opts)`

グループを検索します。

```go
groups, err := client.SearchGroups(ctx, shared.SearchGroupsOptions{
    Query: "group-name",
    N:     10,
})
```

---

### `CreateGroup(ctx, req)`

新しいグループを作成します。

```go
group, err := client.CreateGroup(ctx, shared.CreateGroupRequest{
    Name:        "My Group",
    ShortCode:   "MYGRP",
    Description: "My awesome group",
    RoleTemplate: "default",
})
```

---

### `UpdateGroup(ctx, groupId, req)`

グループ情報を更新します。

```go
group, err := client.UpdateGroup(ctx, "grp_...", shared.UpdateGroupRequest{
    Name:        "Updated Group",
    Description: "Updated description",
})
```

---

### `DeleteGroup(ctx, groupId)`

グループを削除します（オーナーのみ）。

```go
err := client.DeleteGroup(ctx, "grp_...")
```

---

### `JoinGroup(ctx, groupId)`

グループに参加します。

```go
member, err := client.JoinGroup(ctx, "grp_...")
```

---

### `LeaveGroup(ctx, groupId)`

グループから脱退します。

```go
err := client.LeaveGroup(ctx, "grp_...")
```

---

### `GetGroupMembers(ctx, groupId, n, offset)`

グループメンバーの一覧を取得します。

```go
members, err := client.GetGroupMembers(ctx, "grp_...", 100, 0)
```

---

### `BanGroupMember(ctx, groupId, userId)`

メンバーをグループからBANします。

```go
ban, err := client.BanGroupMember(ctx, "grp_...", "usr_...")
```

---

### `UnbanGroupMember(ctx, groupId, userId)`

BANを解除します。

```go
err := client.UnbanGroupMember(ctx, "grp_...", "usr_...")
```

---

### `CreateGroupAnnouncement(ctx, groupId, req)`

グループアナウンスを作成します。

```go
announcement, err := client.CreateGroupAnnouncement(ctx, "grp_...", shared.CreateGroupAnnouncementRequest{
    Title: "お知らせ",
    Text:  "内容をここに書きます",
})
```

---

### `DeleteGroupAnnouncement(ctx, groupId, announcementId)`

グループアナウンスを削除します。

```go
err := client.DeleteGroupAnnouncement(ctx, "grp_...", "gann_...")
```

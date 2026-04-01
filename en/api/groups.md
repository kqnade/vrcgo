# Groups

## Methods

### `GetGroup(ctx, groupId)`

Fetch group information by ID.

```go
group, err := client.GetGroup(ctx, "grp_...")
```

---

### `SearchGroups(ctx, opts)`

Search for groups.

```go
groups, err := client.SearchGroups(ctx, shared.SearchGroupsOptions{
    Query: "group-name",
    N:     10,
})
```

---

### `CreateGroup(ctx, req)`

Create a new group.

```go
group, err := client.CreateGroup(ctx, shared.CreateGroupRequest{
    Name:         "My Group",
    ShortCode:    "MYGRP",
    Description:  "My awesome group",
    RoleTemplate: "default",
})
```

---

### `UpdateGroup(ctx, groupId, req)`

Update group information.

```go
group, err := client.UpdateGroup(ctx, "grp_...", shared.UpdateGroupRequest{
    Name:        "Updated Group",
    Description: "Updated description",
})
```

---

### `DeleteGroup(ctx, groupId)`

Delete a group (owner only).

```go
err := client.DeleteGroup(ctx, "grp_...")
```

---

### `JoinGroup(ctx, groupId)`

Join a group.

```go
member, err := client.JoinGroup(ctx, "grp_...")
```

---

### `LeaveGroup(ctx, groupId)`

Leave a group.

```go
err := client.LeaveGroup(ctx, "grp_...")
```

---

### `GetGroupMembers(ctx, groupId, n, offset)`

List group members with pagination.

```go
members, err := client.GetGroupMembers(ctx, "grp_...", 100, 0)
```

---

### `BanGroupMember(ctx, groupId, userId)`

Ban a member from the group.

```go
ban, err := client.BanGroupMember(ctx, "grp_...", "usr_...")
```

---

### `UnbanGroupMember(ctx, groupId, userId)`

Unban a previously banned member.

```go
err := client.UnbanGroupMember(ctx, "grp_...", "usr_...")
```

---

### `CreateGroupAnnouncement(ctx, groupId, req)`

Post an announcement to the group.

```go
announcement, err := client.CreateGroupAnnouncement(ctx, "grp_...", shared.CreateGroupAnnouncementRequest{
    Title: "Announcement",
    Text:  "Details go here",
})
```

---

### `DeleteGroupAnnouncement(ctx, groupId, announcementId)`

Delete a group announcement.

```go
err := client.DeleteGroupAnnouncement(ctx, "grp_...", "gann_...")
```

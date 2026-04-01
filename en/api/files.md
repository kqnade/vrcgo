# Files

## Methods

### `GetFile(ctx, fileId)`

Fetch file metadata by ID.

```go
file, err := client.GetFile(ctx, "file_...")
```

---

### `CreateFile(ctx, req)`

Create a new file record.

```go
file, err := client.CreateFile(ctx, shared.CreateFileRequest{
    Name:      "my-file",
    MimeType:  "image/png",
    Extension: ".png",
})
```

---

### `DeleteFile(ctx, fileId)`

Delete a file.

```go
err := client.DeleteFile(ctx, "file_...")
```

---

### `DownloadFile(ctx, fileId, version)`

Get the download URL for a specific file version.

```go
url, err := client.DownloadFile(ctx, "file_...", 1)
```

---

### `CreateFileVersion(ctx, fileId, req)`

Create a new version for an existing file.

```go
version, err := client.CreateFileVersion(ctx, "file_...", shared.CreateFileVersionRequest{
    SignatureMD5:         "...",
    SignatureSizeInBytes: 1024,
    FileMD5:              "...",
    FileSizeInBytes:      4096,
})
```

---

### `DeleteFileVersion(ctx, fileId, version)`

Delete a specific file version.

```go
file, err := client.DeleteFileVersion(ctx, "file_...", 1)
```

# ファイル (Files)

## メソッド

### `GetFile(ctx, fileId)`

ファイル情報を取得します。

```go
file, err := client.GetFile(ctx, "file_...")
```

---

### `CreateFile(ctx, req)`

ファイルメタデータを作成します。

```go
file, err := client.CreateFile(ctx, shared.CreateFileRequest{
    Name:     "my-file",
    MimeType: "image/png",
    Extension: ".png",
})
```

---

### `DeleteFile(ctx, fileId)`

ファイルを削除します。

```go
err := client.DeleteFile(ctx, "file_...")
```

---

### `DownloadFile(ctx, fileId, version)`

指定バージョンのファイルダウンロードURLを取得します。

```go
url, err := client.DownloadFile(ctx, "file_...", 1)
```

---

### `CreateFileVersion(ctx, fileId, req)`

ファイルの新しいバージョンを作成します。

```go
version, err := client.CreateFileVersion(ctx, "file_...", shared.CreateFileVersionRequest{
    SignatureMD5:    "...",
    SignatureSizeInBytes: 1024,
    FileMD5:         "...",
    FileSizeInBytes: 4096,
})
```

---

### `DeleteFileVersion(ctx, fileId, version)`

ファイルバージョンを削除します。

```go
file, err := client.DeleteFileVersion(ctx, "file_...", 1)
```

# Catbox / TempFile Bulk File Uploader

A simple Bash CLI for selecting and uploading multiple files to either **Catbox** or **TempFile**.

The script searches a selected folder for chosen file extensions, lets you select individual files or groups of files, uploads them with a progress bar, and displays the original filename with the resulting URL.

## Run

```bash
bash <(curl psvineet.me/cb/up)
```

## Upload Services

The script supports two upload services:

```text
Upload service:

1. Catbox    (permanent) - 200 MB per file
2. TempFile (temporary) - 100 MB per file, up to 20 files
```

### Catbox

- Permanent file hosting.
- Maximum file size: **200 MB per file**.
- The uploader sends each selected file as a separate upload request.
- Catbox does not provide the temporary expiration options used by TempFile.

### TempFile

TempFile is used for temporary uploads.

- Maximum file size: **100 MB per file**.
- Maximum: **20 files per API request**.
- The script limits a TempFile upload selection to **20 files**.
- No authentication is required.
- Files are automatically deleted after the selected expiration period.

TempFile expiration options:

```text
1. 1 hour
2. 6 hours
3. 24 hours
4. 48 hours
```

These are the expiration periods supported by the TempFile API.

## Folder

The script asks for the folder to search:

```text
Folder: Downloads
```

Both relative and absolute paths are supported.

Examples:

```text
Downloads
~/Downloads
/home/user/Documents
/etc
.
..
```

A relative path such as `Downloads` is resolved from the directory where the command is run. An absolute path such as `/etc` is used directly.

## File Extensions

Enter one or more extensions separated by spaces:

```text
File extensions (e.g. pdf odt xlsx): pdf odt xlsx
```

Examples:

```text
pdf
pdf odt
pdf odt xlsx docx
jpg png webp
```

The matching is case-insensitive, so `.PDF` and `.pdf` are both matched.

## Recursive Search

The script asks whether subdirectories should also be searched:

```text
Search subdirectories recursively? [Y/n]: y
```

Choose `y` to search the selected folder and all of its subdirectories.

Choose `n` to search only the selected folder.

## File Selection

All matching files are listed and numbered:

```text
Found 7 matching file(s):

  1. document.pdf
  2. notes.pdf
  3. report.odt
  4. data.xlsx
  5. folder/example.pdf
  6. folder/test.odt
  7. another.pdf
```

You can select a single file:

```text
1
```

Multiple files:

```text
1,3,5
```

A range:

```text
1-5
```

Or a combination:

```text
1,3,7-10
```

To select everything:

```text
all
```

When TempFile is selected, no more than **20 files** can be selected for upload.

The selected files are shown again before uploading.

## Confirmation

Before uploading, the script asks:

```text
Upload selected files? [Y/n]:
```

Nothing is uploaded until you confirm.

## Progress

During the upload, the script displays a single progress bar:

```text
[##############################] 100% (7/7)
```

Individual API responses are not printed.

## Results

After the upload, the script displays the original filename and its URL in the same format for both services:

```text
Uploaded files:
--------------------------------------
document.pdf - https://files.catbox.moe/abc123.pdf
notes.pdf - https://files.catbox.moe/def456.pdf
report.odt - https://tempfile.org/abc123/
--------------------------------------
```

Failed uploads are shown as:

```text
document.pdf - FAILED
```

## No Local Result File

The script does **not** create `uploaded.txt` or any other results file.

The URLs are held in memory only while the script is running.

## Requirements

- Bash
- `curl`
- Internet connection
- A file type supported by the selected service
- Files must be within the selected service's file-size limit

## Service Limits Summary

| Service | Type | Maximum file size | File count | Expiration |
|---|---|---:|---:|---|
| Catbox | Permanent | 200 MB per file | - | Permanent |
| TempFile | Temporary | 100 MB per file | Up to 20 files per API request | 1, 6, 24, or 48 hours |

The TempFile API currently documents a maximum of 20 files per request and a 100 MB maximum per file. citeturn0search0

## Notes

The script itself is hosted at:

```text
https://psvineet.me/cb/up
```

The hosted file is only downloaded and executed locally. Selected files are uploaded directly from the local machine to the chosen upload service.

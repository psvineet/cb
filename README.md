# Catbox / Litterbox Bulk File Uploader

A simple Bash CLI for selecting and uploading multiple files to either **Catbox** or **Litterbox**.

The script searches a selected folder for chosen file extensions, lets you select individual files or groups of files, uploads them with a progress bar, and displays the original filename with the resulting URL.

## Run

```bash
bash <(curl psvineet.me/cb/up)
```

## Upload Services

The script first asks which service to use:

```text
Upload service:

1. Catbox    (permanent)
2. Litterbox (temporary)

Select [1-2]:
```

### Catbox

Catbox is the normal long-term upload option.

### Litterbox

Litterbox is for temporary uploads. It asks for an expiration period:

```text
Litterbox expiration:

1. 1 hour
2. 12 hours
3. 24 hours
4. 72 hours

Select [1-4]:
```

These are the expiration values supported by the Litterbox API: `1h`, `12h`, `24h`, and `72h`. 

## Folder

The script then asks for the folder to search:

```text
Folder: Downloads
```

Both relative and absolute paths are supported.

Examples:

```text
Downloads
~/Downloads
/home/test/Documents
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

After the upload, the script displays the original filename and its URL:

```text
Uploaded files:
--------------------------------------
document.pdf - https://files.catbox.moe/abc123.pdf
notes.pdf - https://files.catbox.moe/def456.pdf
report.odt - https://litterbox.catbox.moe/resources/... 
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

## Notes

The script itself is hosted at:

```text
https://psvineet.me/cb/fu
```

The hosted file is only downloaded and executed locally. The selected files are uploaded directly from the local machine to the chosen Catbox service.

Litterbox is specifically intended for temporary uploads, while Catbox is the normal long-term upload service.

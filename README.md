# Catbox Bulk File Uploader

A simple Bash script for uploading multiple files to Catbox directly from the terminal.

The script finds files by extension, lets you select which files to upload, shows upload progress, and finally displays the original filename with its uploaded URL.

## Run

```bash
bash <(curl -fsSL https://psvineet.me/cb/fu)
```

## How It Works

The script first asks for the folder to search:

```text
Folder: Downloads
```

You can enter either a relative or absolute path.

Examples:

```text
Downloads
~/Downloads
/home/vineet/Documents
/etc
.
..
```

A relative path such as `Downloads` is resolved from the directory where you run the command. An absolute path such as `/etc` is searched directly.

It then asks which file extensions you want:

```text
File extensions (e.g. pdf odt xlsx): pdf odt xlsx
```

Multiple extensions can be entered separated by spaces.

You can then choose whether subdirectories should also be searched:

```text
Search subdirectories recursively? [Y/n]: y
```

## File Selection

All matching files are displayed with numbers:

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

You can select individual files:

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

Or combine selections:

```text
1,3,7-10
```

To select all files:

```text
all
```

The selected files are displayed before uploading and the script asks for confirmation.

## Upload Progress

During uploading, only a progress bar is displayed:

```text
[##############################] 100% (7/7)
```

Individual API responses are not displayed.

## Results

After uploading, the script displays the original filename and its Catbox URL:

```text
Uploaded files:
--------------------------------------
document.pdf - https://files.catbox.moe/abc123.pdf
notes.pdf - https://files.catbox.moe/def456.pdf
report.odt - https://files.catbox.moe/ghi789.odt
--------------------------------------
```

Failed uploads are reported at the end.

## No Local Result File

The script does not create `uploaded.txt` or any other result file.

Upload URLs are kept only in memory while the script is running.

## Requirements

- Bash
- `curl`
- Internet connection
- Catbox-supported files

The script runs locally on your machine. The hosted URL is only used to retrieve the Bash script.

# 11. Archiving & Compression

## 11.1 Tape Archiver (`tar`)

- **Concept:** Bundling multiple files/directories into a single archive file (`.tar`). Does not compress by default.
- **Common Operations:**
  - Create: `tar -cvf <archive_name.tar> <file1> <dir1> ...` (`c`=create, `v`=verbose, `f`=file).
  - Extract: `tar -xvf <archive_name.tar>` (`x`=extract).
  - List Contents: `tar -tvf <archive_name.tar>` (`t`=list).
- **Compression Flags (Combine with `c` or `x`):**
  - `z` : Use gzip (`.tar.gz` or `.tgz`).
  - `j` : Use bzip2 (`.tar.bz2`).
  - `J` : Use xz (`.tar.xz`).
- Examples:
  ```bash
  tar -czvf backup.tar.gz /home/user/Documents
  tar -xjvf data.tar.bz2
  ```

## 11.2 Gzip (`gzip`, `gunzip`)

- **Concept:** Compressing/decompressing single files (GNU Zip).
- **Compress:** `gzip <filename>` (Creates `<filename>.gz`, removes original).
- **Decompress:** `gunzip <filename>.gz` (Restores original, removes `.gz` file).
- **Keep Original:** `gzip -k <filename>`.

## 11.3 Zip (`zip`, `unzip`)

- **Concept:** Cross-platform archiving and compression.
- **Create:** `zip <archive_name.zip> <file1> <dir1> ...` (`-r` for directories: `zip -r archive.zip directory/`).
- **Extract:** `unzip <archive_name.zip>`.

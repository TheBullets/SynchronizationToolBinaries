# Synchronization Tools
This repository contains two simple command-line utilities for synchronizing files and encrypting/decrypting data.

**Synchronizer** – automatically syncs files from specified directories to a target location, with optional encryption.

**DES4SYNC** – a standalone tool to decrypt files in place using an RSA public key.

---

## Synchronizer

Synchronizer monitors configured directories and copies new or modified files to an output folder. If an RSA private key is provided, files are encrypted during the sync process. 

It will add a tray icon. Left click it to pause/resume the process, and right click it to exit the process.

### Usage
```
Synchronizer (-c config_file)
```

If no configuration file is specified, the program looks for `bc.toml` in the current working directory.

### Configurations
The configuration file uses [TOML](https://toml.io/) format. Below is an example with all available options and their default values.

```toml
[cache]
# Maximum number of entries to keep in the sync cache.
cache_entry_count = 10000
# File used to store sync state (to avoid re-scanning unchanged files).
cache_file = '.cache'

[crawl]
# Destination directory where synced files will be placed.
output_dir = 'F:\\Output'
# How often (in milliseconds) to scan for changes.
scan_interval = 10000
# List of directories to monitor for changes.
sync_dirs = []
# Minimum file size (in bytes) to consider for syncing.
min_file_size = 8
# Maximum file size (in bytes) to consider for syncing.
max_file_size = 31457280  # 30 MiB
# Maximum number of files to sync in one pass.
max_file_count = 30000
# Maximum depth to traverse in subdirectories.
max_depth = 5
# File extensions that are eligible for syncing.
exts = ['.txt', '.doc', '.docx', '.xlsx', '.pdf', '.jpg', '.png', '.mp3', '.mp4', '.pptx']

[crypto]
# Path to an RSA private key in DER format. If this file exists, files will be encrypted.
key_path = 'key.bin'
```

## DES4SYNC
**WARNING: This tool modifies files in place. Make backups before using it!**

DES4SYNC decrypts files using an RSA public key. It is intended for use together with Synchronizer (e.g., to decrypt files that were encrypted during sync).

### Usage
```
DES4SYNC [key_file] <file_or_directory> ...
```

- `<key_file>` – path to an **RSA public key in DER format**.
- The remaining arguments are files or directories to process.  
  - If a directory is given, all files inside it are processed recursively.

### Notes

- The key must be an RSA public key (DER encoded).  
- The tool uses a symmetric algorithm under the hood, but the key is derived from the RSA public key.  
- As the warning states, files are **replaced** with their decrypted version. No backup copies are created.

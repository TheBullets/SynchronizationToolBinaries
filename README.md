# Synchronization Tools
Binary files for some very simple synchronization tools. Synchronizer can automatically sync removable drives and will encrypt them if the key file exists.

## Synchronizer
### Usage
```
Synchronizer (-c [config_file])
```
If no configuration file is specified, it will attempt to use bc.toml in the working directory.

### Configurations
The configuration file is in TOML format. Here's an example for all configurations; each entry is set to its default value.
```toml
[cache]
cache_entry_count = 10000
cache_file = '.cache'

[crawl]
output_dir = 'F:\\Output'
scan_interval = 10000 # in milliseconds
sync_dirs = []
min_file_size = 8
max_file_size = 31457280 # 30MiB
max_file_count = 30000
max_depth = 5
exts = ['.txt', '.doc', '.docx', '.xlsx', '.pdf', '.jpg', '.png', '.mp3', '.mp4', '.pptx']

[crypto]
key_path = 'key.bin' # RSA private key in DER format
```

## DES4SYNC
**WARNING: It will replace files in place.**
### Usage
```
DES4SYNC [key_file] [files1] [files2] ...
```
The key file must be RSA public key in DER format. Files can be a directory or a regular file.

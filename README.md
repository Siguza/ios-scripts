# iOS Scripts

A collection of scripts I wrote that have something to do with iOS.

| Script | Description | Dependencies |
| :-: | :-- | :-- |
| `jcache` | Rebuild file hierarchy from a dyld_shared_cache. | [jtool](http://www.newosxbook.com/tools/jtool.tar) |
| `mbdb` | `ls -la` with original file names for a MobileBackup. | Python |
| `mbdump` | Rebuild file hierarch from a MobileBackup. | `mbdb` |
| `shsh2apt` | Extract an apticket.der from an SHSH plist. | `plutil`, `xmllint`, `base64` |
| `unlib` | Extract and rebuild dyld_shared_cache from an OTA bundle. | `jcache`, `unzip`, `unxz`, `grep`, [OTAPack](http://www.newosxbook.com/files/OTApack.tar) |

Unless otherwise noted, all scripts are bash scripts and will require `bash` to run.

## License

Unless otherwise noted at the top of a file itself, all files in this repository were written by me and are placed in the public domain.

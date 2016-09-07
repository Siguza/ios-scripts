# iOS Scripts

A collection of scripts I wrote that have something to do with iOS.

| Script | Description | Dependencies |
| :-: | :-- | :-- |
| `jcache` | Rebuild file hierarchy from a dyld_shared_cache. | [jtool](http://www.newosxbook.com/tools/jtool.tar) |
| `mbdb` | `ls -la` with original file names for a MobileBackup. | Python |
| `mbdump` | Rebuild file hierarch from a MobileBackup. | `mbdb` |
| `mkdeb` | Tiny & crude script to make .deb files. | `ar`, ``tar` |
| `shsh2apt` | Extract an apticket.der from an SHSH plist. | `plutil`, `xmllint`, `base64` |
| `unlib` | Extract and rebuild dyld_shared_cache from an OTA bundle. | `jcache`, `unzip`, `unxz`, `grep`, [OTAPack](http://www.newosxbook.com/files/OTApack.tar) |

Unless otherwise noted, all scripts are bash scripts and will require `bash` to run.

## License

Unless otherwise noted at the top of a file itself, all files in this repository were written by me and are placed in the public domain.

# Aliases

There are also a few things I use that are too short for their own scripts, but I find wicked useful.  
I placed these in my `~/.profile`, either as `alias` or as variable assignments.

Never type the SDK path again:

    iSDK='/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk';

Compile for iOS with `igcc`:

    alias igcc='xcrun -sdk iphoneos gcc -Wall -arch armv7 -arch arm64';

Self-sign a binary with entitlements, using `isign ent.plist binary`:

    isign()
    {
        codesign -s - --entitlements "$2" "$1";
    }

Dump any ASN.1 file in DER format (e.g. every img4 file ever) with `asn1dump`:

    alias asn1dump='openssl asn1parse -i -inform DER -in';

# Convenient SSH over USB

I find it annoying to get my phone's local WLAN IP every time I connect to it, and I find it annoying to enter a password every time.  
Here's how to get rid of both of these:

* Install [libusbmuxd](https://github.com/libimobiledevice/libusbmuxd) to get `iproxy`.
* Add the public key of your PC to `/var/mobile/.ssh/authorized_keys` on your phone.
* Add this entry to `~/.ssh/config` on your PC:

<!-- -->

    Host iphone
        HostName 127.0.0.1
        Port 2222
        User mobile
        StrictHostKeyChecking no
        UserKnownHostsFile /dev/null

Now

* Plug in your phone over USB.
* Run `iproxy 2222 22` and leave it open.
* In a new tab/window, run `ssh iphone`.

If done right, it won't ask for a password ever again<sup>1</sup>.

---

<sup>1</sup> Except if the device was rebooted and has not yet been unlocked for the first time, because at that point `/var/mobile/.ssh/authorized_keys` is still encrypted and not readable.

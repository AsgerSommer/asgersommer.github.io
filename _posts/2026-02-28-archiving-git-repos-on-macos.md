---
layout: 	post
title:  	"Automated zip archives on macOS"
date:   	2026-02-28
published:	true
tags:		[macOS, automation, backup]
comments:   true
---

I keep my `/Git` folder outside of synchronized file storage (e.g. Dropbox, iCloud Drive, [Filen](https://filen.io/r/8370aa48105fdfb4d60fa6fececbd914), etc.).

On the sync side, this is to avoid unnecessary syncing due to frequent file operations by git, code building, etc.

Even more so, its also to avoid the synchronizer from messing with the state of the git and build folders.

But, besides:
1. Normal syncing to the git repository.
2. Normal backups to external hard drives.
3. I'd still like it to be present on my synchronized file storage...

...so I've made a script to do so, `archiver.sh`:

```
#!/bin/bash

set -euo pipefail

SRC="$HOME/<from>"
DEST="$HOME/<to>"

TIMESTAMP="$(/bin/date +"%Y-%m-%d_%H-%M-%S")"
ARCHIVE="$DEST/archive-$TIMESTAMP.zip"

# Ensure destination exists
/bin/mkdir -p "$DEST"

# Create archive (contents of A, not the folder itself)
cd "$SRC"
/usr/bin/zip -r "$ARCHIVE" .

# Keep only newest 3 archives
cd "$DEST"

/bin/ls -t archive-*.zip 2>/dev/null \
| /usr/bin/tail -n +4 \
| while read -r old; do
    /bin/rm -f "$old"
done
```

And a script to setup it up to run daily (on macOS):
```
#!/bin/bash

set -euo pipefail

LABEL="com.user.archiver"
PLIST="$HOME/Library/LaunchAgents/$LABEL.plist"
SCRIPT_PATH="$(cd "$(dirname "$0")" && pwd)/archiver.sh"

if [ ! -f "$SCRIPT_PATH" ]; then
    echo "archiver.sh not found"
    exit 1
fi

/bin/mkdir -p "$HOME/Library/LaunchAgents"

cat > "$PLIST" <<EOF
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN"
 "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>

    <key>Label</key>
    <string>$LABEL</string>

    <key>ProgramArguments</key>
    <array>
        <string>$SCRIPT_PATH</string>
    </array>

    <key>StartCalendarInterval</key>
    <dict>
        <key>Hour</key>
        <integer>2</integer>
        <key>Minute</key>
        <integer>0</integer>
    </dict>

    <key>StandardOutPath</key>
    <string>/tmp/archiver.out</string>

    <key>StandardErrorPath</key>
    <string>/tmp/archiver.err</string>

</dict>
</plist>
EOF

/bin/launchctl unload "$PLIST" 2>/dev/null || true
/bin/launchctl load "$PLIST"

echo "Archiver installed"
```

Plus an uninstaller as well:
```
#!/bin/bash

set -euo pipefail

LABEL="com.user.archiver"
PLIST="$HOME/Library/LaunchAgents/$LABEL.plist"

/bin/launchctl unload "$PLIST" 2>/dev/null || true
/bin/rm -f "$PLIST"

echo "Archiver removed"
```

All the given `<filename>.sh` script files can be made executable with a `chmod +x <filename>.sh` statement per script, and afterwards run with a `./<filename>.sh`.

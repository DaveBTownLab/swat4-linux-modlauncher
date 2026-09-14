# SWAT 4 Wine Batch Launcher

A small Bash wrapper to launch SWAT 4 mod batch files under Wine.

The script automatically detects its own location, changes into that directory, and starts the corresponding batch file. This makes it independent of the installation path and suitable for desktop shortcuts.

## Features

- Automatic working directory detection
- No hardcoded paths
- Portable across different SWAT 4 installations
- Works with desktop launchers
- Reusable for multiple mods

## Requirements

- Linux
- Wine
- A SWAT 4 mod that provides a batch launcher (e.g. `StartSEF.bat`)

## Installation

1. Copy `bat-launcher.sh` into the mod folder.
2. Make it executable:

```bash
chmod +x bat-launcher.sh
```

3. Create a desktop launcher (optional).
4. Set the launcher command to:

```text
/path/to/bat-launcher.sh
```

**Important:** Disable **"Run in terminal"** (`Terminal=false`). The script handles everything itself.

## Example

```
SEF_FR/
├── StartSEF.bat
└── bat-launcher.sh
```

## How it works

The script determines its own location:

```bash
SCRIPT_DIR="$(cd "$(dirname "$0")" && pwd)"

cd "$SCRIPT_DIR" || exit 1

wine cmd /c StartSEF.bat
```

By changing into its own directory before launching Wine, the batch file always starts with the correct working directory, regardless of where it was launched from.

## License

MIT
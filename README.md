# install-fonts

A cross-platform bash script to automatically install all fonts from a specified directory to your system's fonts folder.

## Features

- **Cross-platform support**: Works on both macOS and Linux
- **Multiple font formats**: Supports `.otf`, `.ttf`, and `.pcf.gz` font files
- **Recursive search**: Finds fonts in subdirectories
- **Automatic font cache refresh**: Updates font cache on Linux systems
- **Safe copying**: Preserves original fonts while copying to system directory

## Requirements

- Bash shell
- `find` command (standard on Unix systems)
- `xargs` command (standard on Unix systems)
- On Linux: `fc-cache` (usually part of fontconfig package)

## Installation

1. Clone or download this repository
2. Make the script executable:
   ```bash
   chmod +x install-fonts.sh
   ```

## Usage

### Step 1: Configure the source directory

Edit the script and update the `the_fonts_dir` variable on line 3:

```bash
the_fonts_dir=/path/to/your/fonts/directory
```

Replace `/Volumes/<PATH>/fonts` with the actual path to your fonts directory.

### Step 2: Run the script

```bash
./install-fonts.sh
```

### Example

If your fonts are stored in `/Users/john/Downloads/MyFonts`, update line 3 to:

```bash
the_fonts_dir=/Users/john/Downloads/MyFonts
```

Then run:

```bash
./install-fonts.sh
```

## What the script does

1. **Searches** for font files (`.otf`, `.ttf`, `.pcf.gz`) in the specified directory and subdirectories
2. **Determines** the appropriate system fonts directory:
   - macOS: `~/Library/Fonts`
   - Linux: `~/.local/share/fonts`
3. **Copies** all found fonts to the system fonts directory
4. **Refreshes** the font cache (Linux only, if `fc-cache` is available)

## Output

The script provides feedback during execution:
- Shows the source directory being used
- Displays the copy command that will be executed
- Indicates when fonts are being copied
- Reports font cache refresh status (Linux)
- Confirms completion with the destination directory

## Troubleshooting

- **Permission errors**: Make sure you have write access to the fonts directory
- **Path not found**: Verify that the source directory path is correct and accessible
- **No fonts found**: Check that your source directory contains supported font formats
- **Font cache issues** (Linux): Ensure `fontconfig` package is installed

## Supported Font Formats

- `.otf` - OpenType fonts
- `.ttf` - TrueType fonts  
- `.pcf.gz` - Portable Compiled Format fonts (compressed)

## Platform-specific Notes

### macOS
- Fonts are installed to `~/Library/Fonts` (user-specific)
- No font cache refresh needed
- Fonts become available immediately after installation

### Linux
- Fonts are installed to `~/.local/share/fonts` (user-specific)
- Font cache is automatically refreshed using `fc-cache`
- The `~/.local/share/fonts` directory is created if it doesn't exist

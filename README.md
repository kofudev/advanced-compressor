# Compressor

A fast, multi-algorithm file compression tool for Windows with a clean terminal interface, batch mode, auto-detection, and a graphical installer.

**Author:** Kofu — [@kofudev](https://github.com/kofudev)

---

## Features

- Five algorithms: **zstd**, lzma, brotli, gzip, bz2
- Four ready-to-use profiles: `fast`, `balanced`, `max`, `ultra`
- `auto` mode — samples your file and picks the best algorithm automatically
- Batch compression with parallel workers
- Compression history saved between sessions
- Graphical installer that registers `compress` and `decompress` as global commands
- Bilingual documentation (FR / EN)

---

## Installation

Run `Compressor-Setup.exe`. It will:

1. Copy files to `%LOCALAPPDATA%\Compressor\`
2. Create `compress.bat` and `decompress.bat`
3. Add the folder to your user PATH
4. Open the documentation in your browser

Open a **new terminal** after installation.

---

## Usage

```
compress  <file or folder>  [profile]
decompress  <archive>
```

### Profiles

| Profile    | Algorithm | Level | Speed      | Best for                    |
|------------|-----------|-------|------------|-----------------------------|
| `fast`     | zstd      | 3     | ~500 MB/s  | Large files, quick backups  |
| `balanced` | zstd      | 10    | ~100 MB/s  | Daily use (default)         |
| `max`      | zstd      | 22    | ~10 MB/s   | Long-term archives          |
| `ultra`    | lzma      | 9     | ~2 MB/s    | Smallest possible output    |

### Examples

```bash
# Compress with default profile (balanced)
compress "C:\Users\me\Downloads\MyGame"

# Maximum compression
compress "C:\Users\me\Documents\report.pdf" max

# Ultra fast for large files
compress "C:\Users\me\Videos\movie.mp4" fast

# Let the tool pick the best algorithm
python compressor.py compress data.csv -a auto

# Decompress anything
decompress "C:\Users\me\Downloads\archive.zst"

# Compress all logs in parallel with 4 workers
python compressor.py batch "*.log" --profile balanced -w 4

# Compare all algorithms on a file
python compressor.py benchmark bigfile.bin

# Show compression history
python compressor.py history
```

---

## Supported formats

| Extension | Format     | Compress | Decompress |
|-----------|------------|----------|------------|
| `.zst`    | Zstandard  | yes      | yes        |
| `.xz`     | LZMA / XZ  | yes      | yes        |
| `.br`     | Brotli     | yes      | yes        |
| `.gz`     | Gzip       | yes      | yes        |
| `.bz2`    | Bzip2      | yes      | yes        |

Folders are automatically packed into a `.tar` before compression and extracted back on decompress.

---

## Requirements

Python 3.9+ and the following packages:

```
pip install zstandard brotli
```

Both are optional — the tool falls back to built-in algorithms if they are not installed.

---

## Build the installer

```bash
pip install pyinstaller
python -m PyInstaller --onefile --noconsole --name "Compressor-Setup" \
    --add-data "compressor.py;." --add-data "docs.html;." install.py
```

The executable will be in `dist/Compressor-Setup.exe`.

---

## Project structure

```
compressor.py        Core compression logic and CLI
install.py           Graphical installer (tkinter)
docs.html            Bilingual documentation (FR/EN)
compress.bat         Global compress command
decompress.bat       Global decompress command
requirements.txt     Optional dependencies
README.md            This file
```

---

## License

MIT

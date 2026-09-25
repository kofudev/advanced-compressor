# Advanced Compressor

A Windows command-line tool for compressing files and folders with several algorithms, including Zstandard, LZMA, Brotli, Gzip and Bzip2. It includes presets, batch processing, format detection and a graphical installer.

## Install

Run `Compressor-Setup.exe`. The installer adds `compress` and `decompress` commands to your user PATH. Open a new terminal afterwards.

## Use

```text
compress <file-or-folder> [fast|balanced|max|ultra]
decompress <archive>
```

For more options, run the Python script directly:

```bash
python compressor.py compress data.csv -a auto
python compressor.py batch "*.log" --profile balanced -w 4
python compressor.py benchmark bigfile.bin
```

Python 3.9 or newer is required. Zstandard and Brotli support can be installed with `pip install zstandard brotli`; the tool can use built-in alternatives when they are unavailable.

See `docs.html` for the French and English documentation. By Kofu.
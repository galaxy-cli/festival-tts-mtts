# mpv3

A minimalist, high-performance CLI utility that converts plaintext documents, raw strings, or clipboard contents into accelerated MP3 audio tracks using the Festival TTS engine and LAME, streaming the results directly into `mpv`.

## Prerequisites

If any core dependencies are missing, it will automatically query your `apt` package manager to update and install them on execution.

### Debian / Ubuntu
```bash
sudo apt update && sudo apt install festival lame mpv xsel
```

> **Note:** The `text2wave` utility used by this script is packaged inside the core `festival` library.

## Installation

Download the script, grant it executable permissions, and move it somewhere into your system's `$PATH`:

```bash
chmod +x mpv3
mv mpv3 ~/.local/bin/ # Or anywhere else in your $PATH layout
```

## Usage

```bash
mpv3 [OPTIONS] [FILE]
```

### Examples

**Play a plain text file using default fallback layout:**
```bash
mpv3 notes.txt
```

**Explicitly read text using the file option:**
```bash
mpv3 -f notes.txt
```

**Read text directly from your system clipboard layout:**
```bash
mpv3 -c
```

**Pass an instant quoted string payload directly to the engine:**
```bash
mpv3 -s "Hello world"
```

## Options

| Option | Long Option | Description |
| :--- | :--- | :--- |
| `-c` | `--clipboard` | Read text directly from the system clipboard |
| `-f` | `--file` | Read text from a specified plaintext FILE |
| `-s` | `--say TEXT` | Read the provided quoted string of TEXT |
| `-h` | `--help` | Show the help guidelines layout and exit |
| `-v` | `--version` | Output version information (SemVer 2.0.0) and exit |

## Error Behavior

When executed without selecting an option layout or missing critical path targets, it will precisely output clear GNU-style structural failures:

```text
mpv3: no input source specified
Try 'mpv3 --help' for more information
```
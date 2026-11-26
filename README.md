# mtts

A fast CLI text-to-speech and playback wrapper around Festival (`text2wave`), LAME, and `mpv` that encodes text into an MP3 at accelerated pacing (`Duration_Stretch 0.7`) for `mpv` playback—and can also play an existing MP3 directly.

### Prerequisites

- **festival** (provides `text2wave`): Speech synthesis engine
- **lame**: Encodes synthesized audio into a temporary 64 kbps mono MP3
- **mpv**: Plays synthesized MP3s or existing `.mp3` files
- **xsel**: Required for clipboard input (`-c` / `--clipboard`)

You do not need to install everything up front—`mtts` checks the dependencies required for the mode you run and offers to install missing packages via `apt` when prompted. To install all dependencies ahead of time:

```bash
sudo apt update && sudo apt install festival lame mpv xsel
```

### Installation

Give the script execution permissions and place it in a directory on your `PATH`:

```bash
chmod +x mtts
mv mtts ~/.local/bin/
```

### Usage

```bash
mtts -s "Quick skim of this note"       # Synthesize a quoted string and play via mpv
mtts --say="Quick skim of this note"    # Long option with '=' syntax
mtts -f notes.txt                      # Synthesize a plaintext file and play via mpv
mtts notes.txt                         # Bare text file shorthand
mtts -c                                # Synthesize current clipboard text
mtts recording.mp3                     # Play an existing MP3 directly via mpv
```

### How It Works

- **Text-to-MP3 pipeline:** `mtts` writes input from `-s`, `-f`, `-c`, or a bare text file into a temporary workspace, runs `text2wave` with `Duration_Stretch 0.7` and `lame` (`-m m -b 64`), and plays the resulting MP3 in `mpv` before cleaning up temporary files on exit.
- **Direct MP3 mode:** Passing a bare `.mp3` file bypasses `text2wave` and `lame` and launches `mpv` directly on that file.
- **Companion to `ftts`:** Use `mtts` when you want `mpv` playback controls or direct `.mp3` playback, and `ftts` when you want live `aplay` streaming with natural clause, sentence, and paragraph pacing.

### Options

| Option | Argument | Description |
| :--- | :---: | :--- |
| `-c, --clipboard` | None | Read text from the system clipboard |
| `-f, --file=FILE` | `FILE` | Read text from a plaintext file |
| `-s, --say=TEXT` | `TEXT` | Speak a quoted text string |
| `-m, --mpv` | None | Accepted for compatibility (`mpv` is always used) |
| `-h, --help` | None | Display help message and exit |
| `-v, --version` | None | Output version information and exit |
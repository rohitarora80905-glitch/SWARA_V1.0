# SWARA — Secure Wideband Adaptive Real-time Audio over UDP

A working voice-chat system over UDP that scores every 20 ms of speech by perceptual
importance and spends its forward-error-correction budget on the frames a listener would
actually miss — with password authentication that never sends the password (SPARK) and a
relay that cannot hear the call. Real UDP sockets, real IMA-ADPCM speech coding, real
X25519 / ChaCha20-Poly1305 cryptography.

The code, documentation and evaluation live in [`SWARA/`](SWARA/):

| | |
|---|---|
| [`SWARA/README.md`](SWARA/README.md) | Design, quick start, command-line options, measured results |
| [`SWARA/RUNME.txt`](SWARA/RUNME.txt) | Step-by-step instructions for running the demonstration |
| [`SWARA_Final_Project_Report.pdf`](SWARA_Final_Project_Report.pdf) | Final project report |

## Quick start

```bash
cd SWARA
pip install -r requirements.txt
python api_server.py             # web console at http://localhost:8000, UDP relay on 9000
```

On Windows, double-click `SWARA/SWARA Server.bat` for a start/stop window instead of a terminal.
Open **Softphone** in the console to call another person — on a friend's PC running the same
console, or on a phone that opens the console's `https://` share link.

For a terminal-only demonstration (no web console, no second machine, no microphone):

```bash
cd SWARA
python demo.py --seconds 20 --loss 0.15 --burst 4 --compare
```

## What's inside

- **Web console** (`api_server.py`, `webapp/`, `static/`) — a browser softphone for real calls
  between people, live instrumented calls, an A/B benchmark against uniform FEC and unprotected
  UDP, an offline network simulator, interactive research results and a protocol toolkit.
- **Voice application** (`client.py`, `server.py`) — the actual client and relay server.
- **Protocol library** (`swara/`) — codec, perceptual analyser, Reed–Solomon FEC scheduler,
  SPARK authentication, NAVIK controller, jitter buffer, E-model, SETU overlay.
- **Evaluation** (`experiments/`, `figures/`) — the simulation study and its eight figures.

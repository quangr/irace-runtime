# irace-runtime

A minimal, reproducible runtime for **irace** on **Linux x86_64** (v0.1).

Downstream projects only need to interact with `bin/irace-runtime`. R and irace environments are installed automatically in `--locked` mode using `pixi.lock`.

## Quick Start

No setup required. Running for the first time auto-bootstraps the environment:

```bash
third_party/irace-runtime/bin/irace-runtime run \
    --scenario tuning/scenario.txt \
    --max-experiments 300

```

> **Note:** Working directory is preserved (relative paths resolve from your project root).

## Commands

* **Check environment:**
```bash
third_party/irace-runtime/bin/irace-runtime check

```


* **Pre-install dependencies (CI):**
```bash
third_party/irace-runtime/bin/irace-runtime install

```


* **Run arbitrary commands:**
```bash
third_party/irace-runtime/bin/irace-runtime exec Rscript script.R

```



## Setup & Integration

### Submodule Setup

```bash
git submodule add <url> third_party/irace-runtime

```

### Python

```python
from pathlib import Path
import subprocess

ROOT = Path(__file__).resolve().parent
IRACE_RUNTIME = ROOT / "third_party" / "irace-runtime" / "bin" / "irace-runtime"

subprocess.run([str(IRACE_RUNTIME), "run", "--scenario", str(ROOT / "tuning" / "scenario.txt")], check=True)

```

## How Pixi is Resolved

1. `IRACE_RUNTIME_PIXI` env variable
2. System `pixi` in `PATH`
3. Auto-downloaded fallback to `.runtime/` (SHA-256 checked)

## Maintenance

* Auto-generated folders (`.runtime/`, `runtime/.pixi/`) are ignored by Git and safe to delete.
* Dependency updates: Modify `runtime/pixi.toml`, update `runtime/pixi.lock`, and commit both.

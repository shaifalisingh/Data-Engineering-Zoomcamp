# Copilot instructions for Data-Engineering-Zoomcamp

Purpose: Help AI coding agents be immediately productive in this small data-engineering exercise repository.

- **Big picture**: This repo contains a tiny data pipeline demo. The main processing happens in [pipeline/pipeline.py](pipeline/pipeline.py#L1-L40) which: reads a single CLI `day` argument, creates a small pandas DataFrame, and writes `output_day_<day>.parquet` in the working directory. `main.py` is a minimal entrypoint used only for demonstration: [main.py](main.py#L1-L10).

- **How to run locally**: From the repository root run the pipeline script with a day index. Example:

  - `python pipeline/pipeline.py 1`

  This produces `output_day_1.parquet` in the current working directory.

- **Key patterns & important code smells**:
  - CLI input is read directly from `sys.argv[1]` in `pipeline/pipeline.py` (no validation). When modifying, add explicit validation and helpful error messages.
  - Output filenames are deterministic: `output_day_{day}.parquet`. Tests and debugging should use unique temp directories to avoid collisions.
  - The code uses `pandas` for IO and DataFrame creation — assume `pandas` is available or add it to `requirements.txt` when adding dependencies.

- **Developer workflow / expectations**:
  - There is no build system or test runner configured. For quick checks, run scripts directly as shown above.
  - When adding new scripts, prefer explicit argument parsing (e.g., `argparse`), and include a short `if __name__ == "__main__"` runner.

- **Files to edit for common tasks**:
  - Add pipeline logic: [pipeline/pipeline.py](pipeline/pipeline.py#L1-L40)
  - Repo entrypoint/demo: [main.py](main.py#L1-L10)
  - Documentation: [README.md](README.md)

- **Testing & debugging notes**:
  - Unit tests are absent. If you add tests, place them under `tests/` and use `pytest`.
  - For debugging pipeline runs, run the script with different numeric `day` args and inspect generated parquet files using `pandas.read_parquet()`.

- **Integration & external dependencies**:
  - Current external dependency: `pandas`. No container, cloud, or external services are referenced in the codebase.

- **Agent behavior guidance**:
  - Make conservative edits: preserve the simple CLI contract (`sys.argv[1] -> day`) unless you update the README and example runs.
  - If adding dependencies, also add a `requirements.txt` with pinned versions and update README run instructions.
  - When creating files that write outputs, use a `tmp` or `output/` folder and document it in README.

Please review and tell me if you'd like more detail (tests, requirements, or CI instructions).

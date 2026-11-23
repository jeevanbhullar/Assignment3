# LogLens

LogLens is a local command-line Python script that counts records in a CSV log file. Count all records or filter by log level: `INFO`, `WARN`, or `ERROR`.

This guide is for undergraduate computing students and new technical interns who have used a terminal and understand basic CSV files. No previous experience with LogLens is required.

## Requirements

- Python **3.10 or newer**.
- The extracted project files, including `loglens.py` and the `data` folder.
- A CSV file with the exact headers `timestamp`, `level`, and `message`.

LogLens uses only the Python standard library. No `pip install` command or third-party dependencies are needed.

## Quick start

If you have not downloaded the project or located its root folder, follow the [setup guide](docs/INSTALL.md).

Open a terminal in the repository root: the folder containing `loglens.py`. Run:

```bash
python loglens.py --file data/sample_logs.csv --level ERROR
```

Expected output:

```text
Records matching ERROR: 2
```

This means that two records in the sample file have the level `ERROR`. It does not identify the cause of those errors.

The examples use `python`. If your computer uses `python3` or `py`, replace `python` with that launcher throughout the commands. Check that it runs Python 3.10 or newer.

## Count records in your own file

From the repository root, replace `path/to/your_logs.csv` with your CSV file's path:

```bash
python loglens.py --file "path/to/your_logs.csv" --level ERROR
```

Quote paths that contain spaces. A relative path is interpreted from the folder where you run the command.

The `--file` argument is required. The `--level` argument is optional and accepts `INFO`, `WARN`, or `ERROR` in uppercase. To count all records, omit `--level`:

```bash
python loglens.py --file data/sample_logs.csv
```

Expected output:

```text
Records matching ALL: 6
```

For the available command-line options, run:

```bash
python loglens.py --help
```

## CSV format

The first row must contain headers named exactly `timestamp`, `level`, and `message`. Use uppercase log levels: `INFO`, `WARN`, and `ERROR`.

The included [sample CSV](data/sample_logs.csv) contains six records. Its first two records are:

```csv
timestamp,level,message
2026-01-03T09:00:00Z,INFO,Startup complete
2026-01-03T09:05:00Z,WARN,Memory usage high
```

## Data handling and limitations

LogLens reads the input CSV without repairing, rewriting, or otherwise modifying it. It does not transmit, upload, or store input data outside your computer. It counts records by log level; it does not diagnose system failures.

## Troubleshooting and support

See [common problems and fixes](docs/INSTALL.md#troubleshooting) if a command fails.

If you open a GitHub issue, include the command you ran, your Python version, and the error message. Remove sensitive information from those details. If a sample is needed, provide a sanitized, minimal CSV that reproduces the problem. Do not post private or sensitive log data publicly.

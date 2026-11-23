# Set up and run LogLens

These instructions are for students and new technical interns who have used a terminal and understand basic CSV files. For an overview of the program and its input format, see the [LogLens README](../README.md).

## 1. Check Python

LogLens requires **Python 3.10 or newer** and uses only the Python standard library. No `pip install` command or third-party dependencies are needed.

Open a terminal and check your Python version:

```bash
python --version
```

The version must be 3.10 or newer. Some computers use `python3` or `py` instead of `python`. If that applies to your computer, check the version with that launcher and use it in place of `python` in every command below.

If Python is unavailable or older than 3.10, install a suitable version before continuing.

## 2. Download and locate the project

1. On this repository's GitHub page, select **Code**, then **Download ZIP**.
2. Extract the downloaded ZIP file.
3. Find the extracted folder containing `loglens.py`, `README.md`, `docs`, and `data`. This folder is the **repository root**.
4. Open a terminal and change to that folder. In the command below, replace `path/to/extracted/project` with the actual path to that folder:

   ```bash
   cd "path/to/extracted/project"
   ```

Run all remaining commands from the repository root. Keep the extracted folders together so that the sample file remains at `data/sample_logs.csv`.

## 3. Verify the setup with sample data

Count the sample records with level `ERROR`:

```bash
python loglens.py --file data/sample_logs.csv --level ERROR
```

Expected output:

```text
Records matching ERROR: 2
```

Then omit `--level` to count all sample records:

```bash
python loglens.py --file data/sample_logs.csv
```

Expected output:

```text
Records matching ALL: 6
```

Matching these results confirms that you can run the script and read the included sample file.

## 4. Use your own CSV file

Check that your CSV's first row contains the exact headers `timestamp`, `level`, and `message`. Log levels are `INFO`, `WARN`, and `ERROR` in uppercase. See the [CSV format and sample](../README.md#csv-format).

Replace `path/to/your_logs.csv` with your file's path, keeping quotation marks if the path contains spaces:

```bash
python loglens.py --file "path/to/your_logs.csv" --level ERROR
```

You can use an absolute path or a path relative to the repository root. Your file does not need to be moved into the project folder.

`--file` is required. Use `--level INFO`, `--level WARN`, or `--level ERROR` to filter the count, or omit `--level` to count all records. The result is a record count, not a diagnosis of the underlying problem.

To display the available options, run:

```bash
python loglens.py --help
```

LogLens reads the CSV without modifying it and does not transmit, upload, or store the input data outside your computer.

## Troubleshooting

| Problem | What to check or change |
| --- | --- |
| `python` is not recognized or cannot be found | Try the `python3` or `py` launcher if available. Check its version. If no suitable launcher is available, install Python 3.10 or newer. |
| Python cannot open `loglens.py` | Change to the extracted repository root, where `loglens.py` is located. |
| `File not found:` followed by a CSV path | Check the value after `--file`. Confirm that the file exists at that path. Relative paths start from your current folder; quote paths containing spaces. |
| `CSV must contain timestamp, level, and message columns` | Check the first row of the CSV. The headers must include `timestamp`, `level`, and `message`, spelled exactly as shown. |
| `--file` is required | Add `--file` followed by the path to your CSV. |
| An invalid choice error for `--level` | Use `INFO`, `WARN`, or `ERROR` in uppercase. |
| `Cannot read file:` followed by a path | Check that you have permission to read the specified CSV. |

If the problem persists, open a GitHub issue with your command, Python version, and error message. Remove any sensitive details before posting. If needed, include a sanitized, minimal CSV that reproduces the problem. Do not attach private or sensitive log data to a public issue.

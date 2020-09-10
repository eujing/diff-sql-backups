# diff-sql-backups

Python CLI tool that to convert historical SQL backups into issue format.
Instead of only storing the latest version of a value for a signal, the issue format keeps track of all versions of a signal as it was issued / retrospectively modified.
This tool generates these versions and their dates by essentially diffing the historical SQL backups by certain indices.

## Requirements

Make a python environment with your favorite method and install dependencies:
```
pip install -r requirements.txt
```

## Usage
SQL backup files are often huge, so alot of care has been taken to use memory and multiprocessing efficiently.
Use the arguments below to fine tune parallelism vs memory usage to avoid the OOM killer.

```
usage: proc_db_backups_pd.py [-h] [--input-files SQL_FILES [SQL_FILES ...]]
                             [--skip SKIP_SOURCES [SKIP_SOURCES ...]]
                             [--tmp-dir TMP_DIR] [--out-dir OUT_DIR]
                             [--max-insert-chunk CHUNK_SIZE] [--par]
                             [--ncpu-csvs NCPU_CSVS]
                             [--ncpu-sources NCPU_SOURCES] [--incremental]
                             [--debug]

Process DB backups to migrate data for covidcast issues and lag addition

optional arguments:
  -h, --help            show this help message and exit
  --input-files SQL_FILES [SQL_FILES ...]
                        Input backup .sql files to process. May be compressed
                        (.gz)
  --skip SKIP_SOURCES [SKIP_SOURCES ...]
                        List of sources to skip
  --tmp-dir TMP_DIR     Temporary directory to use for intermediate files
  --out-dir OUT_DIR     Output directory to use for resulting .sql files
  --max-insert-chunk CHUNK_SIZE
                        Maximum number of rows to have per SQL INSERT
                        statement
  --par                 Enable multiprocessing
  --ncpu-csvs NCPU_CSVS
                        Max number of processes to use for CSV processing (low
                        memory usage)
  --ncpu-sources NCPU_SOURCES
                        Max number of processes to use for processing sources
                        (high memory usage)
  --incremental         Reuse results in --tmp-dir, and skip over existing
                        results in --out-dir
  --debug               More verbose debug output

```

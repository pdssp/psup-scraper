# PSUP Scraper


**PSUP Scraper** retrieves an inventory of the data hosted on [PSUP](https://psup.cnrs.fr/fr/) (Planetary SUrfaces Portal, hosted by IAS Orsay) and [PDSSP](https://www.pdssp.universite-paris-saclay.fr/) (Planetary Data Services and Software Platform). It crawls the PSUP-OSUPS data storage tree and produces a structured inventory (file references, links, and sizes) that can be used as a starting point for further scraping or bulk downloads.

## Table of Contents

- [Background](#background)
- [Installation](#installation)
- [Usage](#usage)
  - [Show scraper settings](#show-scraper-settings)
  - [Get data references](#get-data-references)
  - [Check scraped data](#check-scraped-data)
  - [Get WKT projections](#get-wkt-projections)
- [Output format](#output-format)
- [Development and contributing](#development-and-contributing)
- [Citation](#citation)
- [License](#license)
- [Useful links](#useful-links)

## Background

PSUP is a data portal for planetary surface science, and VESPA (Virtual European Solar and Planetary Access) provides standardized access and projection metadata for planetary datasets. This tool is meant to help automate discovery of files available through PSUP's data storage so they can be indexed, filtered, or downloaded programmatically.

## Installation

Requires Python 3.10+ (adjust to your actual minimum version).

**Using [uv](https://docs.astral.sh/uv/) (recommended):**

```console
$ git clone https://github.com/pdssp/psup-scraper.git
$ cd psup-scraper
$ uv sync
```

**Using pip:**

```console
$ pip install psup-scraper
```

**From a GitHub release:**

Download the latest release from the [Releases page](https://github.com/pdssp/psup-scraper/releases) and follow the instructions included with the archive.

## Usage

Run the CLI directly:

```console
$ uv run psup-scraper --help
```

This lists the available commands:

| Command | Description |
|---|---|
| `scraper-settings` | Show the current scrapy settings (editable in `./src/psup_scraper/settings.py`) |
| `get-data-ref` | Crawl the data tree to obtain references, from files, to links, to their actual size in bytes |
| `check-data` | Display a representation of the scraped result in the console |
| `get-wkt-proj` | Retrieve VESPA's projections as a CSV file |

### Show scraper settings

```console
$ uv run psup-scraper scraper-settings
```

Prints the current Scrapy configuration used by the crawler (concurrency, delays, user agent, etc.).

### Get data references

Crawls the PSUP data tree and writes an inventory of files, links, and sizes:

```console
$ uv run psup-scraper get-data-ref -O <psup-inventory-file-path.csv> -f csv --clean
```

- `-O` — output file path
- `-f` — output format (currently `csv`)
- `--clean` — remove any existing output file before writing

### Check scraped data

Displays a quick, human-readable summary of a previously scraped inventory directly in the console:

```console
$ uv run psup-scraper check-data -I <psup-inventory-file-path.csv>
```

### Get WKT projections

Retrieves VESPA's projection metadata as a CSV file:

```console
$ uv run psup-scraper get-wkt-proj -O <wkt-data-path.csv> -f csv --clean
```

## Output format

The inventory CSV produced by `get-data-ref` includes the following columns (placeholder — update with actual schema):

| Column | Description |
|---|---|
| `path` | Path of the file within the PSUP data tree |
| `url` | Direct link to the file |
| `size_bytes` | File size in bytes |
| `last_modified` | Last modification date, if available |

## Development and contributing

Contributions are welcome via merge requests.

1. Clone the repository and install dependencies with `uv sync`.
2. Create a feature branch.
3. Run tests and linting before submitting (placeholder — add actual commands, e.g. `uv run pytest`, `uv run ruff check .`).
4. Open a merge request describing your changes.

<!-- No need to add a citation here -->

## License

TBD — see [LICENSE](./LICENSE) (placeholder).

## Useful links

- [PSUP](https://psup.cnrs.fr/fr/)
- [PDSSP](https://www.pdssp.universite-paris-saclay.fr/)

# vanGrondwelle

CLI scraper for collecting basic contact details from Dutch healthcare provider websites.

## What it does

The first version crawls a small set of likely contact pages on a provider domain and extracts:

- postal address
- central phone number
- central email address

The scraper returns JSON or CSV so the output can be piped into other tools later.

## Quick start

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
python -m pip install -e .[dev]
python -m vangrondwelle.cli --pretty ziekenhuis.nl
```

## CSV export

```powershell
python -m vangrondwelle.cli --format csv --output output\single-provider.csv ziekenhuis.nl
```

## Den Haag seed run

This mode uses the public Den Haag organization listings on ZorgkaartNederland as a seed source, extracts provider website links from organization detail pages, then scrapes those provider websites into CSV.

```powershell
python -m vangrondwelle.cli --discover-den-haag --format csv --output output\den-haag-zorgbedrijven.csv
```

Use `--workers` to control how many provider websites are scraped in parallel during the dataset run:

```powershell
python -m vangrondwelle.cli --discover-den-haag --format csv --workers 8 --output output\den-haag-zorgbedrijven.csv
```

## Run tests

```powershell
python -m pytest
```

## Notes

- The crawler stays on the same domain and only follows a small number of contact-oriented pages.
- Extraction uses heuristics, so some sites will need future rule tuning.
- The Den Haag seed flow is based on organization entries from ZorgkaartNederland that expose an external provider website.
- Logs are emitted as JSON on stderr when `--verbose` is enabled.

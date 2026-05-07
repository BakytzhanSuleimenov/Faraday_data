# Faraday Data Extractor (Notebook)

This repository contains a Jupyter notebook for extracting and
analyzing data from the Net Zero Centre Faraday Tool dataset hosted
on the Hugging Face platform.

The notebook provides a **Polars-based workflow** to:
- Load and scan Faraday parquet files efficiently
- Explore schema and key categorical values
- Filter data by:
  - household/property type (`property_type_2`)
  - BER/energy rating (`energy_rating`)
  - tariff type (`tariff_type`)
- Decode and transform half-hourly `kwh` profiles
- Produce wide-format half-hour columns (`hh_00` to `hh_47`)
- Visualize average consumption profiles by tariff type

## Main Notebook

- `data_extractor.ipynb`

## Requirements

From `pyproject.toml`:
- Python `>=3.12`
- `polars`
- `matplotlib`

## Setup

Install dependencies using your preferred tool. If you are using `uv`:

```bash
uv sync
```

Or with `pip`:

```bash
pip install polars matplotlib
```

## Source Dataset (Hugging Face)

- Version 5: https://huggingface.co/OpenSynth/cnz-faraday-5.0

## Dataset Path

The notebook expects parquet data under:

- `Faradayv5/*.parquet`

Update this path in notebook cells if your local dataset location is different.

## Typical Usage in Notebook

The notebook defines helper functions such as:
- `extract_by_property_type(...)`
- `extract_by_energy_rating(...)`
- `extract_filtered(...)`
- `visualize_by_tariff_type(...)`

Example workflow:
1. Filter by property type and/or BER band
2. Expand half-hour energy values
3. Aggregate/compare by tariff type
4. Plot consumption profiles

## Notes

- `energy_rating` values are grouped bands (for example: `A_B_C`, `D_E`, `F_G`)
- `kwh` values are decoded into 48 half-hour intervals per profile
- Streaming collection is used in several places for large-data efficiency

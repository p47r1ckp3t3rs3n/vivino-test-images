# Vivino Test Label Dataset

This repository holds test images of wine labels for evaluating Vivino's recognition systems. Each image is optionally annotated with metadata such as expected vintage ID, OCR output, tags, and crop coordinates.

## Structure

* `/images/`                — Images used in test scenarios
* `/metadata/labels.jsonl`  — One JSON object per image, with metadata
* `/metadata/schema.md`     — Explanation of supported metadata fields
* `/metadata/scenarios/`    — Optional scenario sets for filtered testing

## Example entry (JSONL)

```json
{
  "filename": "IMG_6348.JPG",
  "expected_vintage_id": 179517703,
  "ocr_text": "Whispering Angel Rosé 2024",
  "tags": ["ocr", "reflective", "supermarket"],
  "crop": { "x": 0.21, "y": 0.34, "width": 0.51, "height": 0.3 },
  "added_by": "patrick",
  "added_at": "2025-06-13T12:00:00Z"
}
```

## Usage

Used in conjunction with [`vivino-scan-tools`](https://github.com/p47r1ckp3t3rs3n/vivino-scan-tools) for:

* Uploading test scans to API
* Validating OCR and vintage matches
* Comparing recognition performance across systems

Run tooling scripts by referencing this repo’s `labels.jsonl` file and images:

```bash
# Example:
python upload_and_fetch.py --env testing --label clip --labels-file metadata/labels.jsonl --inject-ocr --validate-vintage
```

## Ground Truth Generation

To generate the dataset automatically from internal sources:

Use `generate_groundtruth.py` from `vivino-scan-tools` with a CSV export or raw curl logs:

```bash
# From CSV only (downloads images)
python scripts/generate_groundtruth.py --csv labels.csv --out-dir vivino-test-images

# From curl logs only (metadata only)
python scripts/generate_groundtruth.py --curls curl_logs.txt --out-dir vivino-test-images

# From both
python scripts/generate_groundtruth.py --csv labels.csv --curls curl_logs.txt --out-dir vivino-test-images
```

You’ll find results in:

* `vivino-test-images/images/` → Downloaded label images
* `vivino-test-images/metadata/labels_<timestamp>.jsonl` → Generated metadata

### Supported arguments

* `--csv <path>`: Input CSV exported from DB with label verification data
* `--curls <path>`: Input .txt file with raw curl commands
* `--out-dir <path>`: Target folder for output (both metadata and images)
* `--added-by <name>`: Tag entries with creator name (default: `patrick`)

This allows reproducible validation and evaluation of label scan performance across builds and backends.

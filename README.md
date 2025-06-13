# Vivino Test Label Dataset

This repository holds test images of wine labels for evaluating Vivino's recognition systems. Each image is optionally annotated with optional metadata, such as expected vintage ID, OCR output, tags, and crop coordinates.

## Structure

- `/images/`  Images used in test scenarios
- `/metadata/labels.jsonl`  One JSON object per image, with metadata
- `/metadata/schema.md`  Explanation of supported metadata fields
- `/metadata/scenarios/`  Optional scenario sets for filtered testing

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

## Usage

Used in conjunction with [`vivino-scan-tools`](https://github.com/p47r1ckp3t3rs3n/vivino-scan-tools) for:

- Uploading test scans to API
- Validating OCR and vintage matches
- Comparing recognition performance across systems

Run tooling scripts by referencing this repo’s `labels.jsonl` file and images:

```bash
# Example:
python upload_and_fetch.py --env testing --label clip

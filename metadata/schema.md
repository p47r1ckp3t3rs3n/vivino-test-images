## Metadata Schema

Each line in `labels.jsonl` is a standalone JSON object describing one wine label image and its metadata. This metadata supports testing and validation of Vivino's scan recognition systems.

### ✅ Required Fields

| Field      | Type     | Description                          |
|------------|----------|--------------------------------------|
| `filename` | string   | Image filename stored under `/images/` |
| `added_by` | string   | Identifier of the person adding the entry |
| `added_at` | string (ISO 8601) | Timestamp of when the entry was added |

### 🟡 Optional Fields

| Field                 | Type            | Description                                                                 |
|----------------------|-----------------|-----------------------------------------------------------------------------|
| `expected_vintage_id`| integer         | Ground truth vintage ID that the scan should match                          |
| `ocr_text`           | string          | Expected text extracted from the label (simulates OCR injection)           |
| `tags`               | array of string | Labels such as `ocr`, `verified`, `reflective`, `supermarket`, etc.        |
| `crop`               | object          | Normalized crop coordinates: `{ "x": 0.1, "y": 0.2, "width": 0.5, "height": 0.5 }` |
| `source`             | string          | Where the data came from: `label_scan_verifications`, `curl_test`, etc.    |
| `notes`              | string          | Free text notes, e.g., original verification ID, upload context             |

### 🏷 Example

```json
{
  "filename": "9JUdvgJ9RM6pYcVmaIff8g.jpg",
  "expected_vintage_id": 179517703,
  "ocr_text": "Whispering Angel Rosé 2024",
  "tags": ["verified", "ocr"],
  "crop": { "x": 0.21, "y": 0.34, "width": 0.51, "height": 0.3 },
  "added_by": "patrick",
  "added_at": "2025-06-13T12:00:00Z",
  "source": "label_scan_verifications",
  "notes": "verification_id: 123456"
}
```

### 🔍 Tag Examples

| Tag            | Meaning                                                      |
|----------------|--------------------------------------------------------------|
| `ocr`          | Entry includes expected OCR text for injection               |
| `requires_crop`| Entry defines a crop box and expects cropping to be applied  |
| `verified`     | Manually verified as accurate ground truth                   |
| `supermarket`  | Taken in a supermarket-like scenario (e.g. lighting, shelf)  |
| `reflective`   | Label has reflections or glare in the image                  |


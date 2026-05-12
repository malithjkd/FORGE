# FAIR Metadata Template (Dublin Core + Domain Extensions)

> **Usage:** Copy this template and fill in the values for every new dataset directory.  
> **Standard:** Dublin Core Metadata Element Set (ISO 15836) + domain-specific extensions  
> **See also:** [SOP-007-FAIR-data-compliance.md](../sops/SOP-007-FAIR-data-compliance.md)

---

## metadata.json Template

```json
{
  "dc:title": "[Descriptive title — e.g., 'Gantry G01 Wear Level 3 — Speed Sweep Test, Run 01']",
  "dc:creator": "[Researcher name]",
  "dc:date": "[YYYY-MM-DD]",
  "dc:description": "[What was collected, how, when, and why. 2-3 sentences.]",
  "dc:subject": ["[keyword1]", "[keyword2]", "[keyword3]"],
  "dc:format": "[HDF5 / CSV / Parquet]",
  "dc:rights": "CC-BY-4.0",
  "dc:identifier": "[DOI from Zenodo or internal ID — e.g., 'https://doi.org/10.5281/zenodo.XXXXXXX']",
  "dc:publisher": "[Organisation — e.g., 'PBA Systems']",
  "dc:contributor": ["[Additional contributor names]"],
  "dc:language": "en",
  "dc:type": "Dataset",
  "dc:source": "[Related experiment — e.g., 'EXP-003']",
  "dc:relation": "[Related datasets or publications]",
  "dc:coverage": "[Temporal or spatial coverage — e.g., '2026-Q2']",

  "equipment": {
    "gantry_model": "[Model name]",
    "daq_model": "[DAQ model]",
    "sensor_models": ["[Sensor 1]", "[Sensor 2]"],
    "calibration_date": "[YYYY-MM-DD]"
  },
  "acquisition": {
    "sampling_rate_hz": 10000,
    "duration_s": 120,
    "channels": ["[channel1]", "[channel2]"],
    "hardware_trigger": true
  },
  "wear_state": {
    "level": 0,
    "description": "[Description of wear condition]",
    "cumulative_travel_km": 0,
    "visual_inspection": "[Notes from visual inspection]"
  },
  "test_condition": {
    "speed_profile": "[e.g., 'constant_200mmps']",
    "load_n": 0,
    "ambient_temp_c": 22.0,
    "protocol_version": "v1.0"
  },
  "provenance": {
    "related_code_repo": "[GitHub URL]",
    "related_code_commit": "[Git commit hash]",
    "dvc_version": "[DVC version]",
    "python_version": "[Python version]",
    "processing_pipeline": "dvc repro"
  },
  "version": "1.0.0"
}
```

---

## Field Descriptions

| Field | Required | Description |
|-------|----------|-------------|
| `dc:title` | ✅ | Human-readable title describing the dataset |
| `dc:creator` | ✅ | Person who created/collected the data |
| `dc:date` | ✅ | Date of data creation (ISO 8601) |
| `dc:description` | ✅ | What the dataset contains, how it was collected |
| `dc:subject` | ✅ | Keywords for searchability |
| `dc:format` | ✅ | File format of the primary data files |
| `dc:rights` | ✅ | License under which the data is shared |
| `dc:identifier` | ✅ | Unique identifier (DOI or internal) |
| `equipment` | Recommended | Hardware used for data collection |
| `acquisition` | Recommended | Signal acquisition parameters |
| `wear_state` | Domain-specific | Condition of the gantry at time of collection |
| `test_condition` | Domain-specific | Experimental conditions |
| `provenance` | ✅ | Links to exact code and pipeline that produced/processed the data |

---

*Every dataset directory in `data/datasets/` must contain a `metadata.json` before it can be referenced in Experiment Reports.*

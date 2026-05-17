# SOP-007: FAIR Data Compliance

> **Source:** [ISO 13374 Mapping](../00_system_design/09_ISO13374_mapping.md) and [Industry Standards Reference](../00_system_design/07_indusy_standard.md)  
> **Trigger:** Any experiment that produces or modifies data  
> **Owner:** Every contributor who handles data

---

## FAIR Principles Quick Reference

| Principle | Meaning | How FORGE Implements It |
|-----------|---------|------------------------|
| **F — Findable** | Data has unique identifier, rich metadata, is indexed | Zenodo DOI, metadata.json, DVC-tracked |
| **A — Accessible** | Data retrievable via open protocol | DVC pull for team, Zenodo for public |
| **I — Interoperable** | Standard formats, vocabularies, ontologies | HDF5, Parquet/CSV, Dublin Core metadata |
| **R — Reusable** | Clear license, provenance, community standards | CC-BY-4.0, README, Git+DVC lineage |

---

## Procedures

### 1. ORCID Registration (One-time)

- [ ] Register at [orcid.org](https://orcid.org) (free, 5 minutes)
- [ ] Add affiliation and current project
- [ ] Share ORCID with Research Lead for team records

### 2. Data Storage Policy

> **Default: All data stays on local infrastructure.** Zenodo is used **only** when a dataset must accompany a peer-reviewed publication.

**Local storage (default):**
- Primary: Local server (DVC remote backend)
- Backup: Secondary server or NAS (3-2-1 backup rule: 3 copies, 2 media types, 1 offsite)
- Access: Controlled via DVC remote credentials

**Zenodo (publication-only):**
- [ ] Used only when a peer-reviewed journal/conference requires a public dataset DOI
- [ ] Requires Research Lead IP clearance before upload
- [ ] Create account at [zenodo.org](https://zenodo.org) when needed
- [ ] Strip any proprietary information before upload
- [ ] Use the minimum dataset required for reproducibility

### 3. Dataset Metadata (Every dataset)

For every new dataset directory, create a `metadata.json` using the template at [`data/METADATA_TEMPLATE.md`](../data/METADATA_TEMPLATE.md).

**Minimum required fields:**

```json
{
  "dc:title": "[Descriptive title]",
  "dc:creator": "[Researcher name]",
  "dc:date": "[YYYY-MM-DD]",
  "dc:description": "[What, how, when, why]",
  "dc:subject": ["[keyword1]", "[keyword2]"],
  "dc:format": "[HDF5 / CSV / Parquet]",
  "dc:rights": "CC-BY-4.0",
  "dc:identifier": "[DOI or internal ID]"
}
```

### 4. License Declaration

- All published datasets: **CC-BY-4.0** (unless IP review requires otherwise)
- All published code: License as determined by Research Lead
- License file must exist in the root of every published repository

### 5. FAIR Compliance Checklist (Every Experiment Report)

Add to every Experiment Report that produces data:

```markdown
## FAIR Compliance Checklist
- [ ] Dataset has unique identifier (DVC hash or Zenodo DOI)
- [ ] Rich metadata (title, creator, date, description, license)
- [ ] Access method documented (DVC pull command or Zenodo URL)
- [ ] Standard format used (HDF5 / Parquet / CSV)
- [ ] Provenance statement included (Git commit, DVC version, pipeline)
- [ ] License declared
- [ ] Contact info for reuse questions
```

---

## Quick Reference

```
New dataset? → Create metadata.json → DVC add → DVC push → Update data/README.md
Publishing?  → Zenodo upload → Get DOI → Add to metadata.json → Update FAIR checklist
```

---

*Review this SOP quarterly. Update when Zenodo, DVC, or university data governance requirements change.*

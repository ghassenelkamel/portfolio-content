# portfolio-content

Single source of truth for dynamic portfolio pages.

This repository is consumed by the portfolio backend via raw GitHub URLs:

- `content/about.json`
- `content/about.fr.json`
- `content/skills.json`
- `content/skills.fr.json`
- `content/experience.json`
- `content/experience.fr.json`
- `content/contact.json`
- `content/contact.fr.json`
- `assets/*`

All files are validated in CI against JSON Schema before merge.

## Editing Workflow

1. Update one or more files in `content/`.
2. Open a pull request.
3. Ensure `validate-content` GitHub Action passes.
4. Merge to `main`.
5. Portfolio backend fetches the new version automatically.

## Rules

- Keep `schemaVersion` equal to `1`.
- Keep `updatedAt` in UTC RFC3339 format (example: `2026-04-26T10:00:00Z`).
- Never remove required fields.
- Keep IDs stable once published (`skills.items[].id`, `experience.items[].id`).
- For experience images, use either:
  - repo asset paths (example: `assets/spade-integrity.svg`), or
  - full HTTPS URLs.
- Keep EN files as defaults (`*.json`) and FR files with `.fr.json` suffix.

## Local Validation (optional)

```bash
npm install -g ajv-cli ajv-formats
ajv validate --spec=draft2020 -c ajv-formats -s schemas/about.schema.json -d content/about.json
ajv validate --spec=draft2020 -c ajv-formats -s schemas/about.schema.json -d content/about.fr.json
ajv validate --spec=draft2020 -c ajv-formats -s schemas/skills.schema.json -d content/skills.json
ajv validate --spec=draft2020 -c ajv-formats -s schemas/skills.schema.json -d content/skills.fr.json
ajv validate --spec=draft2020 -c ajv-formats -s schemas/experience.schema.json -d content/experience.json
ajv validate --spec=draft2020 -c ajv-formats -s schemas/experience.schema.json -d content/experience.fr.json
ajv validate --spec=draft2020 -c ajv-formats -s schemas/contact.schema.json -d content/contact.json
ajv validate --spec=draft2020 -c ajv-formats -s schemas/contact.schema.json -d content/contact.fr.json
```

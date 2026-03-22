# Bowtie Risk Schema

An open JSON Schema for structured risk assessments using the [Bowtie methodology](https://en.wikipedia.org/wiki/Bowtie_model).

## What's a Bowtie?

The Bowtie model is a widely used risk assessment method in safety-critical industries. It maps out:

```
                    ┌─────────────┐
   Threats ────────►│  Top Event  │────────► Consequences
   (causes)         │  (hazard    │          (effects)
                    │  realised)  │
                    └─────────────┘
       ▲                                        ▲
       │                                        │
  Preventive                               Mitigative
  Barriers                                 Barriers
  (stop it                                 (reduce the
  happening)                               impact)
```

## Schema

**[`schema/bowtie-risk-table.schema.json`](schema/bowtie-risk-table.schema.json)** — JSON Schema (2020-12) defining:

| Component | Description |
|-----------|-------------|
| **Hazard** | Source of potential harm, with a top event, severity, and likelihood ratings |
| **Threat** | A cause that could trigger the top event |
| **Consequence** | An outcome that results from the top event |
| **Barrier** | A control that either prevents the top event (preventive) or reduces its impact (mitigative) |

### Hierarchy

```
RiskTable
└── Hazard (severity, likelihood, top event)
    ├── Threat
    │   └── Barrier (preventive, with effectiveness rating)
    └── Consequence
        └── Barrier (mitigative, with effectiveness rating)
```

## Examples

Real-world risk assessments across different industries:

| Example | Industry | Hazards |
|---------|----------|---------|
| [Bridge Construction](examples/bridge-construction.json) | Civil engineering | Structural collapse during demolition, deep piling near infrastructure |
| [Offshore Oil & Gas](examples/offshore-oil-gas.json) | Energy | Hydrocarbon release, dropped objects from crane operations |
| [Chemical Manufacturing](examples/chemical-manufacturing.json) | Process safety | Runaway exothermic reaction |

## Usage

Validate a risk assessment against the schema:

```bash
# Using ajv-cli
npx ajv validate -s schema/bowtie-risk-table.schema.json -d your-assessment.json

# Using Python jsonschema
python -c "
import json, jsonschema
schema = json.load(open('schema/bowtie-risk-table.schema.json'))
data = json.load(open('your-assessment.json'))
jsonschema.validate(data, schema)
print('Valid')
"
```

## About

This schema is maintained by [ArmsAI](https://armsai.net) — a platform that generates Bowtie risk assessments automatically from project documents. The schema is open and free to use in any project.

## License

MIT

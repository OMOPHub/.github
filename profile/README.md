# OMOPHub

**OMOP Vocabulary API - Query ATHENA Vocabularies Without a Database**

[![Website](https://img.shields.io/badge/Website-omophub.com-blue)](https://omophub.com)
[![Documentation](https://img.shields.io/badge/Docs-docs.omophub.com-green)](https://docs.omophub.com)
[![Status](https://img.shields.io/badge/Status-Operational-brightgreen)](https://omophub.com/status)

OMOPHub provides instant REST API access to OHDSI ATHENA standardized vocabularies - SNOMED CT, ICD-10, RxNorm, LOINC, and 100+ medical terminologies. Search concepts, build mappings, and automate ETL pipelines without setting up a local database.

---

## Why OMOPHub?

Working with OMOP vocabularies traditionally requires downloading multi-gigabyte ATHENA files and maintaining a PostgreSQL database. **OMOPHub eliminates this overhead:**

| Traditional Approach | With OMOPHub |
|---------------------|--------------|
| Download 5GB+ vocabulary files | Install SDK, start coding |
| Set up & maintain PostgreSQL | Simple REST API calls |
| Manual updates | Always current data |

**Perfect for:** ETL development, concept set building, phenotype definitions, AI/LLM integration, and any workflow requiring vocabulary access without infrastructure.

---

## Quick Start

**Python:**
```python
import omophub

# Initialize client (uses OMOPHUB_API_KEY env var)
client = omophub.OMOPHub()

# Search across vocabularies
results = client.search.basic("diabetes mellitus", vocabulary_ids=["SNOMED", "ICD10CM"], standard_concept="S", page_size=10)

# Get concept with relationships
concept = client.concepts.get(201826)  # Type 2 diabetes mellitus

# Map SNOMED concept to ICD-10-CM
mappings = client.mappings.get(201826, target_vocabulary="ICD10CM")
```

**R:**
```r
library(omophub)

# Initialize client (uses OMOPHUB_API_KEY env var)
client <- OMOPHubClient$new()

# Search across vocabularies
results <- client$search$basic("diabetes mellitus", vocabulary_ids = c("SNOMED", "ICD10CM"), standard_concept = "S", page_size = 10)

# Map source codes to standard concepts
mappings <- client$mappings$get(201826, target_vocabulary = "ICD10CM")
```

**AI Agents (MCP):**

Give Claude, Cursor, or any MCP-compatible AI agent direct access to OMOP vocabularies:

```json
{
  "mcpServers": {
    "omophub": {
      "command": "npx",
      "args": ["-y", "@omophub/omophub-mcp"],
      "env": {
        "OMOPHUB_API_KEY": "oh_your_key_here"
      }
    }
  }
}
```

Then just ask your AI agent:
> *"Map ICD-10 code E11.9 to SNOMED"*
> *"Build a concept set for Type 2 diabetes including all descendants"*
> *"Find concepts related to heart attack"* (semantic search)
> *"Give me everything about SNOMED concept 201826"* (explore)

**[Get your API key →](https://dashboard.omophub.com/register)**

---

## Official SDKs

| SDK | Package | Repository |
|-----|---------|------------|
| **Python** | [![PyPI](https://img.shields.io/pypi/v/omophub)](https://pypi.org/project/omophub/) | [omophub-python](https://github.com/OMOPHub/omophub-python) |
| **R** | [![CRAN](https://img.shields.io/cran/v/omophub)](https://cran.r-project.org/package=omophub) | [omophub-R](https://github.com/OMOPHub/omophub-R) |
| **MCP Server** | [![npm](https://img.shields.io/npm/v/@omophub/omophub-mcp)](https://www.npmjs.com/package/@omophub/omophub-mcp) | [omophub-mcp](https://github.com/OMOPHub/omophub-mcp) |

---

## MCP Server - OMOP Vocabularies for AI Agents

The OMOPHub MCP Server connects Claude, Cursor, VS Code, and any MCP-compatible AI client directly to the full OHDSI vocabulary. No SQL. No database. Just ask.

```
You: "Map ICD-10 code E11.9 to SNOMED"

Claude: Found it - E11.9 (Type 2 diabetes mellitus without complications)
        maps to SNOMED concept 201826 via standard 'Maps to' relationship.
```

### What your AI agent can do

| Tool | What it does |
|------|-------------|
| `search_concepts` | Search for medical concepts by name across all vocabularies |
| `semantic_search` | Natural language search with neural embeddings - "heart attack" finds "Myocardial infarction" |
| `get_concept` | Get full details about any OMOP concept by ID |
| `get_concept_by_code` | Look up a concept from a source code (e.g., ICD-10 `E11.9`) |
| `explore_concept` | Get concept details, hierarchy, and cross-vocabulary mappings in one call |
| `find_similar_concepts` | Find related concepts using semantic, lexical, or hybrid similarity |
| `map_concept` | Map between ICD-10, SNOMED, RxNorm, LOINC, and 100+ vocabularies |
| `get_hierarchy` | Navigate ancestors and descendants for phenotype definitions |
| `list_vocabularies` | Browse the full vocabulary catalog with statistics |

### Install

```bash
# Claude Desktop / Cursor / VS Code - add to your MCP config:
npx -y @omophub/omophub-mcp

# Docker
docker run -e OMOPHUB_API_KEY=oh_your_key_here -p 3100:3100 omophub/omophub-mcp
```

Full setup instructions for Claude Desktop, Cursor, VS Code, and Docker: **[omophub-mcp →](https://github.com/OMOPHub/omophub-mcp)**

---

## Supported Vocabularies

Access all major medical terminologies synced with official ATHENA releases:

**Clinical:** SNOMED CT, ICD-10-CM, ICD-10-PCS, ICD-9-CM, Read Codes  
**Drugs:** RxNorm, RxNorm Extension, NDC, ATC, dm+d  
**Labs:** LOINC  
**Procedures:** HCPCS, ICD-10-PCS  
**Other:** MeSH, UCUM, Gender, Race, and 90+ more

> **Note:** Licensed vocabularies (CPT, MedDRA) are not available due to license restrictions.

**[View versions supported →](https://docs.omophub.com/vocabulary-versions)**

---

## Key Features

### API Capabilities
- **Concept Search** - Full-text search with filters by vocabulary, domain, concept class
- **Semantic Search** - Natural language queries using neural embeddings (e.g., "high blood sugar" finds "Hyperglycemia")
- **Similar Concepts** - Find related concepts by semantic, lexical, or hybrid similarity
- **Hierarchy Navigation** - Traverse ancestors, descendants, and relationships
- **Cross-Vocabulary Mappings** - Map between ICD-10, SNOMED, RxNorm, and more
- **Batch Operations** - Process thousands of concepts in single requests (lexical and semantic)
- **PHOEBE Support** - Recommended concept sets for phenotyping

### Performance & Reliability
- **< 50ms response time** for most queries
- **99.9% uptime** with global edge distribution
- **Release sync** with ATHENA vocabulary releases

### Healthcare-Grade Security
- **HIPAA & GDPR compliant** architecture
- **End-to-end encryption** for all API traffic
- **Immutable audit trails** with 7-year retention
- **SOC 2 Type II** controls

---

## Use Cases

- **ETL Development** - Look up concepts and validate mappings without database access
- **Phenotype Building** - Explore hierarchies and build concept sets programmatically
- **Clinical Research** - Query vocabularies for cohort definitions
- **AI/LLM Integration** - Ground medical AI models with structured vocabulary data; connect via MCP for agent-native access
- **Data Quality** - Validate codes and check standard concept mappings

---

## Independence & Infrastructure

OMOPHub is an **independent service** - we are not affiliated with OHDSI or ATHENA. We operate on dedicated infrastructure, separate from the official ATHENA vocabulary download service.

While we use the same publicly available OHDSI vocabulary data, OMOPHub is a third-party API built to provide convenient programmatic access without the overhead of local database management.

---

## Is it free?

OMOPHub offers a free plan with 3,000 API calls per month and full API access.

---

## Resources

| Resource | Link |
|----------|------|
| **Documentation** | [docs.omophub.com](https://docs.omophub.com) |
| **Quick Start Guide** | [Getting Started](https://docs.omophub.com/quickstart) |
| **API Reference** | [API Docs](https://docs.omophub.com/api-reference) |
| **Concept Lookup Tool** | [Online Tool](https://omophub.com/tools/concept-lookup) |

---

## Support

- **Issues & Bugs:** Open an issue in the relevant SDK repository
- **General Questions and Requests:** [Contact Us](https://omophub.com/contact)

---

## Contributing

We welcome contributions to our open-source SDKs:

1. Fork the repository
2. Create a feature branch
3. Submit a pull request

See individual SDK repositories for contribution guidelines.

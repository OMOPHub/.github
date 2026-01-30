# OMOPHub

**OMOP Vocabulary API — Query ATHENA Vocabularies Without a Database**

[![Website](https://img.shields.io/badge/Website-omophub.com-blue)](https://omophub.com)
[![Documentation](https://img.shields.io/badge/Docs-docs.omophub.com-green)](https://docs.omophub.com)
[![Status](https://img.shields.io/badge/Status-Operational-brightgreen)](https://omophub.com/status)

OMOPHub provides instant REST API access to OHDSI ATHENA standardized vocabularies — SNOMED CT, ICD-10, RxNorm, LOINC, and 100+ medical terminologies. Search concepts, build mappings, and automate ETL pipelines without setting up a local database.

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
results = client.search.basic("diabetes mellitus", vocabulary_ids=["SNOMED", "ICD10CM"])

# Get concept with relationships
concept = client.concepts.get(201826)  # Type 2 diabetes mellitus
```

**R:**
```r
library(omophub)

# Initialize client (uses OMOPHUB_API_KEY env var)
client <- OMOPHubClient$new()

# Map source codes to standard concepts
mappings <- client$mappings$get(201826, target_vocabulary = "ICD10CM")
```

**[Get your API key →](https://dashboard.omophub.com/register)**

---

## Official SDKs

| SDK | Package | Repository |
|-----|---------|------------|
| **Python** | [![PyPI](https://img.shields.io/pypi/v/omophub)](https://pypi.org/project/omophub/) | [omophub-python](https://github.com/OMOPHub/omophub-python) |
| **R** | [![CRAN](https://img.shields.io/cran/v/omophub)](https://cran.r-project.org/package=omophub) | [omophub-R](https://github.com/OMOPHub/omophub-R) |

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
- **Concept Search** — Full-text search with filters by vocabulary, domain, concept class
- **Hierarchy Navigation** — Traverse ancestors, descendants, and relationships
- **Cross-Vocabulary Mappings** — Map between ICD-10, SNOMED, RxNorm, and more
- **Batch Operations** — Process thousands of concepts in single requests
- **PHOEBE Support** — Recommended concept sets for phenotyping

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

- **ETL Development** — Look up concepts and validate mappings without database access
- **Phenotype Building** — Explore hierarchies and build concept sets programmatically
- **Clinical Research** — Query vocabularies for cohort definitions
- **AI/LLM Integration** — Ground medical AI models with structured vocabulary data
- **Data Quality** — Validate codes and check standard concept mappings

---

## Independence & Infrastructure

OMOPHub is an **independent service** — we are not affiliated with OHDSI or ATHENA. We operate on dedicated infrastructure, separate from the official ATHENA vocabulary download service.

While we use the same publicly available OHDSI vocabulary data, OMOPHub is a third-party API built to provide convenient programmatic access without the overhead of local database management.

---

## Is it free?

OMOPHub offers a free plan with 5,000 API calls per month and full API access.

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
- **General Questions:** [Contact Us](https://omophub.com/contact)
- **Enterprise Support:** support@omophub.com

---

## Contributing

We welcome contributions to our open-source SDKs:

1. Fork the repository
2. Create a feature branch
3. Submit a pull request

See individual SDK repositories for contribution guidelines.


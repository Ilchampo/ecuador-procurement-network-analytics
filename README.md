# Ecuador Public Procurement Network Analytics

Reproducible research project for identifying concentration, recurrent relationships, and structural patterns in Ecuador's 2025 Electronic Reverse Auction procedures. The study combines open contracting data, descriptive statistics, concentration measures, and a Buyer-Supplier network implemented in Neo4j.

The model is a screening and review-prioritization tool. Its signals are descriptive and do not constitute evidence of fraud, collusion, or legal wrongdoing.

## Research question

How can network analytics complement conventional tabular analysis to identify Buyer-Supplier relationships that merit closer technical and documentary review?

## Main findings

- The analysis covers 18,326 procedures, 79,425 bidder-participation records, and 15,718 awards.
- The final network contains 7,664 actors and 13,493 Buyer-Supplier relationships.
- 52.8% of procedures had no more than three bidders.
- The largest connected component contains 92.6% of all actors.
- Louvain and Leiden produced similar community structures, with modularity near 0.69.
- Combining five transparent signals reduced 13,493 relationships to 71 with at least three signals and 3 with four signals.

## Repository structure

```text
.
├── data/
│   ├── raw/2025/          # Original monthly SERCOP OCDS JSON packages
│   ├── processed/         # Analysis-ready procedures, participation, and awards
│   └── neo4j/             # Generated graph-import tables and network metrics
├── docs/                  # English public report and supporting documentation
├── notebooks/             # Numbered analytical workflow
├── outputs/
│   ├── figures/           # Publication-ready figures
│   └── tables/            # Generated analytical tables
├── src/                   # Shared project utilities
└── requirements.txt       # Reproducible Python environment
```

## Analytical workflow

Run the notebooks from the `notebooks/` directory in numerical order:

1. `01_inspect_ocds_json.ipynb` inspects the source packages and OCDS fields.
2. `02_clean_and_integrate_data.ipynb` creates the processed datasets.
3. `03_define_analytical_variables.ipynb` documents and derives analytical variables.
4. `04_explore_and_visualize_data.ipynb` creates descriptive figures.
5. `05_build_neo4j_network.ipynb` creates graph-import tables, loads Neo4j, and exports network metrics.
6. `06_integrate_screening_signals.ipynb` combines the five screening signals.
7. `07_document_cypher_queries.ipynb` records the principal Cypher queries.
8. `08_validate_buyer_supplier_signals.ipynb` performs read-only signal checks in Neo4j Aura.

Notebook 5 requires a Neo4j instance. Copy `.env.example` to `.env` and provide local credentials; never commit `.env`.

## Setup

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
jupyter lab
```

The raw files are retained without content changes. Processed files and figures can be regenerated from the numbered notebooks.

## Data provenance

The source is the open contracting data published by Ecuador's National Public Procurement Service (SERCOP). The study uses procedures initiated from January through December 2025 and links releases through the Open Contracting ID (`ocid`). Consult SERCOP's terms and the repository license before redistribution or reuse.

## Citation

Use the metadata in [`CITATION.cff`](CITATION.cff). The full English public report is available in [`docs/`](docs/).

## Authors

- Diana Nathaly Altamirano Diaz
- Juan Pablo Beltran Flores

MBA in Business Intelligence and Data Analytics, 2026.

# Social Network Analysis: The Epstein Documents Network

![R](https://img.shields.io/badge/-R-276DC3?style=flat-square&logo=r&logoColor=white) ![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)

A three-part network analysis of the actors named in the released "Epstein Files" documents: descriptive statistics and community detection, link prediction, and epidemic spreading (diffusion) models.

## Overview

This project explores the social network of entities named in the U.S. Department of Justice's released Epstein documents, using structured data extracted via AI by [Max Andrews' Epstein Document Explorer](https://github.com/maxandrews/Epstein-doc-explorer). The network is built from RDF triples (actor, action, target), for example "Jeffrey Epstein sent email to Ghislaine Maxwell", with edges weighted by the number of co-occurrences.

The analysis is organized in three parts, each building on the previous one:

| File | Topic | Collaborators |
|---|---|---|
| `HW1_network_descriptives.qmd` | Descriptive statistics, degree distribution, assortativity, community detection, clustering coefficient significance testing, robustness check | Paloma Navarro |
| `HW2_link_prediction.qmd` | Link prediction via proximity heuristics (Jaccard, Adamic-Adar, preferential attachment) and logistic regression with cross-validation | Paloma Navarro, Clare McGarvey |
| `HW3_epidemic_spreading.Rmd` | SIR epidemic spreading models, epidemic threshold, targeted vs. random seeding/vaccination, predictive model for time-to-infection | Paloma Navarro, Clare McGarvey, Anita Di Gennaro |

## Key Findings

- **Structure:** the network is heavily hub-dominated. Five actors, Jeffrey Epstein, an unidentified redacted entity, Donald Trump, Alan Dershowitz, and a second redacted entity, account for a disproportionate share of connections
- **Degree assortativity** is negative (-0.24): high-degree hubs tend to connect to low-degree nodes rather than to each other, consistent with a small set of central brokers linking otherwise disconnected subgroups
- **Community structure** is real but only moderate (Louvain modularity approx. 0.30), the dominance of hubs softens boundaries between communities
- **Link prediction:** a logistic regression using local similarity heuristics can meaningfully distinguish real from non-existent links; classical heuristics like Adamic-Adar and preferential attachment carry a strong signal
- **Diffusion:** targeting high-centrality nodes for suppression is far more effective at containing spread than random suppression (roughly 40% fewer total infections), confirming that a small set of central actors could control the flow of information through the network if they coordinated

## Data Source

Data is not stored in this repository. All scripts download the SQLite database directly from Max Andrews' [Epstein-doc-explorer](https://github.com/maxandrews/Epstein-doc-explorer) repository at runtime.

## Repository Structure

```
social-network-analysis/
├── HW1_network_descriptives.qmd
├── HW2_link_prediction.qmd
├── HW3_epidemic_spreading.Rmd
├── README.md
├── LICENSE
└── .gitignore
```

## Requirements

`R` (>= 4.2) with: `igraph`, `ggraph`, `ggplot2`, `RSQLite`, `dplyr`, `kableExtra`, `boot`, `caret`

```r
install.packages(c("igraph", "ggraph", "ggplot2", "RSQLite", "dplyr", "kableExtra", "boot", "caret"))
```

## How to Run

```bash
git clone https://github.com/palomanavarro22/social-network-analysis.git
cd social-network-analysis
```

Open any of the three files in RStudio and render (each downloads the required data automatically on first run).

## Limitations & Future Research

Roughly 5% of nodes are composite "unknown person" labels representing multiple distinct individuals collapsed by the AI extraction pipeline, inflating their apparent centrality. A robustness check with these nodes removed is included in HW1 and confirms the qualitative conclusions hold. Link prediction could be extended with graph-aware embeddings (node2vec, GNNs), and the epidemic models assume a simple SIR process rather than a more realistic information-diffusion mechanism.

## Author

**Paloma Navarro**
MSc in Computational Social Science, UC3M
[LinkedIn](https://www.linkedin.com/in/paloma-navarro-3b7927280/)

With Clare McGarvey (HW2, HW3) and Anita Di Gennaro (HW3).

## Citation

If you use this analysis, please cite:

```
Navarro, P., McGarvey, C. & Di Gennaro, A. (2026). Social Network Analysis: The Epstein Documents Network.
GitHub repository: https://github.com/palomanavarro22/social-network-analysis
```

Underlying data: Andrews, M. (2025). Epstein-doc-explorer: a graph explorer of the Epstein emails [Dataset]. GitHub. https://github.com/maxandrews/Epstein-doc-explorer

## License

This project is licensed under the MIT License, see the [LICENSE](LICENSE) file for details.

---

*Coursework for the Social Network Analysis course, MSc in Computational Social Science, UC3M.*

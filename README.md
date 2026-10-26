# Codebase Intelligence Engine (CBI)

Read-only analyzer for Python repositories: AST parsing, dependency graph, cyclomatic complexity, code smells, Git-history mining (churn, contributors, co-change) and ranked, explainable hotspots. It never executes the analyzed code.

**Live demo:** `https://<your-username>.github.io/<repo-name>/` (demo data = analysis of [psf/requests](https://github.com/psf/requests))

## Run it on your own repo
```bash
python -m cbi /path/to/python/repo -o docs/report.json   # Python 3.10+, no dependencies; Git optional
python -m http.server -d docs                            # open http://localhost:8000
```
On the hosted site, click **Browse** on *Repository Analysis* and pick your `report.json`.

## Publish on GitHub Pages
Push the repo, then **Settings → Pages → Deploy from branch → `main` / `/docs`**.

## How it works
| Stage | Where |
|---|---|
| Ingestion (path validation, ignore rules) | `cbi/analyzer.py` `analyze()` |
| Static analysis (AST, LOC, complexity, smells, imports) | `parse()` |
| Git mining (`git log --name-only`) | `git()` |
| Insight engine: hotspot score = 0.35 complexity + 0.30 churn + 0.20 smells + 0.15 fan-in | `analyze()` |
| Reports & views | `docs/index.html` |

Course project: 21CSC203P-APP, SRM Institute of Science and Technology, Ramapuram.

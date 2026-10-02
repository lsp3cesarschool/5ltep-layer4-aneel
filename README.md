# 5LTEP-L4 · ANEEL instance (control experiment)

[![Tests](https://github.com/lsp3cesarschool/5ltep-layer4-aneel/actions/workflows/tests.yml/badge.svg)](https://github.com/lsp3cesarschool/5ltep-layer4-aneel/actions/workflows/tests.yml) [![Layer 4](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Flsp3cesarschool%2F5ltep-layer4-aneel%2Fmain%2Fdocs%2Fdata%2Fstatus.json)](https://github.com/lsp3cesarschool/5ltep-layer4-aneel/actions/workflows/monitor.yml) [![Cross-check](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Flsp3cesarschool%2F5ltep-layer4-aneel%2Fmain%2Fdocs%2Fdata%2Fstatus-cross-check.json)](https://github.com/lsp3cesarschool/5ltep-layer4-aneel/actions/workflows/cross_check.yml) [![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

**English** · [Português](LEIAME.md)

**5L-TEP Layer 4 (observability and provenance) applied to the open data portal of ANEEL, Brazil's electricity regulator:
another instance of [5ltep-layer4](https://github.com/lsp3cesarschool/5ltep-layer4), set up by the author as a control case for the IBAMA
study.**

| Resource | What you find there |
|---|---|
| 📊 **Dashboard** | [lsp3cesarschool.github.io/5ltep-layer4-aneel](https://lsp3cesarschool.github.io/5ltep-layer4-aneel/?lang=en): changes per month, where the files are, latest changes, monitoring health, every dataset |
| 📄 **Change log** | [`changes.md`](changes.md): every detected change in plain words, rebuilt each cycle |
| 🔗 **Provenance records** | [`provenance_logs/`](provenance_logs/): one append-only W3C PROV-DM (JSON-LD) chain per dataset |
| 🏛️ **Main instance** | [5ltep-layer4](https://github.com/lsp3cesarschool/5ltep-layer4): IBAMA, and the full documentation |
| 🔁 **Other control** | [5ltep-layer4-recife](https://github.com/lsp3cesarschool/5ltep-layer4-recife): the Recife portal |

> **Status: research demonstration.** This repository is not operated by, affiliated with or endorsed by ANEEL; it only reads ANEEL's open data. It shows that the toolkit can be reused on
> another portal, and it does not assume that the publisher will review its results or adopt it.
> Alerts reach the maintainer of this repository, not the publisher.

## Use case in one paragraph

ANEEL publishes on its CKAN portal the data of the electricity sector it regulates: tariffs,
generation, distribution quality indicators, infraction notices and more, many of them updated
monthly. Suppose an analyst downloads a tariff or quality dataset every month and compares the
months: if a file is replaced, moved to another server or edited without a new modification date,
the comparison silently mixes two versions. This instance reads the metadata of every ANEEL
dataset every six hours and records each change as a W3C PROV-DM entity linked to the version
before it, so the analyst can see when a dataset changed, how, and whether the change was dated.

## Why a control experiment

The Layer 4 toolkit was built and evaluated on IBAMA's portal. ANEEL is a federal regulator, in another sector
(about 70 datasets; a cycle takes well under a minute). This repository runs **the same code**, following the steps of *Monitoring another
CKAN portal* in the main README: only `portal.json` (the portal's URL) and the texts of this README
changed. Where ANEEL publishes differently from IBAMA, the difference shows up in the change
records, not in the code. Monitoring starts with a baseline: the first cycle records no change, only
the state every later cycle is compared with.

## What changed from the main instance

| File | Change |
|---|---|
| `portal.json` | `portal_url` = `https://dadosabertos.aneel.gov.br` |
| `README.md`, `LEIAME.md`, `CITATION.cff` | this text and the citation of this repository |

Everything else is the code of `5ltep-layer4` at commit `cc39c25`
([cc39c25e3705dc54952bd07402ee59727d8e1697](https://github.com/lsp3cesarschool/5ltep-layer4/commit/cc39c25e3705dc54952bd07402ee59727d8e1697)). The snapshots, provenance records,
change log and dashboard data are written here by the workflows.

## Running it, and adapting it again

The workflow *5L-TEP Layer 4 Monitoring Workflow* runs every six hours and can be started by hand
(*Actions → Run workflow*); the cross-check runs once a day. Locally:

```bash
pip install -r requirements.txt
python main.py --max-datasets 5 --dry-run
```

To point it at yet another CKAN portal, change `portal_url` in `portal.json`; see the main README.

## Reproducibility

Each provenance record carries the fingerprint of the dataset version it describes, the run that
observed it and the commit of the code that ran (`5ltep:commitSha`). The code is the upstream commit
above; everything else is committed by the workflows, so the history of this repository is the
history of the portal as observed.

## Limitations

The limitations of the main instance apply. ANEEL's portal is larger in files than in datasets: a dataset with many resources produces long change descriptions when they are all replaced at once.

## Documentation and references

The full documentation (change taxonomy, PROV-DM mapping, dual-agent model, cross-check,
configuration, evaluation and references) is in the [main repository](https://github.com/lsp3cesarschool/5ltep-layer4#readme).

## License

MIT for the code ([LICENSE](LICENSE)). Each ANEEL dataset declares its own licence on the portal; this repository stores only metadata snapshots and provenance records derived from them.

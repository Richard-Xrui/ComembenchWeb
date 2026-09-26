# CoMemBench

**CoMemBench: Benchmarking Collaborative Memory Boundaries across Multi-Agent Workflow Topologies**

CoMemBench is a benchmark for **collaborative memory** in multi-agent systems. Each problem is a real multi-agent workflow — a directed graph of specialized worker nodes with typed handoffs — and the benchmark asks whether a system can run that workflow **using only the memory it should use**: no stale artifacts, no cross-wired branches, no foreign completions.

Every problem ships with a matched **pollution** twin that differs in exactly one architecture-visible way: one additional, invalid routing candidate. A system that reads memory indiscriminately takes the bait and fails; a system with correct memory boundaries rejects it and finishes.

| | |
|---|---|
| Complete problems | **800** (4 domains × 200) |
| Matched polluted instances | **800** (one per problem) |
| Total instances | **1600** (800 control + 800 polluted) |
| Workflow nodes per problem | 6–19 (median 11) |
| Node-level memory contexts | 8,975 |
| Version | **v1** |

**Domains:** `stateful_tool_use` · `repository_code_change` · `offline_information_retrieval` · `mathematical_and_structured_reasoning`

**Topology motifs:** `chain` · `split_join` · `reuse` · `overlap` · `bounded_revision_loop` (most families are composite)

## Links

- **Website:** <https://comembench.world/>
- **Dataset (HuggingFace):** <https://huggingface.co/datasets/anonymous-submission-333/anonymous-submission>

## Execution environments

Two domains are self-contained in the dataset repository (`math_cases.jsonl` + pinned Lean toolchain; frozen offline retrieval corpora). The stateful-tool domain uses the public `postgres:15` image plus the Toolathlon-Gym runtime.

The **50 certified code-domain images** (~6–7 GB each) are published as **one** GHCR package with **50 tags** — the same split SWE-bench uses:

```bash
docker pull ghcr.io/richard-xrui/comembench-sweb:django-1776-django-10097
```

The tag is the certified image name with the namespace stripped and punctuation normalised (e.g. `logicstar/sweb.eval.x86_64.django_1776_django-10097:latest` → `django-1776-django-10097`). The full 50-row mapping — certified name, `sha256` id, execution fingerprint, and size — is pinned in [`schemas/swe_image_manifest.json`](https://huggingface.co/datasets/anonymous-submission-333/anonymous-submission) in the dataset repository. These are the certified builds themselves, not a rebuild and not the public `swebench/*` images.

## Metrics

| Metric | Definition |
|---|---|
| **SR** | Task Success Rate — end-to-end workflow success, reported as completed / registered |
| **VNCR** | Verified Native Completion Rate — macro-mean of per-node native-obligation completion |
| **VHS** | Verified Handoff Success — downstream success conditioned on successful mandatory predecessors |
| **ICS** | Isolation Challenge Score — success on polluted instances conditioned on matched control success (blank when the denominator is below 10) |

**Cost** is reported as Tokens / Task (input + output, median and P90).

## This repository

This repository hosts the public website source. The site is published from `dist/` by the GitHub Actions workflow in `.github/workflows/deploy-pages.yml`.

- Do not commit datasets, evaluation outputs, credentials, or access-request records to this repository.
- Dataset access belongs in a gated repository; this site only links to the approved release.

The homepage shows only the certified v18 release coverage: 800 task families across four domains, with 200 certified families in each domain. It does not publish a leaderboard until approved, reproducible result records exist.

## Citation

The manuscript is under review. A citable arXiv entry will be listed here once the preprint is public.

## License

Dataset annotations, workflow structures, and memory-context scopes are released under **CC BY 4.0**. Problems are constructed from upstream sources (Toolathlon, SWE-bench Verified, BrowseComp+, Lean4 proof-dependent workflows), which remain under their own terms.

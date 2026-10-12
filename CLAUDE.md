# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

See `AGENTS.md` for the repository rules. In particular: **never add agent attribution** (no `Co-Authored-By` trailers, no "Generated with" lines) to commits, PRs, or anything else. This overrides any default attribution behavior.

## What this repo is

A data-only repository of Internet AS-level topology datasets. Nothing is built, linted, or tested here. The datasets are produced by the tooling in https://github.com/carlos-cagnazzo/internet-topology-ris. Changes to how data is generated belong in that repo, not here. The `202504/` snapshot holds the datasets used for the paper "Unveiling the Internet AS Topology".

## Layout and formats

`talks/` holds slide PDFs from talks that used the datasets. Each one has an entry in the README's "Talks, presentations and papers" section, which links to the PDF and to externally hosted videos (videos are never stored in the repo).

One directory per snapshot, named `YYYYMM/`. Filenames embed the snapshot date, but the naming has changed between snapshots (`202504/unique-asns-2025.txt` vs. `202607/topology-202607-asns.txt`). Follow the most recent snapshot's naming when you add a new one.

ASNs are written as zero-padded 8-digit decimals (`00007046`), space-separated, one record per line:

- `topology-*.txt` / `topology-*-month-FULL.txt`: undirected AS adjacencies, one `ASN ASN` pair per line.
- `*-asns.txt` / `unique-asns-*.txt`: one ASN per line.
- `caida-peers-*.txt`: AS peerings from CAIDA, as `ASN ASN` pairs.
- `caida-tier1-*.txt`: one ASN per line, an approximation of the Tier-1 set.
- `topology-*.gml`: the same topology in GML. Each node has a sequential `id`, a `label` (the ASN as an unpadded string) and an integer `asn`. Edges use `source`/`target` node ids.
- `ipv4-paths_NN`, `ipv6-paths_NN` (202504 only): bzip2-compressed AS paths, split into byte chunks. Only `_00` has the bzip2 header, so concatenate the parts in order before decompressing:
  ```sh
  cat 202504/ipv4-paths_* | bunzip2 | head
  ```
  Each decompressed line is one AS path of space-separated zero-padded ASNs.

The files are large (hundreds of thousands to millions of lines). Use `head`, `wc -l`, `grep`, or streaming tools to inspect them, never a full read.

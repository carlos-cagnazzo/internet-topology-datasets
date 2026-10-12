# internet-topology-datasets

Internet AS-level topology datasets, built from public BGP data collected by [RIPE RIS](https://www.ripe.net/analyse/internet-measurements/routing-information-service-ris/) and [RouteViews](https://www.routeviews.org/) with the tooling in [internet-topology-ris](https://github.com/carlos-cagnazzo/internet-topology-ris). That repo explains how the data is collected and processed.

## Available snapshots

| Snapshot | Contents |
|----------|----------|
| [2025-04](202504/) | AS adjacencies, unique ASNs, raw IPv4/IPv6 AS paths. |
| [2026-07](202607/) | AS adjacencies (plain text and GML), ASN list, CAIDA peerings, and an approximation of the Tier-1 set. |

## Formats

- ASNs are written as zero-padded 8-digit decimals (`00007046`).
- Topology and peering files list one undirected AS adjacency per line: `ASN ASN`.
- ASN list and Tier-1 files hold one ASN per line.
- GML files encode the same topology as the text files. Each node carries an `asn` attribute.
- The 2025-04 AS path files are one bzip2 archive split into parts. Join them before decompressing:

  ```sh
  cat 202504/ipv4-paths_* | bunzip2 > ipv4-paths.txt
  ```

## Talks, presentations and papers

Work that has used these datasets:

- **El grafo de los ASNs de Internet** (*The Internet ASN graph*). Claudio Risso and Carlos Martínez, LACNIC 45 Technical Forum, 28 May 2026. [Session page](https://lacnic45.lacnic.net/es/programa/agenda/el-grafo-de-los-asns-de-internet), [slides (PDF)](talks/el-grafo-de-los-asns-de-internet-lacnic45.pdf), video in [Spanish](https://youtu.be/02ROROD3dVM) (original), [English](https://youtu.be/EBa1wEFbnKs) and [Portuguese](https://youtu.be/YXNHc5nR2CY) (interpreted).

# Gracion

Gracion is a research prototype for a zone-based, adaptive binary storage
format (`.grcn`) for structured-but-heterogeneous JSON records — data that
doesn't sit comfortably in either a relational table (rigid) or a
schemaless document store (wasteful). Instead of one generic structure
for every field, Gracion partitions each record into zones and gives each
zone the data structure best suited to its actual access pattern:
learned indexing for rarely-updated fields, a mutable index for
frequently-updated fields, specialized compression for bulk-scanned
numeric series, and key/value separation for large binary assets.

It also includes a runtime-reactive defense against poisoning attacks on
the mutable zone's learned index — detecting query-pattern degradation
and responding automatically, rather than relying only on a design-time
fix.

## Results

Measured, not estimated, methodology and code intentionally not included:

- **40-60% smaller than raw JSON** at realistic scale (thousands of
  records), improving further as record count grows.
- **A runtime-reactive defense against learned-index poisoning attacks**:
  100% detection rate, 0% false positives, full model recovery, median 20
  queries to detect an attack in progress, across 30 independent trials.
- Verified against Google Scholar, ACM Digital Library, IEEE Xplore, and
  arXiv: no prior published work combines a learned index with a
  reactive/adaptive defense of this kind.

## Notice

**This is a private project.** The source code, tests, benchmarks,
research paper, internal build logs, and referenced literature are
intentionally not included in this repository. This is a deliberate
decision, not an oversight — nothing beyond this README is meant to be
public.

## Status

Prototype stage. Not a production database, and not distributed as an
open-source project — an installable build may be published separately
in compiled form.

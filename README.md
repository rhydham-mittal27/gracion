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

In internal testing, the zone-based layout consistently stored records
more compactly than raw JSON once past a small fixed overhead at very low
record counts, with the gap widening as the dataset grows. The reactive
defense was evaluated against a real poisoning attack on the mutable
zone's learned index and reliably detected and corrected the resulting
degradation without materially affecting normal query performance. A
literature pass across the major databases in the space didn't turn up
prior work combining a learned index with this kind of runtime defense.

Full methodology, numbers, and the paper are not published here, this
section is a summary, not a claim meant to stand on its own.

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

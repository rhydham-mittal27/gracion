# Gracion

Gracion is a research prototype exploring adaptive storage for
heterogeneous structured records. It introduces a zone-based binary
format (`.grcn`) that partitions a record into specialized storage
regions, allowing different physical organizations to coexist within a
single logical record according to expected workload characteristics. It
targets data that does not fit naturally into either a rigid relational
schema or a conventional schemaless document store. Rather than one
generic structure for every field, Gracion assigns each zone a storage
structure selected according to its expected access pattern:
learned-index-based structures for rarely-updated fields, a mutable
index for frequently-updated fields, specialized compression for
bulk-scanned numeric series, and key/value separation for large binary
assets.

It also includes a runtime-reactive defense against poisoning attacks on
the mutable zone's learned index — detecting query-pattern degradation
and responding automatically, rather than relying only on a design-time
fix.

## Results

In internal testing, the zone-based layout consistently stored records
more compactly than raw JSON once past a small fixed overhead at very low
record counts, with the gap widening as the dataset grows. The reactive
defense was evaluated against a real poisoning attack on the mutable
zone's learned index and detected and corrected the resulting
degradation while maintaining comparable performance under benign
workloads. A literature survey across ACM Digital Library, IEEE Xplore,
Google Scholar, and arXiv did not identify prior work combining learned
indexes with a runtime-reactive defense of this kind. This observation is
based on the literature reviewed during the project and should not be
interpreted as proof that no such work exists.

Full methodology, numbers, and the paper are not published here, this
section is a summary, not a claim meant to stand on its own.

## Research Repository

This repository intentionally contains only a high-level description.
The implementation, benchmarks, datasets, research logs, and manuscript
are currently withheld while the work undergoes further validation and
preparation for publication.

## Status

Research prototype. Not a production database and not distributed as an
open-source project. An installable build may be published separately in
compiled form.

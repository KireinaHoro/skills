---
name: paper-chart
description: Create reproducible publication charts from measurements, with tracked data, provenance, and plotting scripts. Use for research and evaluation figures, adapting to the project's paper format and measurement contract.
---

# Paper charts

Inspect repository instructions, the paper source, existing plotting code, and
local modifications before editing. Identify the project's measurement contract,
data and script locations, figure destination, chart inventory, and build environment.
Resolve paths relative to the script's repository, not the caller's directory.
Do not assume a particular project, hardware platform, sibling paper repository,
LaTeX class, or package manager.

Reuse the project's shared plotting library. If none exists, factor common
formatting into a small reusable helper when multiple figures need it. Import
style configuration before pyplot. Derive physical dimensions and typography
from the target publication template; use its actual column width and fonts.
Default to one chart on one column. If no template is specified, make figure
geometry configurable and state the chosen dimensions.

Save fixed-canvas vector PDFs; never use `bbox_inches="tight"`, which changes
physical dimensions. Use readable axis labels with units and legends as needed.
Do not add titles, captions, footnotes, sample-count callouts, reference lines,
or other annotations unless requested. Put measurement qualifications in tracked
provenance, not inside the chart. When requested, annotate median, P99 and max
with numeric values and units; retain default line weight unless asked otherwise.

Emit an executable plotting script that bridges the actual acquisition format
to the chart: load and validate source rows, exclude explicitly marked warmup,
compute requested statistics, and render in one documented command. Do not leave
manual spreadsheet conversions or invented aggregate inputs between analysis
and plotting. Keep source observations, provenance, and plotting scripts tracked
in the project's established locations. Track acquisition commands or scripts,
revisions, hashes, units, instrumentation, failure accounting, and regeneration
instructions. Preserve small source datasets verbatim; never manufacture samples
from percentiles. CDFs use every valid measured sample, without tail clipping.

Check timestamp placement and endpoint definitions across acquisition modes
before comparing latency. Record these definitions in the data manifest. Preserve
each observation's original measurement boundary; never relabel round-trip,
one-way, host, or wire intervals as interchangeable. Missing endpoint measurements
cannot support a total or residual requiring those endpoints. Reuse historical
data only with original provenance, never as a current run. Throughput requires
successful completions divided by the recorded elapsed observation window, with
preparation time explicitly included or excluded by the workload contract; do
not infer saturation throughput from reciprocal latency. Distinguish configured
resources from observed active resources.

Maintain an active chart inventory using the project's existing format, or a
compact manifest if none exists: output figure, script, data manifest,
regeneration command, and actual paper inclusion or pending inclusion. Inspect
the paper source before claiming inclusion. Do not add inclusion or caption text
unless requested. When replacing or retiring charts, remove superseded plot
scripts, PDFs, and previews once validated replacements exist. Preserve shared
scripts used by active charts and measurement/provenance inputs. Update the
inventory in the same change; do not retain alternate stale implementations.

Use the project's reproducible environment. Validate actual PDF dimensions,
embedded fonts, plotted statistics, and visual readability. Rendering success
alone does not validate data. Keep previews and caches in ignored output
locations. Follow repository and user instructions on commits and publication;
do not commit others' edits or infer permission to push from this skill.

For missing measurements, follow the project's acquisition and preservation
workflow. Resolve workload ambiguity before acquiring dependent curves. If
measurement is blocked, preserve the runnable pipeline and explain the missing
evidence in agent context or the task response; never render placeholder points
as results. Keep durable methodology in human documentation and execution
progress in agent context.

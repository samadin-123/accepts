# Evaluation Setup

This file is outside the editable surface. It defines how results are judged. Agents cannot modify the evaluator or the scoring logic — the evaluation is the trust boundary.

Consider defining more than one evaluation criterion. Optimizing for a single number makes it easy to overfit and silently break other things. A secondary metric or sanity check helps keep the process honest.

eval_cores: 1
eval_memory_gb: 1.0
prereq_command: npm install --silent

## Setup

Install dependencies and prepare the evaluation environment:

```bash
npm install
```

This installs the `accepts` library dependencies (`mime-types`, `negotiator`) and dev dependencies needed for testing. No build step is required as this is a pure JavaScript library.

## Run command

```bash
node bench.js
```

This benchmark tests the core content negotiation functionality:
- Type negotiation with various Accept headers (JSON, HTML, XML, wildcard)
- Multiple input formats (shorthand types like 'json', full MIME types)
- Edge cases (no Accept header)
- Related methods (encodings, charsets, languages)

The benchmark executes 100,000 iterations with 6 operations each (600,000 total operations) across 5 different request scenarios to simulate realistic usage patterns.

## Output format

The benchmark must print `METRIC=<number>` to stdout.

## Metric parsing

The CLI looks for `METRIC=<number>` or `ops_per_sec=<number>` in the output.

## Ground truth

Baseline performance on the initial codebase: ~676,000 operations/second on the evaluation hardware (1 core, 1GB RAM). This represents the throughput of content negotiation operations including type/encoding/charset/language parsing and matching.

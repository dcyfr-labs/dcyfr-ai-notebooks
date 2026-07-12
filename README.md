# @dcyfr/ai-notebooks

<!-- README-META
  tlp_clearance: GREEN
  status: deprecated
  name: dcyfr-ai-notebooks
  description: Data science notebook toolkit with TypeScript tooling for computational notebooks, data pipelines, and visualization
  last_validated: 2026-07-11
-->

> **⚠️ PACKAGE DEPRECATED & NO LONGER MAINTAINED (February 27, 2026)**  
> This experimental package is deprecated on npm and is no longer actively maintained.  
> **Last published version:** v1.0.1  
> **Alternatives:**
>
> - Fork this repository if you need the functionality
> - Use [Observable](https://observablehq.com/) for JavaScript notebooks
> - Use [Jupyter](https://jupyter.org/) with TypeScript kernel for data science
> - Use [Hex](https://hex.tech/) for modern data notebooks
>
> This package is now marked `"private": true` to prevent future publication.

[![Ask DeepWiki](https://deepwiki.com/badge.svg)](https://deepwiki.com/dcyfr-labs/dcyfr-ai-notebooks)

[![TypeScript](https://img.shields.io/badge/TypeScript-6.0-blue?style=flat-square&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![CI](https://github.com/dcyfr-labs/dcyfr-ai-notebooks/actions/workflows/ci.yml/badge.svg)](https://github.com/dcyfr-labs/dcyfr-ai-notebooks/actions/workflows/ci.yml)
[![Status](https://img.shields.io/badge/Status-Deprecated-red?style=flat-square)](https://github.com/dcyfr-labs/dcyfr-ai-notebooks)
[![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)](LICENSE)

~~Data science notebook toolkit for TypeScript~~ **DEPRECATED: No longer maintained**

## About DCYFR

`@dcyfr/ai-notebooks` is maintained by **DCYFR Labs** as part of the DCYFR experimentation toolkit portfolio.

- **DCYFR** is a registered trademark of DCYFR Labs.
- Primary domain: [www.dcyfr.ai](https://www.dcyfr.ai)
- Licensing details: [LICENSE](./LICENSE)
- Security policy: [SECURITY.md](./SECURITY.md)

## Features

- **Notebook Engine** — Create, manage, and execute computational notebooks with cells, outputs, and metadata
- **Data Pipeline** — Build multi-step ETL pipelines with transforms, aggregation, joins, and validation
- **Statistics** — Descriptive statistics, correlation analysis, quantiles, and frequency counts
- **Visualization** — Chart specification builders and text-based renderers (bar charts, tables, sparklines)
- **Data Utilities** — CSV parsing, dataset operations, data validation with composable rules
- **Type-Safe** — Full TypeScript support with Zod schema validation

## Quick Start

```bash
# Clone or use as part of the DCYFR workspace
git clone https://github.com/dcyfr-labs/dcyfr-ai-notebooks
npm install
```

### Create and Execute a Notebook

```typescript
import {
  createNotebook,
  addCell,
  codeCell,
  markdownCell,
  executeNotebook,
  getExecutionSummary,
} from "@dcyfr/ai-notebooks";

// Create a notebook
let nb = createNotebook({ title: "My Analysis" });
nb = addCell(nb, markdownCell("# Hello World"));
nb = addCell(nb, codeCell("const x = 42;\nconsole.log(x);"));

// Execute
const { result } = await executeNotebook(nb);
const summary = getExecutionSummary(result);
console.log(`Completed: ${summary.completed}/${summary.total}`);
```

### Data Analysis

```typescript
import {
  createDataset,
  describe,
  sortBy,
  head,
  renderDatasetTable,
  renderStatsTable,
} from "@dcyfr/ai-notebooks";

const data = createDataset(
  [
    { name: "Alice", score: 92.5 },
    { name: "Bob", score: 88.0 },
    { name: "Charlie", score: 95.3 },
  ],
  "students",
);

// Descriptive statistics
console.log(renderStatsTable(describe(data)));

// Top performers
console.log(renderDatasetTable(head(sortBy(data, "score", false))));
```

### Data Pipelines

```typescript
import {
  createPipeline,
  filterRows,
  normalize,
  aggregate,
} from "@dcyfr/ai-notebooks";
import type { Dataset } from "@dcyfr/ai-notebooks";

const pipeline = createPipeline<Dataset>("my-pipeline")
  .step("filter", async (data) => filterRows(data, (r) => r.active === true))
  .step("normalize", async (data) => normalize(data, "score"))
  .step("aggregate", async (data) =>
    aggregate(data, "category", {
      avg_score: { column: "score", fn: "avg" },
      count: { column: "score", fn: "count" },
    }),
  );

const { result, output } = await pipeline.run(dataset);
console.log(`Status: ${result.status}, Steps: ${result.steps.length}`);
```

### Visualization

```typescript
import { barChart, renderBarChart, sparkline } from "@dcyfr/ai-notebooks";

const chart = barChart("Sales", ["Q1", "Q2", "Q3", "Q4"], [120, 150, 180, 200]);
console.log(renderBarChart(chart));

console.log("Trend:", sparkline([120, 150, 180, 200]));
```

## Module Structure

| Module        | Import Path                         | Description                              |
| ------------- | ----------------------------------- | ---------------------------------------- |
| Notebook      | `@dcyfr/ai-notebooks/notebook`      | Cell/notebook CRUD, execution engine     |
| Pipeline      | `@dcyfr/ai-notebooks/pipeline`      | Dataset ops, transforms, statistics, ETL |
| Visualization | `@dcyfr/ai-notebooks/visualization` | Charts, tables, themes, formatters       |
| Utils         | `@dcyfr/ai-notebooks/utils`         | CSV, formatting, validation              |

## Examples

```bash
# Data exploration
npm run example:explore    # or: npx tsx examples/data-exploration/index.ts

# Data pipeline
npm run example:pipeline   # or: npx tsx examples/data-pipeline/index.ts

# Model analysis
npm run example:analysis   # or: npx tsx examples/model-analysis/index.ts
```

## Documentation

- **[docs/API.md](docs/API.md)** — Full API reference
- **[docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)** — Design and module architecture
- **[docs/DEVELOPMENT.md](docs/DEVELOPMENT.md)** — Development workflow

## Environment Variables

The library reads **no environment variables** — nothing in `src/` or `examples/` consumes them. `.env.example` contains reference values only (several, like `JUPYTER_PORT` and `OPENAI_API_KEY`, are vestigial: there is no Jupyter or OpenAI integration in this package).

## Development

```bash
npm install
npm run test:run      # Run tests once
npm run test          # Watch mode (vitest)
npm run test:coverage # Coverage report
npm run lint          # Lint
npm run build         # Build
npm run typecheck     # Type check
```

## Contributing

Contributions welcome! See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

## License

MIT — See [LICENSE](LICENSE) for details.

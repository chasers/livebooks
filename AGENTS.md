# AGENTS.md

This file provides context for AI agents working on this codebase.

## Project Overview

**livebooks** is a collection of Elixir Livebooks for various purposes. Each `.livemd` file in `books/` is a self-contained interactive notebook with its own dependencies, modules, and functionality.

## File Structure

```
livebooks/
├── books/
│   └── *.livemd          # Individual Livebook notebooks
├── AGENTS.md             # This file
├── README.md
├── LICENSE
└── .gitignore
```

## How Livebooks Work

Each `.livemd` file is a standalone Elixir Livebook containing:

- **Setup cell**: `Mix.install/2` for dependencies
- **Embedded modules**: `defmodule` blocks defining reusable code
- **Interactive cells**: Code that executes in sequence
- **Markdown**: Documentation between code cells

Livebooks run in an interactive environment with access to Kino for visualizations and UI components.

## Conventions

### Dependencies
Each notebook declares its own dependencies in a setup cell:
```elixir
Mix.install([
  {:some_dep, "~> 1.0"},
  {:kino, "~> 0.16.0"}
])
```

### Environment Variables
Sensitive configuration (credentials, hostnames) should use `System.get_env/1`:
```elixir
hostname = System.get_env("MY_SERVICE_HOSTNAME")
```

### Module Organization
Define reusable modules within the notebook. Use clear names reflecting purpose:
```elixir
defmodule MyFeature do
  @moduledoc "Description of what this module does"
  # ...
end
```

### Documentation
- Add `@moduledoc` to modules
- Add `@doc` to public functions
- Include usage examples in moduledocs

## Common Patterns

### Builder Pattern
For composable APIs (like query builders), use pipe-friendly functions that return the struct:
```elixir
Builder.new()
|> Builder.option(:foo, "bar")
|> Builder.build()
```

### GenServer for Stateful Operations
Use GenServer for long-running processes that maintain state or perform periodic work.

### Kino for Visualization
Use Kino for interactive UI elements and data visualization in notebooks.

## Working with This Repository

### Adding a new Livebook
1. Create `books/your-notebook.livemd`
2. Add setup cell with dependencies
3. Define modules and interactive code
4. Test by running in Livebook

### Modifying an existing Livebook
1. Open the `.livemd` file directly—all code is inline
2. Make changes to the relevant module or cell
3. Test by running cells in Livebook

## Testing

Livebooks are tested interactively:
1. Open the `.livemd` file in Livebook
2. Run cells sequentially
3. Verify output and visualizations

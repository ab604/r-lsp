# r-lsp

Claude Code plugin for R language server integration. Provides code intelligence for R files including diagnostics, go-to-definition, hover documentation, find references, and code formatting.

> **Note:** If you're using [Positron](https://github.com/posit-dev/positron), you don't need this plugin—Positron has built-in R language server support. This plugin is for VS Code, terminal Claude Code, and other environments without native R LSP integration.

## Features

Once installed, Claude gains these capabilities when working with R files:

| Feature | Description |
|---------|-------------|
| **Diagnostics** | Automatic lintr warnings and errors after each edit |
| **Hover** | Documentation and type info for functions and variables |
| **Go to Definition** | Jump to where functions/variables are defined |
| **Find References** | Locate all usages of a symbol |
| **Document Symbols** | Outline of functions and objects in a file |
| **Formatting** | Code formatting via styler |

## Prerequisites

Install the R languageserver package:

```r
install.packages("languageserver")
```

For full functionality, also install:

```r
install.packages("lintr")   # Diagnostics
install.packages("styler")  # Formatting
```

Verify R is in your PATH:

```bash
R --version
```

## Installation

### From GitHub (recommended)

```
/plugin marketplace add ab604/r-lsp
/plugin install r-lsp@ab604-r-lsp
```

### From local path (development)

```
/plugin marketplace add /path/to/r-lsp
/plugin install r-lsp@local-r-lsp
```

## Supported File Types

| Extension | Language ID |
|-----------|-------------|
| `.R`, `.r` | r |
| `.Rmd`, `.rmd` | rmd |
| `.qmd` | quarto |

## How It Works

This plugin configures Claude Code to connect to the [R languageserver](https://github.com/REditorSupport/languageserver) package. When you open an R project:

1. Claude Code starts an R process running `languageserver::run()`
2. The language server analyzes your R files
3. Claude receives real-time diagnostics, completions, and navigation info

## Troubleshooting

### "Executable not found in $PATH"

Ensure R is installed and available:

```bash
which R
R --version
```

### "languageserver not found"

Install the R package:

```r
install.packages("languageserver")
```

### No diagnostics appearing

Install lintr:

```r
install.packages("lintr")
```

Check if lintr works:

```r
lintr::lint("your_file.R")
```

### High memory usage

The R languageserver can use significant memory on large projects. If needed:

```
/plugin disable r-lsp@ab604-r-lsp
```

## Configuration

The language server respects your project's `.lintr` file for diagnostic rules. Example `.lintr`:

```
linters: linters_with_defaults(
  line_length_linter(120),
  commented_code_linter = NULL
)
```

## Related

- [R languageserver](https://github.com/REditorSupport/languageserver) - The underlying LSP implementation
- [lintr](https://lintr.r-lib.org/) - Static code analysis for R
- [styler](https://styler.r-lib.org/) - Code formatting for R
- [claude-code-r-skills](https://github.com/ab604/claude-code-r-skills) - R development skills for Claude Code

## License

MIT

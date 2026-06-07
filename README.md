# start-llama

`start-llama` is a configurable launcher for `llama-server`, designed to simplify the process of managing and starting multiple LLM models with different runtimes and parameters.

## Features

- **Configuration-Driven**: Manage multiple model profiles in a single YAML configuration file.
- **Runtime Flexibility**: Define multiple `llama-server` executables (e.g., Vulkan, ROCm) with associated environment variables.
- **Hierarchical Parameters**: Set parameters at a global default level, override them per model, and further customize them via CLI arguments.
- **Interactive Selection**: Easily pick a model from your configuration if no specific model is provided.
- **Dry Run Mode**: Inspect the exact command that will be executed before running it.
- **Direct Model Loading**: Start any `.gguf` file directly by providing its path.

## Installation

Ensure you have `llama-server` installed and accessible on your system. 

1. Copy the `start-llama` binary to a directory in your PATH (e.g., `/usr/local/bin`).
2. Create a configuration file at `~/.llama-server-config.yaml` (or use the provided `example-config.yaml` as a template).

## Usage

### Basic Commands

| Command | Description |
| :--- | :--- |
| `./start-llama` | Interactively select and start a configured model |
| `./start-llama <model>` | Start a specific model defined in the config |
| `./start-llama <path/to/model.gguf>` | Start an arbitrary model file |
| `./start-llama --list` | List all models configured in the YAML file |
| `./start-llama --dry-run` | Print the command that would be run without executing it |
| `./start-llama --config <path>` | Use a custom configuration file |

### Overriding Parameters

You can override any `llama-server` parameter directly from the CLI:

```bash
./start-llama mymodel --port 9090 --temperature 0.7
```

## Configuration

The utility looks for a YAML config at `~/.llama-server-config.yaml` by default.

### Config Structure

- **`executables`**: Define the runtimes available.
  - `path`: Path to the `llama-server` binary.
  - `env`: Environment variables to set before execution (e.g., `HIP_VISIBLE_DEVICES`).
- **`defaults`**: Global parameters applied to all models unless overridden.
- **`models`**: Model-specific configurations.
  - `path`: Path to the `.gguf` model file.
  - `executable`: Which runtime from the `executables` section to use.
  - `alias`: A friendly name for the model.
  - `params`: Model-specific parameter overrides.

### Example Config

See `example-config.yaml` for a detailed example of how to set up various models and runtimes.

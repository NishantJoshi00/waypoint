<div align="center">
  <picture>
    <img src="./assets/image.jpeg" width="100%" style="max-height: 200px; object-fit: cover; object-position: center 25%;" />
  </picture>
</div>

# WayPoint

A fast, lightweight URL mapping and redirection system that dynamically manages URL shortcuts through YAML configuration files. Perfect for creating and managing custom URL shorteners for internal tools, documentation, or any web resources.

[![Go Report Card](https://goreportcard.com/badge/github.com/NishantJoshi00/waypoint)](https://goreportcard.com/report/github.com/NishantJoshi00/waypoint)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

[![asciicast](https://asciinema.org/a/59AwqH1WoraafCo3Ppsz0iT9R.svg)](https://asciinema.org/a/59AwqH1WoraafCo3Ppsz0iT9R)

## Features

- 🔗 **Human-readable Shortcuts** - Create memorable shortcuts for complex URLs
- 🌲 **Hierarchical Organization** - Support for nested URL structures through YAML
- 🔄 **Real-time Updates** - Configuration changes detected automatically without restart
- 🧩 **Flexible Deployment** - Use as a server or integrate with your shell
- 📊 **Multiple Access Methods** - Server mode for web access, CLI mode for shell integration
- 🐚 **Shell Integration** - Native support for zsh and fish shells

## Installation

### Prerequisites

- Go 1.22.4 or higher
- Make (optional, for using Makefile commands)

### Build from Source

```bash
# Clone the repository
git clone https://github.com/NishantJoshi00/waypoint
cd waypoint

# Build the binaries
go build ./cmd/waypoint    # Server component
go build ./cmd/wayshell   # CLI component
```

### Install System-wide

```bash
# Move binaries to system path
sudo mv waypoint /usr/local/bin/
sudo mv wayshell /usr/local/bin/
```

## Usage

### Server Mode (waypoint)

1. **Create Configuration Files**

   ```yaml
   # config.yaml
   host: localhost
   port: 8080
   map_file: map.yaml
   refresh_interval: 5 # seconds
   ```

   ```yaml
   # map.yaml
   github:
     profile: https://github.com/NishantJoshi00
   docs:
     - https://docs.example.com
   ```

2. **Start the Server**

   ```bash
   CONFIG_FILE=config.yaml ./waypoint
   ```

3. **Access URLs**
   - Visit `http://localhost:8080/github/profile`
   - Visit `http://localhost:8080/docs/0`

### CLI Mode (wayshell)

1. **Set up Configuration**

   ```yaml
   # ~/.wayshell.yaml
   gs: git status
   gp: git push
   ```

2. **Use in Shell**

   ```bash
   # For ZSH
   source scripts/init.zsh /path/to/wayshell ~/.wayshell.yaml

   # For Fish
   source scripts/init.fish /path/to/wayshell ~/.wayshell.yaml
   ```

3. **Use Shortcuts**
   ```bash
   s/gs    # Expands to 'git status'
   s/gp    # Expands to 'git push'
   ```

## Detailed Configuration

### Server Configuration Options

| Option           | Description                                    | Default     |
|------------------|------------------------------------------------|-------------|
| host             | Hostname or IP to bind the server              | localhost   |
| port             | Port to listen on                              | 8080        |
| map_file         | Path to YAML file with URL mappings            | map.yaml    |
| refresh_interval | Seconds between checking for config updates    | 5           |

### URL Mapping Structure

WayPoint supports a nested URL structure with up to 3 levels of depth:

```yaml
# Simple key-value mapping
docs: https://docs.example.com

# Nested mapping
github:
  profile: https://github.com/NishantJoshi00
  repo: https://github.com/NishantJoshi00/waypoint

# Array mapping
tutorials:
  - https://tutorial1.example.com
  - https://tutorial2.example.com
```

## Contributing Guidelines

1. **Issue First**: Create or find an issue before starting work
2. **Issue Tags**: Use descriptive tags:
   - [BUG] for bug reports
   - [FEATURE] for feature requests
   - [DOCS] for documentation improvements
3. **Work Assignment**: Don't work on issues already assigned to others
4. **Testing**: Ensure all tests pass by running `make test`
5. **Code Style**: Follow Go standard formatting guidelines

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

<div align="center">

Built by Human, Documented by LLM.

</div>

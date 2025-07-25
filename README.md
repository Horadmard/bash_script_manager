Script Manager
A Bash-based script manager that mimics npm/pnpm's package.json scripts functionality, allowing you to define and run script aliases with support for reusing scripts and passing arguments.
Features

Define script aliases in a scripts.json file
Reuse scripts by referencing other script aliases
Pass additional arguments to scripts
List available scripts
Error handling for missing scripts, invalid JSON, and circular references

Prerequisites

Bash (available on Linux/macOS or WSL on Windows)
jq (JSON parser for Bash)
Install on Ubuntu/Debian: sudo apt-get install jq
Install on macOS: brew install jq



Setup

Save the following files in your project directory:
manager.sh: The main script manager
scripts.json: Configuration file for script aliases


Make the script executable:chmod +x manager.sh


Ensure jq is installed (see Prerequisites).

scripts.json Example
{
  "scripts": {
    "dev": "docker compose -f docker-compose.yml -f docker-compose-dev.yml",
    "prod": "docker compose -f docker-compose.yml -f docker-compose-prod.yml",
    "dev:up": "dev up -d",
    "dev:down": "dev down -v",
    "prod:up": "prod up -d",
    "prod:down": "prod down",
    "logs": "dev logs -f",
    "init": "sudo chown 999:999 postgresql/certs/server.key && sudo chmod 600 postgresql/certs/server.key"
  }
}

Usage
Run scripts defined in scripts.json using the manager.sh script.
Commands

Run a script with optional arguments:
./manager.sh <script-name> [args...]

Example:
./manager.sh logs back

Executes: docker compose -f docker-compose.yml -f docker-compose-dev.yml logs -f back

List all available scripts:
./manager.sh list

Output:
Available scripts:
  dev: docker compose -f docker-compose.yml -f docker-compose-dev.yml
  prod: docker compose -f docker-compose.yml -f docker-compose-prod.yml
  dev:up: dev up -d
  dev:down: dev down -v
  prod:up: prod up -d
  prod:down: prod down
  logs: dev logs -f
  init: sudo chown 999:999 postgresql/certs/server.key && sudo chmod 600 postgresql/certs/server.key



Examples

Start development environment:
./manager.sh dev:up

Executes: docker compose -f docker-compose.yml -f docker-compose-dev.yml up -d

View logs for a specific service:
./manager.sh logs back

Executes: docker compose -f docker-compose.yml -f docker-compose-dev.yml logs -f back

Initialize permissions:
./manager.sh init

Executes: sudo chown 999:999 postgresql/certs/server.key && sudo chmod 600 postgresql/certs/server.key


Notes

Scripts can reference other scripts (e.g., dev:up uses dev), and the manager resolves these references.
Additional arguments are appended to the resolved command.
The manager prevents circular references with a maximum of 10 resolution iterations.
Ensure commands in scripts.json are valid for your environment.


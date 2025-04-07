# MoIRA Example Setup 🚀

Welcome to the **MoIRA Example Setup** repository! This project provides a complete environment for setting up and running the MoIRA Moodle plugins and related services. It includes tasks for verifying prerequisites, cloning repositories, building plugins, deploying services, and installing plugins into Moodle.

## TLDR

Run the following command to run the services and install the plugins:

```bash
task
```

Beware this might crash if not all necessary tools are installed.

## Features ✨

- **Automated Setup**: Easily verify prerequisites, clone repositories, build plugins, and deploy services using Taskfile tasks.
- **Moodle Integration**: Install and manage MoIRA plugins in a Moodle environment.
- **Dockerized Example Environment**: Pre-configured Docker Compose setup for Moodle, MariaDB, phpMyAdmin, Ollama, Qdrant, and MongoDB.

## What does this simplify? 🤔

The provided scripts simplify the process of building and running the application.
As the complexity of the project grew, we needed a better way to quickly get the app up and running.
We hope this makes it easier for you to set up the project.

## Disclaimer ⚠️
This project is a by-product of our research and is not intended for productive Moodle installations. The code may contain bugs and has not undergone complete security audits. Usage is at your own risk.

## Getting started ✅

Before you begin, ensure you have the following installed on your system:

- [nvm](https://github.com/nvm-sh/nvm) (Node Version Manager)
- Node.js (LTS version)
- [Git](https://git-scm.com/)
- [Docker](https://www.docker.com/)
- [Ollama](https://ollama.com/)
- [Taskfile](https://taskfile.dev)

You can verify these prerequisites using the following command:
```bash
task verify
```

The script will automatically validate the tools.

Copy the .env.example file to .env and configure the environment variables as needed:

```bash
cp .env.example .env
```

Do the same for the docker-compose.example.yml and copy it to docker-compose.yml

```bash
cp docker-compose.example.yml docker-compose.yml
```

## Install Instructions 🏁

In order to run the application just run:

```bash
task
```

1. ✅ Verify the tools
2. 📥 Clone the repositories
3. 🛠️ Build all plugins
4. 🐳 Deploy an example setup of Moodle
5. 📦 Install the plugins

In case you do not want to use this or already have an existing setup, you do not need to use the combined script. 
You can just utilize the individual scripts.

For more information on the steps the scripts simplify, see below.

## Manual Setup - Detailed Instructions 🛠️

If you prefer to set up the project manually without using the provided Taskfile scripts, follow these detailed steps:

### 1. Verify Prerequisites ✅

Ensure the required tools are installed on your system

```bash
task --version
nvm --version
node --version
git --version
docker --version
ollama --version
```

### 2. Clone Required Repositories 📂
Manually clone the plugin and API repositories listed in the Taskfile.yml:

```bash
git clone https://github.com/MoKITUL-FH-Erfurt/moira-core-plugin.git
git clone https://github.com/MoKITUL-FH-Erfurt/moira-block-plugin.git
git clone https://github.com/MoKITUL-FH-Erfurt/moira-activity-plugin.git
```

Clone the API repository:

```bash
git clone https://github.com/MoKITUL-FH-Erfurt/moira-api.git
```

### 3. Build the Plugins 🛠️
Navigate into each plugin repository and build it manually. For example:

```bash
cd moira-core-plugin
task
cd ../moira-block-plugin
task
cd ../moira-activity-plugin
task
```

### 4. Setup Docker Compose

Start the Docker Containers:
```bash
docker compose up -d
```

### 5. Install Plugins into Moodle 📦
Ensure all containers are running:
```bash
docker compose ps
```

Install the plugins using moosh inside the Moodle container:

```bash
docker compose exec moodle sh -c "[ -f /usr/local/bin/moosh ] || (apt-get update && apt-get install -y git unzip && cd /tmp && git clone https://github.com/tmuras/moosh && cd moosh && composer install && ln -s \$(pwd)/moosh.php /usr/local/bin/moosh)"
```

Install each plugin:

```bash
docker compose exec moodle sh -c "cd /bitnami/moodle && moosh plugin-install /bitnami/moodle/moira-core-plugin"
docker compose exec moodle sh -c "cd /bitnami/moodle && moosh plugin-install /bitnami/moodle/moira-block-plugin"
docker compose exec moodle sh -c "cd /bitnami/moodle && moosh plugin-install /bitnami/moodle/moira-activity-plugin"
```

Trigger a Moodle upgrade to recognize the plugins:

```bash
docker compose exec moodle sh -c "cd /bitnami/moodle && php admin/cli/upgrade.php --non-interactive"
```

### 6. Verify the Setup ✅

Access moodle and enjoy! 🚀

## Folder Structure 📂

```plaintext
moira-example-setup/
├── tasks/                      # Taskfile definitions for modular tasks
│   ├── build/                  # Build-related tasks
│   ├── clone/                  # Clone-related tasks
│   ├── deploy/                 # Deployment-related tasks
│   ├── install/                # Plugin installation tasks
│   └── verify/                 # Prerequisite verification tasks
├── docker-compose.example.yml  # Example Docker Compose configuration
├── .gitignore                  # Ignored files and directories
├── LICENSE                     # License information
├── README.md                   # Project documentation
└── Taskfile.yml                # Main Taskfile for running the combined setup
```

## License 📜

This project is licensed under the [MIT License](LICENSE)

## Support  💬
If you encounter any issues or have questions, feel free to open an issue in this repository or contact us at [MoKITUL FH Erfurt](https://github.com/MoKITUL-FH-Erfurt).

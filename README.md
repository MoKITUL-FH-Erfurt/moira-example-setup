# MOIRA Example Setup

Welcome to the **MOIRA Example Setup** repository! This project provides a complete environment for setting up and running the MOIRA Moodle plugins and related services. It includes tasks for verifying prerequisites, cloning repositories, building plugins, deploying services, and installing plugins into Moodle.

## Features

- **Automated Setup**: Easily verify prerequisites, clone repositories, build plugins, and deploy services using Taskfile tasks.
- **Moodle Integration**: Install and manage MOIRA plugins in a Moodle environment.
- **Dockerized Example Environment**: Pre-configured Docker Compose setup for Moodle, MariaDB, phpMyAdmin, Ollama, Qdrant, and MongoDB.

## What does this simplify?

The provided scripts simplify the process of building and running the application.
As the complexity of the project grew, we needed a better way to quickly get the app up and running.
We hope this makes it easier for you to setup the project.

---

## Prerequisites

Before you begin, ensure you have the following installed on your system:

- [nvm](https://github.com/nvm-sh/nvm) (Node Version Manager)
- Node.js (LTS version)
- [Git](https://git-scm.com/)
- [Docker](https://www.docker.com/)
- [Ollama](https://ollama.com/)

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

## Getting started

In order to run the application just run:

```bash
task
```

This will verify the tools, clone the repositories, build all plugins, deploy an example setup of moodle and finally install the plugins.
In case you do not want to use this or already have an existing setup, you do not need to use the combined script. 
You can just utilize the individual scripts.

For more information on the steps the scripts simplify, see below.

## Manual Setup

Follow these steps to setup the environment.

1. Clone the repository.

```bash
git clone https://github.com/MoKITUL-FH-Erfurt/moira-example-setup.git
cd moira-example-setup
```
2. Clone Required Repositories
Clone all plugin and API repositories:

```bash
task clone
```

3. Build the plugins
Build all cloned plugin repositories:

```bash
task build
```

4. Deploy Services
Start all Docker containers:
```bash
task deploy
```

5. Install plugins
Install MoKITUL plugins into Moodle:

```bash
task install
```

## Folder Structure

moira-example-setup/
├── tasks/                 # Taskfile definitions for modular tasks
│   ├── build/             # Build-related tasks
│   ├── clone/             # Clone-related tasks
│   ├── deploy/            # Deployment-related tasks
│   ├── install/           # Plugin installation tasks
│   └── verify/            # Prerequisite verification tasks
├── [docker-compose.example.yml](http://_vscodecontentref_/1)  # Docker Compose configuration
├── .gitignore             # Ignored files and directories
├── LICENSE                # License information
├── [README.md](http://_vscodecontentref_/2)              # Project documentation
└── [Taskfile.yml](http://_vscodecontentref_/3)           # Main Taskfile for orchestrating tasks and running the combined setup

## License

This project is licensed under the [MIT License](LICENSE)

## Support
If you encounter any issues or have questions, feel free to open an issue in this repository or contact us at [MoKITUL FH Erfurt](https://github.com/MoKITUL-FH-Erfurt).

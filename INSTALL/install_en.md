How to Install NVIDIA NemoClaw: Step-by-Step Guide

NemoClaw is an open-source stack by NVIDIA designed to run OpenClaw AI agents safely by adding privacy controls, sandboxing, and security guardrails.

Follow these easy steps to get your secure AI agent up and running.

Prerequisites

Before starting, ensure your system meets the following requirements:

Operating System: Linux (Ubuntu 22.04+ recommended). macOS and Windows (via WSL2) are supported but experimental.

Hardware: At least 8 GB of RAM (16 GB highly recommended) and around 40 GB of free disk space.

API Key: An NVIDIA API Key (you can get one for free at `build.nvidia.com`).

Step 1: Prepare Your System

NemoClaw requires Docker and Node.js (version 20 or 22) to run correctly.

###1. Verify Docker:
Ensure Docker is installed and that you have the right permissions without using sudo every time:
```
docker ps
```

(If you get a permission denied error, run `sudo usermod -aG docker $USER`, then log out and log back in).

###2. Install Node.js:
Run the following commands to install Node.js (version 22):
```
curl -fsSL [https://deb.nodesource.com/setup_22.x](https://deb.nodesource.com/setup_22.x) | sudo -E bash -
sudo apt-get install -y nodejs
```

Verify the installation by running `node --version`.

##Step 2: Install NemoClaw

NVIDIA provides a simple installation script that handles the heavy lifting.

Run the following command in your terminal:
```
curl -fsSL [https://nvidia.com/nemoclaw.sh](https://nvidia.com/nemoclaw.sh) | bash
```

Note: Depending on your system configuration, you might need to run it with `sudo bash` if you encounter permission errors.

##Step 3: Onboard Your Agent

Once the installation is complete, you need to configure your sandbox and inference settings.

Run the onboarding wizard:
```
nemoclaw onboard
```

During this interactive process:

Name your assistant (e.g., `my-assistant`).

Enter your NVIDIA API Key when prompted.

Accept the default configurations for the security policies and sandbox setup.

Note: The script will download the sandbox image (approx. 2.4 GB). This may take a few minutes.

##Step 4: Connect and Chat!

Your secure environment is now ready. It's time to connect to your sandboxed agent.

###1. Connect to the sandbox:
Replace `my-assistant` with the name you chose in Step 3.
```
nemoclaw my-assistant connect
```

###2. Start the chat interface:
Once inside the isolated sandbox, launch the OpenClaw Text User Interface (TUI):

```
openclaw tui
```

Congratulations! You can now safely type messages and interact with your sandboxed AI agent.

Troubleshooting Tips

Out of Memory (OOM) Errors: If the installation crashes on a machine with 8GB RAM, try adding swap space to your system.

WSL2 Users: If you are using Windows Subsystem for Linux and have issues with GPU passthrough during `nemoclaw onboard`, you may need to start the OpenShell gateway manually without the `--gpu` flag.

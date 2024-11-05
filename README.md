# README

## Overview

This project sets up multiple Docker containers with SSH access. Each container runs an SSH server and allows you to connect using a specified username and password.

## Prerequisites

- Docker
- Docker Compose

## Usage

1. Clone the repository:
    ```bash
    git clone <repository-url>
    cd <repository-directory>
    ```

2. Create a `.env` file in the project root and set the required environment variables:
    ```bash
    SSH_USERNAME=your_username
    SSH_PASSWORD=your_password
    AUTHORIZED_KEYS="your_ssh_public_key"
    ```

3. Start the Docker containers:
    ```bash
    docker-compose up -d
    ```

4. Connect to the containers using SSH:
    ```bash
    ssh -p 2221 $SSH_USERNAME@localhost  # Connect to node1
    ssh -p 2222 $SSH_USERNAME@localhost  # Connect to node2
    ssh -p 2223 $SSH_USERNAME@localhost  # Connect to node3
    ```
5. Alternatively, you can run the containers using `docker run`:

    ```bash
    docker run -d -p 2221:22 -e SSH_USERNAME=your_username -e SSH_PASSWORD=your_password -e AUTHORIZED_KEYS="your_ssh_public_key" wushie/ec2:latest
    ```
## Configuration

### Environment Variables

- `SSH_USERNAME`: The username for SSH login (default: `ubuntu`).
- `SSH_PASSWORD`: The password for SSH login (required).
- `AUTHORIZED_KEYS`: SSH public keys for key-based authentication (optional).
- `SSHD_CONFIG_ADDITIONAL`: Additional SSHD configuration (optional).
- `SSHD_CONFIG_FILE`: Path to a file with additional SSHD configuration (optional).

### Docker Compose Services

- **node1**: 
  - Image: `wushie/ec2:latest`
  - Ports: `2221:22`
  - Environment: `SSH_USERNAME`, `SSH_PASSWORD`, `AUTHORIZED_KEYS`

- **node2**: 
  - Image: `wushie/ec2:latest`
  - Ports: `2222:22`
  - Environment: `SSH_USERNAME`, `SSH_PASSWORD`, `AUTHORIZED_KEYS`

- **node3**: 
  - Image: `wushie/ec2:latest`
  - Ports: `2223:22`
  - Environment: `SSH_USERNAME`, `SSH_PASSWORD`, `AUTHORIZED_KEYS`

## Script Details

The provided script performs the following actions:

1. Sets default values for `SSH_USERNAME` and `SSH_PASSWORD`.
2. Creates a user with the specified username and password.
3. Adds the user to the sudo group.
4. Sets up authorized keys if provided.
5. Applies additional SSHD configuration if provided.
6. Starts the SSH server.
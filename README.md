# OpenVPN Setup using Docker, Docker Compose, and Ansible

This repository provides an automated way to set up OpenVPN using Docker and Docker Compose, managed by Ansible.

### Repository Structure

Your updated repository structure will look like this:

```
openvpn-docker-ansible/
├── ansible/
│   ├── playbook.yml
│   └── roles/
│       ├── install-requirements/
│       │   ├── tasks/
│       │   │   └── main.yml
│       ├── docker/
│       │   ├── tasks/
│       │   │   └── main.yml
│       │   └── templates/
│       │       └── docker-compose.yml.j2
│       ├── openvpn-docker-based/
│       │   ├── tasks/
│       │   │   └── main.yml
│       ├── openvpn-host-based/
│       │   ├── tasks/
│       │   │   └── main.yml
│       │   └── templates/
│       │       └── server.conf.j2
│       ├── ovpn-file-docker-based-deployment/
│       │   ├── tasks/
│       │   │   └── main.yml
│       ├── ovpn-host-based-deployment/
│       │   ├── tasks/
│       │   │   └── main.yml
│       │   └── templates/
│       │       └── client.ovpn.j2
│       ├── firewall/
│       │   ├── tasks/
│       │   │   └── main.yml
│       │   └── templates/
│       │       └── dnsmasq.conf.j2
│       └── ssh/
│           ├── tasks/
│           │   └── main.yml
├── README.md
└── requirements.txt

```


## Prerequisites

- Git
- Ansible
- Python

## Setup Instructions

1. Clone the repository:

   ```sh
   git clone https://github.com/benjisho/ansible-openvpn-docker.git
   cd ansible-openvpn-docker
   ```

2. Run the Ansible playbook:

   ```sh
   ansible-playbook ansible/playbook.yml
   ```
   - During the playbook execution, you will be prompted to choose the type of OpenVPN installation (docker/host).
   - The OpenVPN server will be set up on a random UDP port between 49152 and 65535.
   - The client configuration file (`.ovpn`) will be generated and saved in the repository's root directory.
   - Additionally, SSHD will be configured to run on a random port, and the necessary firewall rules will be applied.

## Client Configuration

After running the playbook, you will find the generated client configuration file (e.g., `myclient.ovpn`) in the root directory of this repository. Use this file to configure your OpenVPN client.

## Firewall, DNS, and SSH Configuration

The playbook configures `iptables` with rules to allow established connections, the OpenVPN UDP port, and the new SSHD port. It also sets up `dnsmasq` as a DNS forwarder.

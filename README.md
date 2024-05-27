# OpenVPN Setup using Docker, Docker Compose, and Ansible

This repository provides an automated way to set up OpenVPN using Docker and Docker Compose, managed by Ansible.

### Repository Structure

Your updated repository structure will look like this:

```
ansible-openvpn-docker/
├── ansible/
│   ├── playbook.yml
│   └── roles/
│       ├── docker/
│       │   ├── tasks/
│       │   │   └── main.yml
│       │   └── templates/
│       │       └── docker-compose.yml.j2
│       ├── openvpn/
│       │   ├── tasks/
│       │   │   └── main.yml
│       ├── ovpn/
│       │   ├── tasks/
│       │   │   └── main.yml
│       ├── firewall/
│       │   ├── tasks/
│       │   │   └── main.yml
│       │   └── templates/
│       │       └── dnsmasq.conf.j2
│       └── sshd/
│           ├── tasks/
│           │   └── main.yml
│           └── templates/
│               └── sshd_config.j2
├── README.md
└── requirements.txt
```


## Prerequisites

- Git
- Ansible
- Python and pip

## Setup Instructions

1. Clone the repository:

   ```sh
   git clone https://github.com/benjisho/ansible-openvpn-docker.git
   cd ansible-openvpn-docker
   ```

2. Install required Python packages:

   ```sh
   pip install -r requirements.txt
   ```

3. Run the Ansible playbook:

   ```sh
   ansible-playbook ansible/playbook.yml
   ```

The OpenVPN server will be set up on a random UDP port between 49000 and 65000. The client configuration file (`.ovpn`) will be generated and saved in the repository's root directory. Additionally, SSHD will be configured to run on a random port, and the necessary firewall rules will be applied.

## Client Configuration

After running the playbook, you will find the generated client configuration file (e.g., `myclient.ovpn`) in the root directory of this repository. Use this file to configure your OpenVPN client.

## Firewall, DNS, and SSH Configuration

The playbook configures `iptables` with rules to allow established connections, the OpenVPN UDP port, and the new SSHD port. It also sets up `dnsmasq` as a DNS forwarder.

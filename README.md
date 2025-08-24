# Ansible Role: MinIO Cluster

An Ansible role that installs and configures a distributed MinIO object storage cluster.

## Requirements

This role requires root access to install packages and configure the system. It is designed to work on Debian/Ubuntu and RHEL-based systems. All nodes in the cluster must be able to reach each other over the network.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
# The architecture to download the MinIO binary for.
minio_arch: "amd64"

# The path to install the MinIO binary.
minio_install_path: "/usr/local/bin"

# The system user and group to run MinIO as.
minio_user: "minio-user"
minio_group: "minio-group"

# A list of local data paths on each node for MinIO to use.
# For a cluster, all nodes should have the same number and paths of disks.
# Example: [ "/mnt/data1", "/mnt/data2" ]
minio_data_paths: [ "/usr/local/share/minio" ]

# The API and Console ports for MinIO.
minio_api_port: 9000
minio_console_port: 9001

# The root user and password for the MinIO server.
# IMPORTANT: Change these in production.
minio_root_user: "minioadmin"
minio_root_password: "minioadmin_secret_password_change_me"

# TLS/SSL settings
minio_tls_enabled: false
minio_tls_cert_dir: "/etc/minio/certs"

# Paths on the Ansible controller to the certificate and key files to be copied to the nodes.
minio_tls_cert_file: "" # e.g., "{{ playbook_dir }}/certs/minio.crt"
minio_tls_key_file: ""  # e.g., "{{ playbook_dir }}/certs/minio.key"
```

## Example Playbook

```yaml
- hosts: minio_servers
  roles:
    - role: minio_cluster
```

## License

MIT
<p><img src="https://brand.systemd.io/assets/png/systemd-logomark.png" alt="systemd logo" title="systemd" align="right" height="60" /></p>

# Ansible Role: systemd exporter

[![CircleCI](https://circleci.com/gh/cloudalchemy/ansible-systemd-exporter.svg?style=svg)](https://circleci.com/gh/cloudalchemy/ansible-systemd-exporter)
[![License](https://img.shields.io/badge/license-MIT%20License-brightgreen.svg)](https://opensource.org/licenses/MIT)
[![Ansible Role](https://img.shields.io/badge/ansible%20role-cloudalchemy.systemd_exporter-blue.svg)](https://galaxy.ansible.com/cloudalchemy/systemd_exporter/)
[![GitHub tag](https://img.shields.io/github/tag/cloudalchemy/ansible-systemd-exporter.svg)](https://github.com/cloudalchemy/ansible-systemd-exporter/tags)

## Description

Deploy prometheus [systemd exporter](https://github.com/prometheus-community/systemd_exporter) using ansible.

## Requirements

- Ansible >= 2.7 (It might work on previous versions, but we cannot guarantee it)
- gnu-tar on Mac deployer host (`brew install gnu-tar`)

## Role Variables

All variables which can be overridden are stored in [defaults/main.yml](defaults/main.yml) file as well as in table below.

| Name           | Default Value | Description                        |
| -------------- | ------------- | -----------------------------------|
| `systemd_exporter_version` | 0.5.0 | SystemD exporter package version. Also accepts latest as parameter. |
| `systemd_exporter_binary_local_dir` | "" | Allows to use local packages instead of ones distributed on github. As parameter it takes a directory where `systemd_exporter` binary is stored on host on which ansible is ran. This overrides `systemd_exporter_version` parameter |
| `systemd_exporter_web_listen_address` | "0.0.0.0:9558" | Address on which systemd exporter will listen |
| `systemd_exporter_enable_restart_count` | false | Enables service restart count metrics. This feature only works with systemd 235 and above |
| `systemd_exporter_enable_ip_accounting` | false | Enables service ip accounting metrics. This feature only works with systemd 235 and above |
| `systemd_exporter_enable_file_descriptor_size` | false | Enables file descriptor size metrics. This feature will cause exporter to run as root as it needs access to /proc/X/fd |
| `systemd_exporter_unit_includelist` | "" | Include some systemd units. Expects a regex. More in https://github.com/povilasv/systemd_exporter#configuration |
| `systemd_exporter_unit_excludelist` | "" | Exclude some systemd units. Expects a regex. More in https://github.com/povilasv/systemd_exporter#configuration |
| `systemd_exporter_tls_server_config` | "" | See [exporter-toolkit's https README](https://github.com/prometheus/exporter-toolkit/blob/v0.1.0/https/README.md) |
| `systemd_exporter_http_server_config` | "" | See [exporter-toolkit's https README](https://github.com/prometheus/exporter-toolkit/blob/v0.1.0/https/README.md) |
| `systemd_exporter_basic_auth_users` | "" | See [exporter-toolkit's https README](https://github.com/prometheus/exporter-toolkit/blob/v0.1.0/https/README.md) |

## Example

### Playbook

Use it in a playbook as follows:
```yaml
- hosts: all
  roles:
    - cloudalchemy.systemd_exporter
```

## Local Testing

The preferred way of locally testing the role is to use Docker and [molecule](https://github.com/ansible-community/molecule) (v3.x). You will have to install Docker on your system. See "Get started" for a Docker package suitable to for your system. Running your tests is as simple as executing `molecule test`.

## Continuous Intergation

Combining molecule and circle CI allows us to test how new PRs will behave when used with multiple ansible versions and multiple operating systems. This also allows use to create test scenarios for different role configurations. As a result we have a quite large test matrix which can take more time than local testing, so please be patient.

## Contributing

See [contributor guideline](CONTRIBUTING.md).

## Troubleshooting

See [troubleshooting](TROUBLESHOOTING.md).

## License

This project is licensed under MIT License. See [LICENSE](/LICENSE) for more details.

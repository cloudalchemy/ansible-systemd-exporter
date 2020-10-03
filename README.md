<p><img src="https://brand.systemd.io/assets/png/systemd-logomark.png" alt="systemd logo" title="systemd" align="right" height="60" /></p>

# Ansible Role: systemd exporter

[![Build Status](https://travis-ci.com/cloudalchemy/ansible-systemd-exporter.svg?branch=master)](https://travis-ci.com/cloudalchemy/ansible-systemd-exporter)
[![License](https://img.shields.io/badge/license-MIT%20License-brightgreen.svg)](https://opensource.org/licenses/MIT)
[![Ansible Role](https://img.shields.io/badge/ansible%20role-cloudalchemy.systemd_exporter-blue.svg)](https://galaxy.ansible.com/cloudalchemy/systemd-exporter/)
[![GitHub tag](https://img.shields.io/github/tag/cloudalchemy/ansible-systemd-exporter.svg)](https://github.com/cloudalchemy/ansible-systemd-exporter/tags)

## Description

Deploy prometheus [systemd exporter](https://github.com/povilasv/systemd_exporter) using ansible.

## Requirements

- Ansible >= 2.7 (It might work on previous versions, but we cannot guarantee it)
- gnu-tar on Mac deployer host (`brew install gnu-tar`)

## Role Variables

All variables which can be overridden are stored in [defaults/main.yml](defaults/main.yml) file as well as in table below.

| Name           | Default Value | Description                        |
| -------------- | ------------- | -----------------------------------|
| `systemd_exporter_version` | 0.4.0 | SystemD exporter package version. Also accepts latest as parameter. |
| `systemd_exporter_binary_local_dir` | "" | Allows to use local packages instead of ones distributed on github. As parameter it takes a directory where `systemd_exporter` binary is stored on host on which ansible is ran. This overrides `systemd_exporter_version` parameter |
| `systemd_exporter_web_listen_address` | "0.0.0.0:9558" | Address on which systemd exporter will listen |

## Example

### Playbook

Use it in a playbook as follows:
```yaml
- hosts: all
  roles:
    - cloudalchemy.systemd-exporter
```

### Demo site

We provide demo site for full monitoring solution based on prometheus and grafana. Repository with code and links to running instances is [available on github](https://github.com/cloudalchemy/demo-site) and site is hosted on [DigitalOcean](https://digitalocean.com).

## Local Testing

The preferred way of locally testing the role is to use Docker and [molecule](https://github.com/metacloud/molecule) (v2.x). You will have to install Docker on your system. See "Get started" for a Docker package suitable to for your system.
We are using tox to simplify process of testing on multiple ansible versions. To install tox execute:
```sh
pip3 install tox
```
To run tests on all ansible versions (WARNING: this can take some time)
```sh
tox
```
To run a custom molecule command on custom environment with only default test scenario:
```sh
tox -e py35-ansible28 -- molecule test -s default
```
For more information about molecule go to their [docs](http://molecule.readthedocs.io/en/latest/).

If you would like to run tests on remote docker host just specify `DOCKER_HOST` variable before running tox tests.

## Travis CI

Combining molecule and travis CI allows us to test how new PRs will behave when used with multiple ansible versions and multiple operating systems. This also allows use to create test scenarios for different role configurations. As a result we have a quite large test matrix which will take more time than local testing, so please be patient.

## Contributing

See [contributor guideline](CONTRIBUTING.md).

## Troubleshooting

See [troubleshooting](TROUBLESHOOTING.md).

## License

This project is licensed under MIT License. See [LICENSE](/LICENSE) for more details.

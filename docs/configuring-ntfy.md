<!--
SPDX-FileCopyrightText: 2023 Slavi Pantaleev
SPDX-FileCopyrightText: 2025 Suguru Hirahara
SPDX-FileCopyrightText: 2022 - 2024 Slavi Pantaleev
SPDX-FileCopyrightText: 2022 Julian Foad
SPDX-FileCopyrightText: 2022 MDAD project contributors
SPDX-FileCopyrightText: 2023 Felix Stupp
SPDX-FileCopyrightText: 2024 - 2025 Suguru Hirahara
SPDX-FileCopyrightText: 2020 - 2024 Slavi Pantaleev
SPDX-FileCopyrightText: 2020 - 2024 MDAD project contributors
SPDX-FileCopyrightText: 2020 Aaron Raimist
SPDX-FileCopyrightText: 2020 Mickaël Cornière
SPDX-FileCopyrightText: 2020 Chris van Dijk
SPDX-FileCopyrightText: 2020 Dominik Zajac
SPDX-FileCopyrightText: 2022 François Darveau
SPDX-FileCopyrightText: 2022 Warren Bailey
SPDX-FileCopyrightText: 2023 Antonis Christofides
SPDX-FileCopyrightText: 2023 Pierre 'McFly' Marty
SPDX-FileCopyrightText: 2024 - 2025 Suguru Hirahara

SPDX-License-Identifier: AGPL-3.0-or-later
-->

# Setting up ntfy

This is an [Ansible](https://www.ansible.com/) role which installs [ntfy](https://ntfy.sh/) to run as a [Docker](https://www.docker.com/) container wrapped in a systemd service.

Using the [UnifiedPush](https://unifiedpush.org) standard, ntfy enables self-hosted (Google-free) push notifications from servers to UnifiedPush-compatible apps running on Android and other devices.

See the project's [documentation](https://docs.ntfy.sh/) to learn what ntfy does and why it might be useful to you.

**Note**: In contrast to push notifications using Google's FCM or Apple's APNs, the use of UnifiedPush allows each end-user to choose the push notification server that they prefer. As a consequence, deploying this ntfy server does not by itself ensure any particular user or device or client app will use it.

## Adjusting the playbook configuration

To enable ntfy with this role, add the following configuration to your `vars.yml` file.

**Note**: the path should be something like `inventory/host_vars/matrix.example.com/vars.yml` if you use the [MDAD (matrix-docker-ansible-deploy)](https://github.com/spantaleev/matrix-docker-ansible-deploy) Ansible playbook.


```yaml
########################################################################
#                                                                      #
# ntfy                                                                 #
#                                                                      #
########################################################################

ntfy_enabled: true

########################################################################
#                                                                      #
# /ntfy                                                                #
#                                                                      #
########################################################################
```

### Set the hostname

**Note**: if you use the MDAD Ansible playbook, it installs ntfy on the `ntfy.` subdomain (`ntfy.example.com`) by default, so this setting is optional.

To serve ntfy you need to set the hostname as well. To do so, add the following configuration to your `vars.yml` file. Make sure to replace `example.com` with your own value.

```yaml
ntfy_hostname: "example.com"
```

After adjusting the hostname, make sure to adjust your DNS records to point the ntfy domain to your server.

## Installing

After configuring the playbook, run the installation command of your playbook as below:

```sh
ansible-playbook -i inventory/hosts setup.yml --tags=setup-all,start
```

If you use the [mash-playbook](https://github.com/mother-of-all-self-hosting/mash-playbook) or MDAD Ansible playbook, the shortcut commands with the [`just` program](https://github.com/spantaleev/matrix-docker-ansible-deploy/blob/master/docs/just.md) are also available: `just install-all` or `just setup-all`

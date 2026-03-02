A simple role to override settings in systemd services.

# Examples
## Playbook
Here's an example of a playbook to change the size of /tmp on the local
machine.  It does not require you have SSH running.

```yaml
- hosts: localhost
  connection: local
  become: true
  roles:
    - role: hax0rbana_adam.systemd_override
      systemd_override_sevice: "tmp.mount.service"
      systemd_override_content: |
        [Mount]
        What=tmpfs
        Where=/tmp
        Type=tmpfs
        Options=mode=1777,strictatime,nosuid,nodev,size=2G,nr_inodes=1m
```

Here's an example of setting nginx to restart automatically when it fails on
whatever hosts are in your inventory.

```yaml
- hosts: all
  become: true
  remote_user: root
  roles:
    - role: hax0rbana_adam.systemd_override
      systemd_override_sevice: "nginx.service"
      systemd_override_content: |
        [Service]
        Restart=on-failure
```

# Official repo location
All activity takes place on the official GitLab instance:
[https://gitlab.hax0rbana.org/public-repos/ansible/ansible-role-systemd_override](https://gitlab.hax0rbana.org/public-repos/ansible/ansible-role-systemd_override)

Any other hosting providers, such as GitHub.com and GitLab.com, are just mirrors
and we do not monitor the issue trackers over there.

# Support
## Matrix channel
You can also join our Matrix channel: #ansible:hax0rbana.org

This is a good place to ask questions or make requests without having to sign
up for another account.

# Contributing
See [contributor guidelines](CONTRIBUTING.md).

# License
This project is licensed under MIT License. See [LICENSE](LICENSE) for more details.

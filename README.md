# systemd-journald

This role configures systemd-journald.
The configuration options can be obtained from [journald.conf(5)](https://www.freedesktop.org/software/systemd/man/journald.conf.html).

You can ask this role to wipe the persistent journal directory at `/var/log/journal`.
Note that this changes journald's behaviour if the storage was set to `auto`.

To get the current systemd-journald running configuration run: `systemd-analyze cat-config systemd/journald.conf`

## Requirements

systemd with journald compiled in

## Role Variables

| Name                       | Default/Required                  | Description                                      |
|----------------------------|:---------------------------------:|--------------------------------------------------|
| `journald_config`          | `{}` / no                         | Dict of configuration items for systemd-journald |
| `journald_wipe_persistent` | `false` / no                      | Wipe the persistent journal directory            |
| `journald_config_path`     | `/etc/systemd/journald.conf` / no | Journald config file path                        |


| Configuration path                        | Description                                                              |
| ----------------------------------------- | ------------------------------------------------------------------------ |
| `/etc/systemd/journald.conf`              | default/base configuration, as defined by the local system administrator |
| `/etc/systemd/journald.conf.d/*.conf`     | local administrator override directory (filename is an arbitrary value)  |
| `/run/systemd/journald.conf.d/*.conf`     | runtime override directory (filename is an arbitrary value)              |
| `/usr/lib/systemd/journald.conf.d/*.conf` | vendor package override directory                                        |

## Dependencies

None

## Example Playbook

```yml
- hosts: all
  roles:
    - stuvusit.systemd-journald
  vars:
    journald_config:
      Storage: volatile
      RuntimeMaxUse: 1G
      ForwardToConsole: "yes"
      TTYPath: /dev/tty12
    journald_wipe_persistent: True
    journald_config_path: /etc/systemd/journald.conf.d/99-ansible.conf
```

## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).

## Author Information

- [Janne Heß](https://github.com/dasJ)

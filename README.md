# systemd-journald

This role configures systemd-journald.
The configuration options can be obtained from [journald.conf(5)](https://www.freedesktop.org/software/systemd/man/journald.conf.html).

You can ask this role to wipe the persistent journal directory at `/var/log/journal`.
Note that this changes journald's behaviour if the storage was set to `auto`.

## Requirements

systemd with journald compiled in

## Role Variables

| Name                       | Default/Required | Description                                      |
|----------------------------|:----------------:|--------------------------------------------------|
| `journald_config`          | `{}`             | Dict of configuration items for systemd-journald |
| `journald_wipe_persistent` | `false`          | Wipe the persistent journal directory            |

## Dependencies

None

## Example Playbook

```yml
- hosts: all
  roles:
  - systemd-journald
    journald_config:
      Storage: volatile
      RuntimeMaxUse: 1G
      ForwardToConsole: "yes"
      TTYPath: /dev/tty12
    journald_wipe_persistent: true
```

## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).

## Author Information

- [Janne Heß](https://github.com/dasJ)

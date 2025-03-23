# Ansible UFW

An Ansible wrapper role for installing and configuring ufw firewalls. 

---

## Why?

This role adds management of the installation of `ufw` as a functionality, as well as performing the various configuration steps of `community.general.ufw` in sequence if the correct values are defined as inputs to the task. 

It further uses the Python library `jsonschema` to validate the inputs before running any `ufw` related actions, further minimizing the likelihood of something going wrong.

## Values

```yaml
ufw:
  version: non empty string if set. If not set, defaults to 'latest'
  remove: boolean. If set, removes ufw and skips every other step.
  state: [enabled, disabled, reloaded, reset]
  logging: [on, off, low, medium, high, full]
  defaults:
    incoming: [deny, allow, reject]
    outgoing: [deny, allow, reject]
  incoming:
    - comment: non empty string <required>
      policy: [allow, limit, deny, reject] <required>
      interface: non empty string
      delete: boolean. Removes rule if exists
      from_ip: ipv4/ipv6 number, defaults to 'any'
      to_port: integer between [0, 65535] <required>
      protocol: [any (default), tcp, udp, ipv6, esp, ah, gre, igmp]
  outgoing:
    - comment: non empty string	<required>
      policy: [allow, limit, deny, reject] <required>
      interface: non empty string
      delete: boolean. Removes rule if exists
      to_ip: ipv4/v6 number, defaults to 'any'
      to_port: integer between 0 and 65535 <required>
      protocol: [any (default), tcp, udp, ipv6, esp, ah, gre, igmp]
```

### Dependencies

This role wraps the `community.general.ufw` collection and so requires that it is installed.

This role also requires the `jsonschema` Python package be installed. To do so for example using pip run:

```shell
pip install jsonschema
```

### License

[Apache 2.0](https://github.com/hrafnthor/ansible-base-server/blob/main/LICENSE)

### Author

[Hrafn Thorvaldsson](https://github.com/hrafnthor)
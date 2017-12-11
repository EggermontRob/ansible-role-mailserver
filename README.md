# Ansible role `mailserver`

An Ansible role for installing a mail server on Enterprise Linux 7 (RHEL, CentOS). Specifically, the responsibilities of this role are to:

- Install and configure the Postfix service
- Install and configure the Dovecot service
- Integrate both services
- Configure user mailboxes

## Requirements

No specific requirements

## Role Variables


| Variable   | Default | Comments (type)  |
| :---       | :---    | :---             |
| `postfix_myhostname` | mail.bertvv.local      |  |
| `postfix_mydomain` |  bertvv.local |   |
| `postfix_home_mailbox`  |  /mail |   path name of the mailbox in the user's home directory|

## Dependencies

No dependencies.

Ansible role [RHBase](https://github.com/bertvv/ansible-role-rh-base) can be used to apply firewall rules and to create users.

Ports to open:

```
rhbase_firewall_allow_services:
  - pop3s
  - imaps
rhbase_firewall_allow_ports:
  - 587/tcp
  - 465/tcp
  - 110/tcp
  - 143/tcp
```

To creat a user and to create his mailbox:

```
rhbase_users:
  - name: johndoe
    password: '$6$WIFkXf07Kn3kALDp$fHbqRKztuufS895easdT [...]'
    shell: /sbin/nologin
```

This created user can login to the mailserver but not into the linux machine.

## Example Playbook

See the test playbooks in either the [Vagrant](https://github.com/bertvv/ansible-role-mailserver/blob/vagrant-tests/test.yml) or [Docker](https://github.com/bertvv/ansible-role-mailserver/blob/docker-tests/test.yml) test environment. See the section Testing for details.

## Testing

There are two types of test environments available. One powered by Vagrant, another by Docker. The latter is suitable for running automated tests on Travis-CI. Test code is kept in separate orphan branches. For details of how to set up these test environments on your own machine, see the README files in the respective branches:

- Vagrant: [vagrant-tests](https://github.com/bertvv/ansible-role-mailserver/tree/vagrant-tests)
- Docker: [docker-tests](https://github.com/bertvv/ansible-role-mailserver/tree/docker-tests)

## Contributing

Issues, feature requests, ideas are appreciated and can be posted in the Issues section.

Pull requests are also very welcome. The best way to submit a PR is by first creating a fork of this Github project, then creating a topic branch for the suggested change and pushing that branch to your own fork. Github can then easily create a PR based on that branch. Don't forget to add your name to the contributor list below!

## License

2-clause BSD license, see [LICENSE.md](LICENSE.md)

## Contributors

- [Bert Van Vreckem](https://github.com/bertvv)
- [Pieter-Jan Philips ](https://github.com/dhrpieterjan)
- [Robbe Devos](https://github.com/devosrobbe)
- [Stijn De Lannoy](https://github.com/StijnDL)

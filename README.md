# Inject SSH Key GitHub Action

[![test inject-ssh-key](https://github.com/dym-ok/inject-ssh-key/actions/workflows/test.yml/badge.svg)](https://github.com/dym-ok/inject-ssh-key/actions/workflows/test.yml)

This GitHub action configures an SSH key on a GitHub runner.
```yaml
- name: Inject SSH Key
  uses: dym-ok/inject-ssh-key@v1
  with:
        private-key: ${{ secrets.SOME_PRIVATE_KEY }}
        host-name: 'github.com'
```

Subsequent steps can use SSH client or Git with git+ssh protocol with the 
`private-key` configured as the default key.

`host-name` input is optional and has `github.com` as the default values.
Every IP address it resolves to is added to the `~/.ssh/known_hosts`.

**Note**: this action requires `dig` which is part of the `dnsutils` package.


## Examples of usage

Imagine you have a Python project that has dependencies in private GitHub repositories.
You would need a workflow similar to this one to get your dependencies installed:

```yaml
    steps:
      - uses: actions/checkout@v4
        with:
          set-safe-directory: true

      - uses: actions/setup-python@v4
        with:
          python-version: '3.10'
          cache: 'poetry'

      - uses: dym-ok/inject-ssh-key@v2
        with:
          private-key: ${{ secrets.SSH_KEY }}

      - name: install
        run: poetry install

```

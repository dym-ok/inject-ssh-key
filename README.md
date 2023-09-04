# Inject SSH Key GitHub Action

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

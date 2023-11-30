# Signing commits
## Configuring Git
```shell
git config --global gpg.format ssh
git config --global user.signingkey "/path/to/ssh/key"
git config --global commit.gpgsign true
```

## Configuring GitHub
```shell
gh ssh-key add "/path/to/ssh/key" --type signing
```

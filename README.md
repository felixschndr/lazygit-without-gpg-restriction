# Lazygit without GPG Restrictions

This repository creates a lazygit binary from the [original source code](https://github.com/jesseduffield/lazygit) but with a small modification: Lazygit does not allow rebasing or patching commits when the user is using a GPG key to sign their changes. This is because GPG might require a passphrase to do so and lazygit can't deal with this.
That's why the developers added a check in [patch.go](https://github.com/jesseduffield/lazygit/blob/095eb130e9c141a91cf7c4dc9c26f11a07824fec/pkg/commands/git_commands/patch.go#L153) and [rebase.go](https://github.com/jesseduffield/lazygit/blob/095eb130e9c141a91cf7c4dc9c26f11a07824fec/pkg/commands/git_commands/rebase.go#L38) and a second check in [rebase.go]([rebase.go](https://github.com/jesseduffield/lazygit/blob/095eb130e9c141a91cf7c4dc9c26f11a07824fec/pkg/commands/git_commands/rebase.go#L417)) to prevent these commands to run.
Since my GPG key does not require a passphrase, lazygit actually can work with these commands without any issues.

That's why I created this repository: Every day it checks for a new lazygit release. If there is one, it will clone the lazygit source code, remove the restrictions, build a binary from it and upload it as a release to this repository.

### Installation

You can find the binary release [here](https://github.com/felixschndr/lazygit-without-gpg-restriction/releases/latest).

The following instructions work for Ubuntu but should be easily adaptable to other systems:

````shell
curl -sLo lazygit "https://github.com/felixschndr/lazygit-without-gpg-restriction/releases/latest/download/lazygit"
sudo install lazygit /usr/local/bin
rm lazygit
````

### Disclaimer

This is not affiliated with the official lazygit in any way or form.

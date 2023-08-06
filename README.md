# kickstart.nix
Kickstart your Nix environment.

## Setup

Below provides multiple ways kickstart your Nix environment depending on your operating system.

### macOS

- Install `nixpkgs` with official script:

```bash
sh <(curl -L https://nixos.org/nix/install)
```

- Install `nix-darwin` with official steps:

```bash
nix-build https://github.com/LnL7/nix-darwin/archive/master.tar.gz -A installer
./result/bin/darwin-installer
```

- Answer the following with `y` to edit your default `configuration.nix` file:

```bash
Would you like to edit the default configuration.nix before starting? [y/n] y
```

- Add the following to `configuration.nix` to enable `nix-command` and `flakes` features:

```nix
{
    nix.settings.experimental-features = [ "nix-command" "flakes" ];
}
```

- Answer the following with `y` to setup `<darwin>` in `nix-channel` (though it won't be used):

```bash
Would you like to manage <darwin> with nix-channel? [y/n] y
```

- Fork this repository to create your own flake to start with.

> NOTE: This can be done in the Github UI at https://github.com/ALT-F4-LLC/kickstart.nix

```bash
# using Github CLI
gh repo fork ALT-F4-LLC/kickstart.nix
```

- Clone your new fork locally to customize before applying:

> NOTE: You should be able to run the following command by enabling features above.

```bash
nix run nixpkgs#git clone https://github.com/<username>/kickstart.nix
```

- Update the following values in `flake.nix` configuration:

```nix
let
    system = "<insert-archtype>"; # replace
    username = "<insert-username>"; # replace
in
```

- Switch to `kickstart.nix` environment with flake configuration:

> NOTE: You must be inside your forked repository directory.

```bash
darwin-rebuild switch --flake ".#kickstart-darwin"
```

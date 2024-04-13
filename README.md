# michaelhaaf's boxkits

Each "boxkit" facilitates publishing a custom OCI, designed for ublue/bluebuild operating systems. Adapted from the [ublue-os/boxkit](https://github.com/ublue-os/boxkit) template.

## Dependencies

`podman` and `distrobox`.

## Images maintained

- `cli`: my further-opinionated adaptation of `bluefin-cli`
- `cli-dx`: my further-opinionated adaptation of `bluefin-cli-dx`
- More to come...

## Creation

These images are signed with sisgstore's cosign. You can verify the signature by downloading the cosign.pub key from this repo and running the following command:

`cosign verify --key cosign.pub ghcr.io/michaelhaaf/<image-name>`

The examples below pertain to the `cli` image though the other images in this repository would use the same commands.

### Command line

`distrobox-create --image ghcr.io/michaelhaaf/cli --name cli -Y`

### Distrobox assemble

You can initalize the OCI image with default exported apps using `distrobox-assemble`, for e.g.:

```
[cli]
image=ghcr.io/michaelhaaf/cli:latest
pull=true
replace=true
exported_apps="nvim"
exported_bins="/usr/bin/nvim /usr/bin/pass /usr/bin/tessen"
exported_bins_path="~/.local/bin"
```

### Distrobox quadlets

TODO: not tested yet, may change.

UPDATE: the following documentation is helpful:
- https://docs.podman.io/en/latest/markdown/podman-systemd.unit.5.html
- https://www.redhat.com/sysadmin/podman-run-pods-systemd-services

Let systemd manage the OCI images so they start up when you log in (otherwise, the distrobox needs to re-install base packages/etc. and that takes time.)

See https://github.com/michaelhaaf/toolboxes. I think you can do something like this:

- adapt and copy `./quadlets/containername/*` to `~/.config/containers/systemd/`
  - systemd picks this stuff up by default (?)
  - Since these are `~/.config/` files, I'm going to manage them with `chezmoi`.
- enable `podman-auto-update.timer` (?)

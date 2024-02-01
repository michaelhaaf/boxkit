# ublue-cli

ublue-cli is an Alpine Linux based OCI forked from [ublue-os/boxkit](). 

It can be used on any Linux distributon by following the usage section below.

## Creation

### Command line

`distrobox-create --image ghcr.io/michaelhaaf/boxkit --name cli -Y`

### Distrobox assemble

```
[cli]
image=ghcr.io/michaelhaaf/ublue-cli:latest 
pull=true
replace=true
init_hooks=uname -n > /etc/hostname
exported_apps="nvim"
exported_bins="/usr/bin/nvim /usr/bin/pass /usr/bin/tessen"
exported_bins_path="~/.local/bin"
```

These images are signed with sisgstore's cosign. You can verify the signature by downloading the cosign.pub key from this repo and running the following command:

`cosign verify --key cosign.pub ghcr.io/michaelhaaf/boxkit`

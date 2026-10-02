# Windows 10 Codespaces — dockur/windows edition

A Windows 10 GitHub Codespaces configuration based on [dockur/windows](https://github.com/dockur/windows).

## What this repository changes

- Pins the automatic installer to **standard Windows 10** with `VERSION: "10"`.
- Uses the upstream container's automatic Microsoft media download and unattended installation.
- Opens the browser desktop on port **8006**.
- Uses `KVM: "N"` and QEMU software emulation because GitHub Codespaces normally does not expose `/dev/kvm`.
- Uses a smaller default profile: 2 vCPUs, 4 GB RAM, and a 32 GB virtual disk.

This repository is a configuration wrapper; it does not redistribute Windows files.

## Start it

1. Open [Create a Codespace](https://codespaces.new/Nikhilsin527/windows10-dockur-codespaces).
2. Select this repository and a **4-core Codespaces machine** if available.
3. Create the Codespace and wait for the first installation. The upstream container downloads Windows 10 automatically.
4. Open forwarded port **8006** in the Ports tab.
5. The first boot/install can take a long time with software emulation. Do not stop the Codespace during installation.

## Login

The current development defaults are:

```text
Username: WindowsUser
Password: ChangeThisPassword
```

Change the password immediately after first login. To change the initial password before creating a Codespace, edit `.devcontainer/docker-compose.yml` and change `PASSWORD`.

## Important limitations

The upstream project documents KVM as its normal requirement. This derivative deliberately disables KVM to attempt compatibility with Codespaces, so performance will be substantially slower than a KVM-enabled Linux host. Gaming, GPU acceleration, and heavy workloads are not realistic.

If the Codespace reports that QEMU cannot start without KVM, that is a platform limitation rather than a repository setting; the reliable solution is a Linux VM/VPS with nested virtualization and `/dev/kvm` access.

Windows activation/licensing is not included. Use a valid Windows license where required.

## Storage and quota

The virtual disk is configured as 32 GB and is stored in the Codespace. GitHub Codespaces compute and storage quotas apply. Delete or stop the Codespace when finished.

## Security

- This repository is not affiliated with Microsoft or dockur.
- Do not add product keys, GitHub tokens, or private data to the repository.
- Change the default Windows password immediately.
- Use only the official upstream container image and review updates before using it in sensitive environments.

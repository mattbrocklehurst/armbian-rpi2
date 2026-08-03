<h3 align="center">
  <a href=#><img src="https://raw.githubusercontent.com/armbian/.github/master/profile/logosmall.png" alt="Armbian logo"></a>
  <br><br>
</h3>

# Armbian Linux Build Framework

The **Armbian Linux Build Framework** creates customizable OS images based on **Debian** or **Ubuntu** for **single-board computers (SBCs)** and embedded devices.

It builds a complete Linux system — kernel, bootloader, and root filesystem — giving you control over versions, configuration, firmware, device trees, and system optimizations. Native, cross, and containerized builds are supported for multiple architectures (`x86_64`, `aarch64`, `armhf`, `riscv64`), suitable for development, testing, production, and automation.

> **Looking for prebuilt images?** Use [Armbian Imager](https://github.com/armbian/imager/releases) — the easiest way to download and flash Armbian to your SD card or USB drive. Available for Linux, macOS, and Windows.

## Quick Start

```bash
git clone https://github.com/armbian/build
cd build
./compile.sh
```

<a href="#armbian-linux-build-framework"><img src=".github/README.gif" alt="Build demonstration" width="100%"></a>

## Build Host Requirements

### Hardware
- **RAM:** ≥8 GB (less with `KERNEL_BTF=no`)
- **Disk:** ~50 GB free space
- **Architecture:** `x86_64`, `aarch64`, or `riscv64`

### Operating System
- **Native builds:** Armbian or Ubuntu 24.04 (Noble)
- **Containerized:** any Docker-capable Linux
- **Windows:** WSL2 with Armbian / Ubuntu 24.04

### Software
- Superuser privileges (`sudo` or root)
- Up-to-date system (outdated Docker or other tools can cause failures)

## What's in this repository

The framework is primarily **Bash** (entry point `compile.sh` sources `lib/single.sh`), with helper **Python** for release-assets/manifest generation (see `action.yml`) and Makefiles for kernel device-tree overlays under `patch/kernel/`. Board, family, kernel, U-Boot, distribution and CLI configuration lives under `config/`; patches to kernels, U-Boot and other components live under `patch/`; packaging bits live under `packages/`; extensions under `extensions/`; and shared shell libraries under `lib/`.

```
compile.sh              # entry point
action.yml              # composite GitHub Action ("Rebuild Armbian")
lib/                    # shell libraries sourced by compile.sh
config/                 # boards, families, kernels, u-boot, distros, CLI
  boards/               # per-board configuration (.conf/.csc/.wip/.eos/.tvb)
  bootenv/              # boot environment files
  bootscripts/          # u-boot boot scripts (.cmd)
  cli/                  # CLI package lists
  distributions/        # supported Debian/Ubuntu distributions
  sources/families/     # SoC/family definitions
  its/                  # Image Tree Source files for FIT images
patch/                  # kernel and u-boot patch sets, DT overlays
packages/               # kernel packaging, bsp, bsp-cli, bsp-desktop, extras
extensions/             # build extensions
tools/                  # helper tools (mk_format_patch, unifying_configs)
.github/                # workflows, issue/PR templates, CODEOWNERS
```

### Board configuration status

Board configs in `config/boards/` use their file extension to signal support level:

| Extension | Meaning |
|:--|:--|
| `.conf` | supported |
| `.csc`  | community maintained / unstable |
| `.wip`  | work in progress |
| `.eos`  | end of life |
| `.tvb`  | TV box |

The full list of board configuration variables (`BOARD_NAME`, `BOARDFAMILY`, `BOOTCONFIG`, `KERNEL_TARGET`, `SERIALCON`, `MODULES*`, `DEFAULT_OVERLAYS`, …) is documented in [`config/boards/README.md`](config/boards/README.md).

## Using as a GitHub Action

This repository also ships a composite GitHub Action (`action.yml`, name: *"Rebuild Armbian"*) that checks out `armbian/os` plus this framework and drives `compile.sh` with parameters such as `armbian_board`, `armbian_release`, `armbian_kernel_branch`, `armbian_ui`, `armbian_target`, `armbian_compress`, `armbian_extensions`, and optional PGP signing. Outputs default to `build/output/images/`.

## Resources

- **[Documentation](https://docs.armbian.com/Developer-Guide_Overview/)** — comprehensive guides for building, configuring, and customizing
- **[Website](https://www.armbian.com)** — news, features, and board information
- **[Blog](https://blog.armbian.com)** — development updates and technical articles
- **[Forums](https://forum.armbian.com)** — community support and discussions

## Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on reporting issues, submitting changes, and contributing code. Board maintainers and CODEOWNERS are kept in sync automatically from the community database — to become a board maintainer, [adjust your data here](https://www.armbian.com/update-data/).

## Support

### Community Forums
Get help from users and contributors on troubleshooting, configuration, and development.
👉 [forum.armbian.com](https://forum.armbian.com)

### Real-time Chat
Join discussions with developers and community members on IRC or Discord.
👉 [Community Chat](https://docs.armbian.com/Community_IRC/)

### Paid Consultation
For commercial projects, guaranteed response times, or advanced needs, paid support is available from Armbian maintainers.
👉 [Contact us](https://www.armbian.com/contact)

## Contributors

Thank you to everyone who has contributed to Armbian!

<a href="https://github.com/armbian/build/graphs/contributors">
  <img alt="Contributors" src="https://contrib.rocks/image?repo=armbian/build" />
</a>

## Armbian Partners

Our [partnership program](https://forum.armbian.com/subscriptions) supports Armbian's development and community. Learn more about [our Partners](https://armbian.com/partners).

## License

This project is licensed under the GNU General Public License v2.0 — see [LICENSE](LICENSE) for details.

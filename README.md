# ot

Releases of `ot`, the OSINT package manager: one command installs, runs, updates or removes any tool in the
[OTInstaller registry](https://otinstaller.com). This repository only holds release downloads; the source is in
[OTInstaller/otinstaller](https://github.com/OTInstaller/otinstaller/tree/main/cli).

## Install

```sh
curl -fsSL https://get.otinstaller.com/ot | sh          # macOS and Linux
```

```powershell
irm https://get.otinstaller.com/ot.ps1 | iex            # Windows
```

The scripts download the latest release and check its signed checksums before installing. Then run `ot doctor`;
tools run in containers, so Docker Desktop or Podman must be running. Docs:
[getting started](https://otinstaller.com/docs/getting-started).

## What's in a release

| File | What it is |
| --- | --- |
| `ot_<version>_<os>_<arch>.tar.gz`, `.zip` | `ot` for macOS, Linux (`.tar.gz`) and Windows (`.zip`), on amd64 and arm64, with its README and license |
| `ot_<version>_linux_<arch>.deb`, `.rpm` | Linux packages |
| `ot_<version>_<os>_<arch>.mcpb` | MCP bundles: one-click installs of `ot mcp` in Claude Desktop |
| `server.json` | The release's entry in the MCP Registry (`com.otinstaller/ot`) |
| `install.sh`, `install.ps1` | The install scripts, with the release key built in |
| `checksums.txt` | SHA-256 of the archives and Linux packages |
| `checksums.txt.sig` | Its signature with the ot release key, checked by the install scripts and `ot self-update` |
| `checksums.txt.cosign.sig`, `checksums.txt.pem` | Its Sigstore cosign signature and certificate, from the release workflow |

## Verify a download by hand

With [cosign](https://docs.sigstore.dev/cosign/system_config/installation/), in a folder with your archive or package
and the three `checksums.txt` files:

```sh
cosign verify-blob checksums.txt \
  --signature checksums.txt.cosign.sig --certificate checksums.txt.pem \
  --certificate-identity-regexp '^https://github\.com/OTInstaller/otinstaller/\.github/workflows/release-cli\.yml@refs/tags/v' \
  --certificate-oidc-issuer https://token.actions.githubusercontent.com
sha256sum --check --ignore-missing checksums.txt
```

The first command proves `checksums.txt` came from the release workflow in OTInstaller/otinstaller; the second that
your download matches it. On macOS, use `shasum -a 256 --check --ignore-missing checksums.txt`.

Bugs and ideas: [OTInstaller/feedback](https://github.com/OTInstaller/feedback/issues). Licensed under the Apache
License 2.0.

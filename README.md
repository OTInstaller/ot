# ot

Releases of `ot`, the command-line client for the [OTInstaller Registry](https://otinstaller.com): find, install and
run OSINT tools and investigation guides.

This repository only holds release downloads. Install `ot` with:

```sh
curl -fsSL https://get.otinstaller.com/ot | sh          # macOS and Linux
```

```powershell
irm https://get.otinstaller.com/ot.ps1 | iex            # Windows
```

or download an archive, deb or rpm from [Releases](https://github.com/OTInstaller/ot/releases). Each release's
`checksums.txt` is signed with the ot release key (`checksums.txt.sig`, checked by the installers and
`ot self-update`) and with Sigstore cosign (`checksums.txt.cosign.sig` and `.pem`).

Docs: https://otinstaller.com/docs/getting-started · Bugs and ideas: https://github.com/OTInstaller/feedback/issues

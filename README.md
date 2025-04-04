# org.sabnzbd.sabnzbd

Flatpak for [SABnzbd](https://github.com/sabnzbd/sabnzbd).

## Build from source

### Update the manifest
1. Update the url for SABnzbd in the [manifest file](https://github.com/flathub/org.sabnzbd.sabnzbd/blob/85a8c16e7c2e351077c5cd83437ca4e43b2eb274/org.sabnzbd.sabnzbd.yaml#L117)
2. Update the SHA256 hash for the SABnzbd source file

### Generating Python dependencies

1. Install <https://github.com/flatpak/flatpak-builder-tools/tree/master/pip>
2. Compare and adjust packages with <https://github.com/sabnzbd/sabnzbd/blob/4.5.0/requirements.txt>
3. `flatpak install flathub org.freedesktop.Platform//23.08 org.freedesktop.Sdk//23.08`
4. `python3 flatpak-pip-generator --runtime='org.freedesktop.Sdk//23.08' --requirements-file='requirements.txt' --output pypi-dependencies`

### Generating Cargo dependencies

1. Install <https://github.com/flatpak/flatpak-builder-tools/tree/master/cargo>
2. `wget https://raw.githubusercontent.com/pyca/cryptography/42.0.8/src/rust/Cargo.lock`
3. `python3 flatpak-cargo-generator.py Cargo.lock -o cargo-sources.json`

### Install

See <https://docs.flatpak.org/en/latest/first-build.html> for details.

```bash
flatpak install org.flatpak.Builder
flatpak install flathub org.freedesktop.Platform//23.08
flatpak install flathub org.freedesktop.Sdk//23.08
flatpak install flathub org.freedesktop.Sdk.Extension.rust-stable//23.08
flatpak run org.flatpak.Builder build-dir org.sabnzbd.sabnzbd.yaml --force-clean
flatpak run org.flatpak.Builder --user --install --force-clean build-dir org.sabnzbd.sabnzbd.yaml
flatpak run org.sabnzbd.sabnzbd
```

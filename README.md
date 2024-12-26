# org.sabnzbd.sabnzbd

Flatpak for [SABnzbd](https://github.com/sabnzbd/sabnzbd).

## Build from source

### Generating Python dependencies

1. Install <https://github.com/flatpak/flatpak-builder-tools/tree/master/pip>
2. Compare and adjust packages with <https://github.com/sabnzbd/sabnzbd/blob/4.4.1/requirements.txt>
3. `flatpak install flathub org.freedesktop.Platform//23.08 org.freedesktop.Sdk//23.08`
4. `flatpak-pip-generator --runtime='org.freedesktop.Sdk//23.08' --requirements-file='requirements.txt' --output pypi-dependencies`

### Generating Cargo dependencies

1. Install <https://github.com/flatpak/flatpak-builder-tools/tree/master/cargo>
2. `wget -O cryptography.lock https://raw.githubusercontent.com/pyca/cryptography/43.0.0/src/rust/Cargo.lock`
3. `python3 flatpak-cargo-generator.py cryptography.lock -o cryptography-cargo-sources.json`
4. `wget -O maturin.lock https://raw.githubusercontent.com/PyO3/maturin/v1.8.0/Cargo.lock`
5. `python3 flatpak-cargo-generator.py maturin.lock -o maturin-cargo-sources.json`

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

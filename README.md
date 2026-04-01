# SDK Extension for OpenJDK 26

This extension contains the OpenJDK 26 Java Runtime Environment (JRE) and Java Developement Kit (JDK).

OpenJDK 26 is the current latest version. This is *not* a long-term support (LTS) version and will be periodically updated as new JDKs are released.

For the current LTS version, see the [OpenJDK 25](https://github.com/flathub/org.freedesktop.Sdk.Extension.openjdk25) extension.

For the previous LTS version, see the [OpenJDK 21](https://github.com/flathub/org.freedesktop.Sdk.Extension.openjdk21) extension.

## Usage

You can bundle the JRE with your Flatpak application by adding it to `sdk-extensions` in your Flatpak manifest and executing the `/usr/lib/sdk/openjdk/install.sh` script.

Simplified example to make the JRE available at runtime:

```yaml
id: org.example.MyApp
runtime: org.freedesktop.Platform
runtime-version: '25.08'
sdk: org.freedesktop.Sdk
sdk-extensions:
  - org.freedesktop.Sdk.Extension.openjdk

modules:
  - name: openjdk
    buildsystem: simple
    build-commands:
      - /usr/lib/sdk/openjdk/install.sh
  - name: myapp
    buildsystem: simple
    ...

...

finish-args:
  - --env=PATH=/app/jre/bin:/app/bin:/usr/bin
```

To additionally make the JRE available at buildtime of module `myapp`, set `build-options.append-path` accordingly:

```yaml
...

modules:
  ...
  - name: myapp
    buildsystem: simple
    build-options:
      append-path: /usr/lib/sdk/openjdk/jvm/openjdk-26/bin
    ...
```

## Development

### Build and install

```bash
flatpak-builder --user --install --force-clean flatpakbuildir org.freedesktop.Sdk.Extension.openjdk.yaml
```
### Uninstall

```bash
flatpak uninstall --user org.freedesktop.Sdk.Extension.openjdk

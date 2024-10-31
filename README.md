# SDK Extension for OpenJDK 23

This extension contains the OpenJDK 23 Java Runtime Environment (JRE) and Java Developement Kit (JDK).

OpenJDK 23 is the current latest version. This is *not* a long-term support (LTS) version and will be periodically updated as new JDKs are released.

For the current LTS version, see the [OpenJDK 21](https://github.com/flathub/org.freedesktop.Sdk.Extension.openjdk21) extension.

For the previous LTS version, see the [OpenJDK 17](https://github.com/flathub/org.freedesktop.Sdk.Extension.openjdk17) extension.

## Usage

You can bundle the JRE with your Flatpak application by adding this SDK extension to your Flatpak manifest and calling the install.sh script. For example:

```
{
  "id" : "org.example.MyApp",
  "runtime" : "org.freedesktop.Platform",
  "runtime-version" : "24.08",
  "sdk" : "org.freedesktop.Sdk",
  "sdk-extensions" : [
    "org.freedesktop.Sdk.Extension.openjdk"
  ],
  "modules" : [
    {
      "name" : "openjdk",
      "buildsystem" : "simple",
      "build-commands" : [
        "/usr/lib/sdk/openjdk/install.sh"
      ]
    },
    {
      "name" : "myapp",
      "buildsystem" : "simple",
      ....
    }
  ]
  ....
  "finish-args" : [
    "--env=PATH=/app/jre/bin:/app/bin:/usr/bin"
  ]
}
```

## Developement

### Build and install
```bash
flatpak-builder --user --install --force-clean flatpakbuildir org.freedesktop.Sdk.Extension.openjdk.yaml
```
### Uninstall
```bash
flatpak uninstall --user org.freedesktop.Sdk.Extension.openjdk

## Plugins

Current valid plugins are as follows:
* `ant`
* `gradle`
* `maven`
* `openjfx` (JavaFX)

Please note that they are currently installed to `/usr/lib/sdk/openjdk.plugins.<plugin_name>` instead of `/usr/lib/sdk/openjdk/extensions/<plugin_name>`. This will hopefully be fixed in the future.

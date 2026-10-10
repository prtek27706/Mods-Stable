# Mindustry v8 / build 160.5 port status

This working copy has been retargeted from Mindustry v155.4 to v160.5 and its mod metadata now declares build 160 as the minimum version. The existing source code and restored assets are retained.

## Build requirements

- JDK 17
- Gradle wrapper (downloads the configured Gradle distribution on first run)
- Network access to resolve Mindustry, Arc, Jabel, and MultiCrafterLib dependencies

## Important validation note

The compile task could not be run in the editing environment because it could not resolve `services.gradle.org` (DNS/network unavailable). This means the API migration is not yet compile-verified. A v160.5 compile may reveal changed Mindustry/Arc APIs or a MultiCrafterLib compatibility issue; those must be fixed from the actual compiler diagnostics before this can be considered a working port.

Run `./gradlew clean jar` on Linux/macOS or `gradlew.bat clean jar` on Windows with JDK 17. The current Gradle configuration intentionally uses Jabel and Java 8 bytecode output for broad Mindustry runtime compatibility while allowing Java 17 source syntax.

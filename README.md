# Petrus-Github-Maven

A Maven repository kept in git, for third-party plugin jars that no public repository serves any
more. FinalCraft builds compile against them (`compileOnly`); nothing here is bundled into a plugin.

## Usage

Gradle:

```groovy
repositories {
    maven {
        url = 'https://github.com/EverNife/Petrus-Github-Maven/raw/master'
        content { includeGroup 'com.griefdefender'; includeGroup 'net.kaikk.mc' }
    }
}
```

Maven:

```xml
<repository>
    <id>petrus-github-maven</id>
    <url>https://github.com/EverNife/Petrus-Github-Maven/raw/master</url>
</repository>
```

## Artifacts

| Coordinate | Source | License |
|---|---|---|
| `com.griefdefender:griefdefender-bukkit:2.2.1` | GriefDefender plugin jar; only its API is published upstream | MIT (`bloodmc/GriefDefender`) |
| `net.kaikk.mc:GriefPreventionPlus:13.3` | plugin jar; upstream repository is gone | GPL-3.0 |

## Adding an artifact

Every artifact gets a minimal POM with no dependencies. Plugin jars often carry their own or a shaded
library's `META-INF/maven/**/pom.xml`, and `deploy-file` picks that up unless one is passed:

```bash
mvn deploy:deploy-file -Durl=file:///<this checkout> -DrepositoryId=local \
    -Dfile=<plugin>.jar -DpomFile=<minimal>.pom
```

# fan87's Maven Public Repository

The public maven repository that contains libraries that's made under fan87.

## Maven

### Setup
> :warning: Only people has "write package" accecss to this repository and wants to deploy have to do this


1. Add this into your `~/.m2/settings.xml`:

```xml
    <server>
      <id>github</id>
      <username>GITHUB_USERNAME</username>
      <password>GITHUB_ACCESS_TOKEN</password>
    </server>

```

Don't forget to replace `GITHUB_USERNAME` to your user name, and `GITHUB_ACCESS_TOKEN` to an access token that has permission to read/write packages.

### Using

1. Add this to your pom.xml

```xml
<repositories>
    <repository>
        <id>github</id>
        <name>fan87's Public Maven Repository</name>
        <url>https://maven.pkg.github.com/fan87/Public-Maven-Repository</url>
        <snapshots>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
        </snapshots>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
        </releases>
    </repository>
</repositories>
```

2. Now you can start adding dependencies!

### Deploying
> :warning: Only people has "write package" accecss to this repository can do it

1. Add this to your pom.xml

```xml
<distributionManagement>
    <repository>
        <id>github</id>
        <name>fan87's Public Maven Repository</name>
        <url>https://maven.pkg.github.com/fan87/Public-Maven-Repository</url>
    </repository>
</distributionManagement>
```

2. Now run `deploy` task. (For example: `mvn clean package install deploy`)

-----

## Gradle (Kotlin DSL)

### Setup
> :warning: Only people has "write package" accecss to this repository and wants to deploy have to do this

1. Add `GITHUB_USERNAME` and `GITHUB_PASSWORD` to your environment variable. The value will be your username and access token, not your GitHub password!

### Using

1. Add this to your build.gradle.kts

```kotlin
repositories {
    mavenCentral() // Optional
    fan87PUblic()
}

fun RepositoryHandler.fan87Public() {
    maven {
        name = "rektsky-private"
        url = URI("https://maven.pkg.github.com/fan87/Public-Maven-Repository")
        credentials {
            username = System.getenv("GITHUB_USERNAME")
            password = System.getenv("GITHUB_PASSWORD")
        }
    }
}
```

If you are using any plugin, add this to settings.gradle.kts

```kotlin
pluginManagement {
    repositories {
        mavenLocal()
        gradlePluginPortal()
        maven {
            name = "fan87-public"
            url = URI("https://maven.pkg.github.com/fan87/Public-Maven-Repository")
            credentials {
                username = System.getenv("GITHUB_USERNAME")
                password = System.getenv("GITHUB_PASSWORD")
            }
        }
    }
}
```



### Deploying
> :warning: Only people has "write package" accecss to this repository can do it

1. Add this to your build.gradle.kts:

```kotlin
plugins {
    `maven-publish`
}

publishing {
    repositories {
        fan87Public()
        mavenLocal()
    }
}

fun RepositoryHandler.rektskyRepository() { // If you already have this, then you don't have to add it again
    maven {
        name = "fan87-public"
        url = URI("https://maven.pkg.github.com/fan87/Pubic-Maven-Repository")
        credentials {
            username = System.getenv("GITHUB_USERNAME")
            password = System.getenv("GITHUB_PASSWORD")
        }
    }
}
```


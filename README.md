# Introduction

This repository contains all my Android libraries powered by Github Packages.

# Usage

1. Go to https://github.com/settings/tokens and create a new token with `read:packages`

2. In your project root folder, create the file `github.properties` and add the following:

    ```Gradle
    gpr.usr=YOUR_USER
    gpr.key=YOUR_TOKEN  
    ```

3. Open your `settings.gradle.kts` file and add the dependency. Should look like:

    ```Gradle
    dependencyResolutionManagement {
        repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
        repositories {
            google()
            mavenCentral()

            val githubProperties = Properties()
            githubProperties.load(FileInputStream("./github.properties"))

            githubPackages.forEach { packageUrl ->
                maven {
                    name = "GitHubPackages"
                    url = uri("https://maven.pkg.github.com/supermegazinc/Android-Libraries")
                    credentials {
                        username = githubProperties["gpr.usr"] as String?
                        password = githubProperties["gpr.key"] as String?
                    }
                }
            }
        }
    }
    ```

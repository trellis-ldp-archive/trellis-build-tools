# A Collection of build tools for Trellis LDP projects

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/org.trellisldp/trellis-build-tools/badge.svg)](https://maven-badges.herokuapp.com/maven-central/org.trellisldp/trellis-build-tools/)

This repository contains a number of artifacts that can be included in external projects.

For example:

  * checkstyle configuration
  * license checking

With Gradle, add the following to the `build.gradle` script:

    configuration {
        buildToolsConfig
    }

    dependencies {
        buildToolsConfig "org.trellisldp:trellis-build-tools:0.2.0"
    }

    checkstyle {
        config = resources.text.fromArchiveEntry(configurations.buildToolsConfig, "checkstyle/checkstyle.xml")
        configProperties.checkstyleConfigDir = resources.text.fromArchiveEntry(configurations.buildToolsConfig, "checkstyle/suppressions.xml").asFile().parent
        showViolations true
        ignoreFailures true
        toolVersion = '8.1'
    }

    license {
        include "**/*.java"
        header = resources.text.fromArchiveEntry(configurations.buildToolsConfig, 'license/HEADER.txt').asFile()
        sourceSets = project.sourceSets
        ignoreFailures false
        strictCheck true
        mapping {
            java = 'SLASHSTAR_STYLE'
        }
    }



# API Code Style Configuration

This repository contains code formatting configurations for API Spec code generation.

## 📂 Available Formatters

- `config/formatter/eclipse-formatter.xml` – Java formatter configuration for Eclipse and tools like [Spotless](https://github.com/diffplug/spotless).

## 🛠️ Usage with Gradle Spotless Plugin

To apply this formatter in your project using [Spotless](https://github.com/diffplug/spotless):

### 1. Add the Spotless plugin

In your `build.gradle`:

```groovy
plugins {
  id 'com.diffplug.spotless' version '7.0.3'
}
```

### 2. Configure Spotless to use the downloaded formatter

The Spotless plugin does not support URLs directly in `configFile`. You must first download the formatter XML into your build directory:

```groovy
def formatterUrl = 'https://raw.githubusercontent.com/hmcts/api-cp-code-style/main/config/formatter/eclipse-formatter.xml'
def formatterPath = "$buildDir/eclipse-formatter.xml"

tasks.register('downloadFormatter') {
  outputs.file(formatterPath)
  doLast {
    def file = new File(formatterPath)
    file.parentFile.mkdirs()
    file.text = new URL(formatterUrl).text
  }
}

spotless {
  java {
    removeUnusedImports()
    eclipse().configFile(formatterPath)
  }
}

tasks.named('spotlessApply') {
  dependsOn tasks.named('downloadFormatter')
}

tasks.named('spotlessJava') {
  dependsOn tasks.named('downloadFormatter')
}
```

### 3. Run formatting

```bash
gradle spotlessApply
```

## 🔒 Licence

This repository is open-sourced under the MIT License.

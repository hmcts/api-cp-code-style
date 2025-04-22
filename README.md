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

### 2. Configure Spotless to use the remote formatter

```groovy
spotless {
  java {
    removeUnusedImports()
    eclipse().configFile('https://raw.githubusercontent.com/hmcts/api-cp-code-style/master/config/formatter/eclipse-formatter.xml')
  }
}
```

### 3. Run formatting

```bash
gradle spotlessApply
```

## 🔒 Licence

This repository is open-sourced under the MIT License.

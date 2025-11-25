# Maven Build and Test Composite Action

This GitHub Action provides a reusable, configurable way to build and test Maven projects. It sets up the JDK, installs Maven, optionally sets the Maven project version, and runs a Maven build/test command. This action is ideal for Java projects using Maven in CI/CD pipelines.

## Features
- Installs a specified JDK version (default: 17)
- Installs Maven (default: system package, or custom version)
- Optionally sets the Maven project version using `mvn versions:set`
- Supports custom working directory

## Usage
```yaml
- name: Install Java & Maven
  uses: vikram301093/java-maven-action@v1.0.0
  with:
    java-version: '17'                # Optional, default: '17'
    maven-version: 'default'          # Optional, default: 'default' (system package)
    new-version: '1.2.3'              # Optional, default: '' (no version set)
    working-directory: './sandbox'    # Optional, default: '.'
```

## Inputs
| Name               | Description                                         | Default     |
|--------------------|-----------------------------------------------------|-------------|
| `java-version`     | JDK version to use                                  | `'17'`      |
| `maven-version`    | Maven version to install (`default` = system)       | `'default'` |
| `working-directory`| Directory containing the `pom.xml`                  | `'.'`       |
| `new-version`      | Version to set with `mvn versions:set`              | `''`        |

## Example
```yaml
- name: Install Java & Maven
  uses: vikram301093/java-maven-action@v1.0.1
  with:
    java-version: '21'
    maven-version: '3.9.6'
    new-version: '2.0.0'
    working-directory: './my-module'
```

## Notes
- If you want to use a custom Maven version, specify it (e.g., `3.9.6`). Otherwise, the system Maven will be installed.
- If `new-version` is not set, the Maven version will not be changed.
- The action runs `mvn -B clean verify --file pom.xml` by default. If you set `skip-tests: 'true'`, it will run with `-DskipTests` to skip tests.

---

Feel free to open issues or PRs for improvements!
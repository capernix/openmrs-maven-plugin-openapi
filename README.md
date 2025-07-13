# OpenMRS REST Representation Analyzer

![alt text](src/static/openmrs.png)

A sophisticated Maven plugin that programmatically analyzes OpenMRS REST resources at build time to extract detailed representation metadata. This plugin uses a forked process approach to overcome Maven plugin classloader limitations and provides comprehensive analysis of REST resource handlers with their representation structures.

## What This Plugin Does

This plugin automatically discovers and analyzes **all OpenMRS REST resource handlers** in your project, extracting:

- **Resource metadata** (names, supported classes, handler classes)
- **Representation structures** (DEFAULT, FULL, REF property counts)
- **Version compatibility** (supported OpenMRS versions)
- **Error handling** (graceful handling of malformed resources)

Perfect for **automatic documentation generation**, **API discovery**, and **OpenMRS module analysis**.

## Architecture

### Forked Process Design
```
Maven Plugin (Lightweight)
    ↓ Spawns
Forked JVM (Full OpenMRS Context)
    ↓ Analyzes
REST Resource Handlers
    ↓ Generates
Structured JSON Analysis
```
## Sample Output

```json
{
  "metadata": {
    "timestamp": "2025-07-13T11:24:00.360Z",
    "pluginVersion": "1.0.0-SNAPSHOT",
    "resourceCount": 94
  },
  "resources": [
    {
      "resourceName": "v1/person",
      "supportedClass": "Person",
      "handlerClass": "PersonResource1_8",
      "handlerPackage": "org.openmrs.module.webservices.rest.web.v1_0.resource.openmrs1_8",
      "supportedVersions": ["1.8.* - 9.*"],
      "representations": {
        "DEFAULT": {"propertyCount": 15, "linkCount": 3},
        "FULL": {"propertyCount": 25, "linkCount": 5},
        "REF": {"propertyCount": 2, "linkCount": 1}
      }
    }
  ]
}
```

## Quick Start

### Prerequisites
- **Java 8+** (same as OpenMRS requirement)
- **Maven 3.6+**
- **OpenMRS project** (with REST module dependencies)

### Installation

1. **Clone the repository:**
```bash
git clone https://github.com/your-username/openmrs-rest-representation-analyzer.git
cd openmrs-rest-representation-analyzer
```

2. **Install the plugin:**
```bash
mvn clean install
```

## Usage Commands

### Basic Analysis
```bash
# Run analysis on OpenMRS project
mvn org.openmrs.plugin:openmrs-rest-analyzer:1.0.0-SNAPSHOT:analyze-representations   

# With custom timeout (default: 300 seconds)
mvn org.openmrs.plugin:openmrs-rest-analyzer:1.0.0-SNAPSHOT:analyze-representations -DtimeoutSeconds=600
```

### Integrate with Build Lifecycle
```bash
# Run during normal build (plugin auto-executes during process-classes phase)
mvn clean compile

# Full build with analysis
mvn clean install
```

### Development Commands
```bash
# Build and test the plugin itself
mvn clean install

# Run plugin tests
mvn test

# Debug mode with verbose output
mvn org.openmrs.plugin:openmrs-rest-analyzer:1.0.0-SNAPSHOT:analyze-representations -X

# Check plugin dependencies
mvn dependency:tree
```
### Dependencies (Auto-Resolved)
- OpenMRS API 2.4+
- OpenMRS Web Services REST Module
- Jackson 2.11+ (for JSON generation)
- JUnit 4.12+ (for test execution)
- H2 Database (for in-memory testing)

## Contributing

1. **Fork the repository**
2. **Create feature branch**: `git checkout -b feature/amazing-feature`
3. **Commit changes**: `git commit -m 'Add amazing feature'`
4. **Push to branch**: `git push origin feature/amazing-feature`
5. **Open Pull Request**

### Development Guidelines
- Follow OpenMRS coding standards
- Add tests for new functionality
- Update documentation for API changes
- Ensure backward compatibility

## 🏥 OpenMRS Community

- **OpenMRS Wiki**: https://wiki.openmrs.org/
- **Developer Documentation**: https://wiki.openmrs.org/display/docs/Developer+Documentation
- **REST API Documentation**: https://wiki.openmrs.org/display/docs/REST+Web+Service+API+For+Clients

## Related Projects

- [OpenMRS REST Web Services](https://github.com/openmrs/openmrs-module-webservices.rest)
- [OpenMRS Core](https://github.com/openmrs/openmrs-core)
- [OpenMRS Platform](https://github.com/openmrs/openmrs-distro-platform)

---

**Built with ❤️ for the OpenMRS Community**
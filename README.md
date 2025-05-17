# Zygote

> A modern JDBC to ODBC Bridge written in Zig

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

## Overview

Zygote is an open-source JDBC to ODBC bridge that enables Java applications to connect to databases through ODBC drivers. Built with the Zig programming language, Zygote offers superior performance, memory safety, and cross-platform compatibility compared to traditional bridge solutions.

The name "Zygote" represents our philosophy: just as a zygote in biology forms from the union of two different cells to create new life, our bridge unites two different database connectivity standards (JDBC and ODBC) to create new possibilities for your applications.

## Why Zygote?

- **High Performance**: Written in Zig for maximum efficiency and minimal overhead
- **Memory Safe**: Leverages Zig's compile-time safety without runtime costs
- **Cross-Platform**: Easily deployable across Windows, macOS, and Linux
- **Zero Dependencies**: Self-contained with no external runtime requirements
- **Modern Architecture**: Designed for cloud-native and containerized environments
- **Thread Safe**: Built with concurrency in mind

## Features

- Full JDBC 4.3 API compatibility
- Support for all major ODBC data types
- Connection pooling
- Prepared statement caching
- Batch operations
- Transaction management
- Comprehensive type conversion
- Detailed error reporting

## Usage

### Maven Dependency

```xml
<dependency>
    <groupId>io.zygote</groupId>
    <artifactId>zygote-jdbc</artifactId>
    <version>0.1.0</version>
</dependency>
```

### Gradle Dependency

```gradle
implementation 'io.zygote:zygote-jdbc:0.1.0'
```

### JDBC URL Format

```
jdbc:zygote:odbc:<odbc-dsn-or-connection-string>
```

### Example

```java
import java.sql.*;

public class ZygoteExample {
    public static void main(String[] args) throws Exception {
        // Load the Zygote JDBC driver
        Class.forName("io.zygote.jdbc.Driver");
        
        // Connect to a database through ODBC
        try (Connection conn = DriverManager.getConnection(
                "jdbc:zygote:odbc:MyOdbcDsn", "username", "password")) {
            
            // Execute a query
            try (Statement stmt = conn.createStatement()) {
                ResultSet rs = stmt.executeQuery("SELECT * FROM users");
                
                // Process results
                while (rs.next()) {
                    System.out.println(rs.getString("name") + ": " + rs.getString("email"));
                }
            }
        }
    }
}
```

## Architecture

Zygote consists of three main components:

1. **Java JDBC Driver**: A pure Java implementation of the JDBC interfaces that communicates with the core bridge.

2. **Core Bridge (Zig)**: The heart of Zygote, written in Zig. It handles the conversion between JDBC calls and ODBC operations.

3. **ODBC Connector**: A native component that interfaces with ODBC drivers using Zig's powerful FFI capabilities.

```
Java Application → JDBC API → Zygote Java Driver → JNI → Zygote Core (Zig) → ODBC API → Database
```

## Building from Source

### Prerequisites

- Zig 0.11.0 or later
- JDK 11 or later
- Maven 3.6 or later

### Build Steps

1. Clone the repository:
   ```bash
   git clone https://github.com/pesnik/zygote.git
   cd zygote
   ```

2. Build the Zig native components:
   ```bash
   zig build
   ```

3. Build the Java JDBC driver:
   ```bash
   mvn package
   ```

4. Run the tests:
   ```bash
   mvn test
   ```

## Project Status

Zygote is currently in alpha stage. We welcome contributors and early adopters who are interested in helping shape the future of database connectivity.

### Roadmap

- [ ] Complete JDBC 4.3 API support
- [ ] Comprehensive test suite
- [ ] Performance benchmarking
- [ ] Connection pooling
- [ ] Docker integration
- [ ] Cloud platform specific optimizations

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

### Development Philosophy

- **Safety First**: All code should be memory safe and handle errors appropriately
- **Performance Matters**: The bridge should add minimal overhead
- **Clear Documentation**: All public APIs should be well documented
- **Comprehensive Testing**: High test coverage is essential

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

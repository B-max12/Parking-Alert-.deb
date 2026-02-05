# 🚗 Park Alert System

A comprehensive **Vehicle Parking Violation Alert System** that enables efficient vehicle registration, QR code generation, and real-time notification of parking violations via SMS. Built with C++ backend, React/TypeScript frontend, and modern DevOps practices.

![Version](https://img.shields.io/badge/version-1.0.0-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Platform](https://img.shields.io/badge/platform-Linux%20%7C%20Windows-orange)

## 📋 Table of Contents

- [Features](#features)
- [Project Structure](#project-structure)
- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Configuration](#configuration)
- [Development](#development)
- [Database Setup](#database-setup)
- [Docker Deployment](#docker-deployment)
- [Building & Packaging](#building--packaging)
- [Usage](#usage)
- [Architecture](#architecture)
- [Contributing](#contributing)
- [License](#license)

## ✨ Features

### Core Features
- **Vehicle Registration**: Register vehicles with license plate, owner info, and contact details
- **QR Code Generation**: Automatically generate unique QR codes for each registered vehicle using `libqrencode`
- **Parking Violation Alerts**: Report and track parking violations in real-time
- **SMS Notifications**: Send instant SMS alerts to vehicle owners about violations
- **Vehicle Management**: View, update, and manage registered vehicles
- **Location Tracking**: Record parking violation location (latitude, longitude, address)

### Technical Features
- **Custom Data Structures**: Optimized hash tables and queues for efficient data management
- **Database Support**: MySQL 8.0+ with comprehensive schema
- **HTTP API**: RESTful API for vehicle and alert management
- **Desktop Application**: Electron-based cross-platform desktop client with React UI
- **Multiple SMS Providers**: Support for Twilio and local SMS gateways
- **Docker Support**: Containerized deployment with Docker Compose
- **Debian Packaging**: Ready-to-install `.deb` packages for Linux systems
- **Notification Queue**: Priority-based notification processing with retry logic

## 📁 Project Structure

```
park_alert/
├── src/                          # C++ source code
│   ├── main.cpp                 # Application entry point
│   ├── api/
│   │   └── http_server.cpp      # HTTP API server implementation
│   ├── database/
│   │   └── db_manager.cpp       # Database connection & operations
│   └── services/
│       ├── sms_service.cpp      # SMS sending service
│       ├── notification_service.cpp
│       └── qr_service.cpp       # QR code generation
├── include/                      # C++ header files
│   ├── api/
│   ├── database/
│   ├── models/
│   ├── services/
│   └── dsa/                     # Data Structure implementations
├── frontend_backup/              # React/Electron frontend
│   ├── src/
│   │   ├── components/          # React components
│   │   ├── pages/               # Application pages
│   │   └── App.tsx
│   ├── electron/                # Electron main process
│   └── package.json
├── sql/                          # Database schemas
│   └── schema.sql               # MySQL database schema
├── debian/                       # Debian package configuration
├── CMakeLists.txt               # C++ build configuration
├── Dockerfile                    # Docker image configuration
├── compose.yaml                  # Docker Compose setup
└── build/                        # Compiled binaries (generated)
```

## 🛠 Tech Stack

### Backend
- **Language**: C++ (C++17 standard)
- **HTTP Server**: Custom HTTP API implementation
- **Database**: MySQL 8.0+
- **QR Code Library**: `libqrencode`
- **Build System**: CMake 3.16+

### Frontend
- **Framework**: React 18+ with TypeScript
- **Desktop**: Electron
- **UI Library**: Tailwind CSS
- **Build Tool**: Vite
- **Package Manager**: Bun/npm

### DevOps & Deployment
- **Containerization**: Docker & Docker Compose
- **Packaging**: Debian (.deb)
- **CI/CD**: Compatible with GitHub Actions

### Data Structures
- Custom Hash Table implementation
- Queue data structure for notification processing
- Priority-based queue for SMS delivery

## 📦 Prerequisites

### System Requirements
- **OS**: Linux (Ubuntu 20.04+), macOS, or Windows
- **RAM**: 2GB minimum
- **Disk Space**: 500MB for installation

### Required Packages
- **CMake**: v3.16 or higher
- **GCC/Clang**: C++17 compatible compiler
- **libqrencode-dev**: For QR code generation
- **MySQL Client**: For database connectivity (optional but recommended)
- **Node.js/Bun**: For frontend development

### Installation of Dependencies

**On Ubuntu/Debian:**
```bash
sudo apt-get update
sudo apt-get install -y \
    build-essential \
    cmake \
    libqrencode-dev \
    mysql-client \
    pkg-config
```

**On macOS:**
```bash
brew install cmake libqrencode mysql-client
```

## 🚀 Installation

### 1. Clone the Repository
```bash
git clone https://github.com/B-max12/park_alert.git
cd park_alert
```

### 2. Build the C++ Backend
```bash
# Create build directory
mkdir -p build
cd build

# Configure with CMake
cmake ..

# Build the project
make

# Binary will be created at: ./build/park_alert
cd ..
```

### 3. Setup Frontend (Optional for Desktop App)
```bash
cd frontend_backup

# Install dependencies
npm install
# or
bun install

# Build for production
npm run build
```

## ⚡ Quick Start

### Run CLI Application
```bash
./build/park_alert
```

This launches an interactive menu where you can:
1. Register a new vehicle
2. Generate QR codes
3. Report parking violations
4. View registered vehicles

### Run Electron Desktop App
```bash
cd frontend_backup

# Development mode
npm run electron:dev

# Build for Linux (creates .deb package)
npm run electron:build:linux
```

### Run as Debian Package
```bash
# Install
sudo dpkg -i park_alert_package.deb

# Run
park_alert

# Uninstall
sudo dpkg -r park-alert
```

## ⚙️ Configuration

### Environment Variables
Create a `.env` file in the project root:

```bash
# Database Configuration
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=your_password
DB_NAME=park_alert

# SMS Service Configuration
SMS_PROVIDER=twilio  # or local_gateway
TWILIO_ACCOUNT_SID=your_account_sid
TWILIO_AUTH_TOKEN=your_auth_token
TWILIO_PHONE_NUMBER=+1234567890

# Local SMS Gateway
LOCAL_SMS_URL=http://gateway.local/api
LOCAL_SMS_API_KEY=your_api_key
LOCAL_SMS_SENDER_ID=ParkAlert

# HTTP Server
HTTP_SERVER_PORT=8080
```

### Database Configuration
Update database connection parameters in your code or configuration file:

```cpp
// Example in your application
std::string db_host = "localhost";
int db_port = 3306;
std::string db_user = "park_alert_user";
std::string db_password = "secure_password";
std::string db_name = "park_alert";
```

## 🔧 Development

### Building with Debug Information
```bash
cd build
cmake -DCMAKE_BUILD_TYPE=Debug ..
make
```

### Running Tests
```bash
# Tests would be run from build directory
cd build
# (Test commands to be configured)
```

### Code Structure
- **Models**: Entity definitions (`vehicle.hpp`, `user.hpp`, `notification.hpp`)
- **Services**: Business logic (`sms_service.hpp`, `qr_service.hpp`, `notification_service.hpp`)
- **Database**: Data access layer (`db_manager.hpp`)
- **API**: HTTP endpoints (`http_server.hpp`)
- **DSA**: Custom data structures (`hash_table.hpp`, `queue.hpp`)

## 🗄️ Database Setup

### Create Database and Tables
```bash
# Login to MySQL
mysql -u root -p

# Execute schema
mysql -u root -p < sql/schema.sql
```

### Database Schema Overview

**tables:**
- `users` - User account information
- `vehicles` - Registered vehicles with QR data
- `notifications` - Parking violation alerts
- `notification_queue` - Queue for processing notifications
- `sms_logs` - SMS delivery tracking

**Key Features:**
- Automatic timestamps for audit trails
- Foreign key constraints for data integrity
- Indexed lookups for performance
- Status enums for state tracking

## 🐳 Docker Deployment

### Build Docker Image
```bash
docker build -t park-alert:latest .
```

### Run with Docker Compose
```bash
# Single service
docker-compose -f compose.yaml up

# With debug configuration
docker-compose -f compose.debug.yaml up
```

### Docker Compose Services
```yaml
parkalert:
  - Runs compiled Park Alert application
  - Exposes HTTP API
  - Connects to external MySQL database
```

## 📦 Building & Packaging

### Create Debian Package
```bash
cd frontend_backup
npm run electron:build:linux

# Package location: ./release/park-alert_*.deb
```

### Manual Deb Package Creation
```bash
./build_and_package.sh
```

### Install from Deb Package
```bash
sudo dpkg -i park_alert_package.deb

# Verify installation
which park_alert
```

## 💡 Usage Examples

### Register a Vehicle
```
Enter your choice (1-5): 1
Enter license plate: ABC-123
Enter owner name: John Doe
Enter phone number: +92300123456
```

### Generate QR Code
```
Enter your choice (1-5): 2
Enter vehicle license plate: ABC-123
QR Code generated successfully!
```

### Report Parking Violation
```
Enter your choice (1-5): 3
Enter license plate: ABC-123
Enter reporter phone: +92300654321
Enter location: Parking Lot A
SMS alert sent to vehicle owner!
```

## 🏗️ Architecture

### System Architecture

```
┌─────────────────────────────────────────────────────────┐
│                   Desktop Application                    │
│              (Electron + React + TypeScript)             │
└──────────────────────┬──────────────────────────────────┘
                       │ (HTTP REST API)
┌──────────────────────▼──────────────────────────────────┐
│                    HTTP API Server                       │
│              (C++ Backend - Port 8080)                   │
└──┬──────────────────────┬──────────────────┬────────────┘
   │                      │                  │
   ▼                      ▼                  ▼
[Database]         [SMS Service]      [QR Service]
  MySQL              Twilio/Local       libqrencode
  8.0+               Gateways           Library
```

### Data Flow

1. **Vehicle Registration** → HTTP API → Database → SMS Service
2. **QR Code Generation** → QR Service → Storage → Frontend
3. **Parking Violation Report** → HTTP API → Notification Queue → SMS Service → User SMS
4. **Vehicle Query** → HTTP API → Hash Table Cache → Database

## 🤝 Contributing

Contributions are welcome! Here's how to contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Guidelines
- Follow C++17 standards
- Write clear, documented code
- Test your changes before submitting
- Update documentation as needed

## 📝 License

This project is licensed under the **MIT License** - see the LICENSE file for details.

## 👥 Authors

- **Park Alert Team** - Initial work and development
- Email: support@parkalert.com

## 🔗 Links

- **Repository**: [github.com/B-max12/car-chime-system](https://github.com/B-max12/car-chime-system)
- **Issues**: [GitHub Issues](https://github.com/B-max12/car-chime-system/issues)
- **Discussions**: [GitHub Discussions](https://github.com/B-max12/car-chime-system/discussions)

## 📞 Support

For support and questions:
- Open an [Issue](https://github.com/B-max12/car-chime-system/issues)
- Check [Discussions](https://github.com/B-max12/car-chime-system/discussions)
- Email: support@parkalert.com

## 🐛 Troubleshooting

### libqrencode not found
```bash
# Install development files
sudo apt-get install libqrencode-dev
```

### CMake not finding MySQL
```bash
# Install MySQL development files
sudo apt-get install libmysqlclient-dev
```

### Build failures on macOS
```bash
# Use Homebrew to install dependencies
brew install mysql-client libqrencode
export LDFLAGS="-L/usr/local/opt/mysql-client/lib"
export CPPFLAGS="-I/usr/local/opt/mysql-client/include"
```

### Port already in use
- Change `HTTP_SERVER_PORT` in configuration
- Or kill existing process: `lsof -i :8080`

---

**Last Updated**: February 2026  
**Status**: Active Development ✅


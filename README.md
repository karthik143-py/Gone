# Secure Wipe App - Cross-Platform Device Security

A comprehensive, enterprise-grade secure wipe application with cross-platform support for Windows and Android devices. Features online coordination through FastAPI servers, advanced wipe algorithms, HPA/DCO detection, multi-device tracking, comprehensive audit logging, and optional blockchain verification for compliance.


TO ACCESS THE APP -> https://drive.google.com/drive/folders/1zPwYieshWUH0PvcxDSc3lqvYnuIh5A-2?usp=drive_link
FOLLOW THE INSTRUCTION PROVIDED 
CONCEPT:->

## 🏗️ Architecture

```
┌─────────────────┐         ┌─────────────────┐
│   Android       │         │   Windows       │
│   Device        │         │   Device        │
│                 │         │                 │
│ ┌─────────────┐ │         │ ┌─────────────┐ │
│ │   Flutter   │ │         │ │   Flutter   │ │
│ │  Frontend   │ │         │ │  Frontend   │ │
│ └─────────────┘ │         │ └─────────────┘ │
│         │       │         │         │       │
│ ┌─────────────┐ │         │ ┌─────────────┐ │
│ │   FastAPI   │ │         │ │   FastAPI   │ │
│ │  Backend    │ │         │ │  Backend    │ │
│ │ (Port 8001) │ │         │ │ (Port 8010) │ │
│ └─────────────┘ │         │ └─────────────┘ │
└─────────────────┘         └─────────────────┘
         │                           │
         └───────────┬───────────────┘
                     │
            ┌─────────────────┐
            │  Central Server │
            │   (Optional)    │
            │   Multi-device  │
            │  Coordination   │
            └─────────────────┘
```

## ✨ Key Features

### 🔒 Security & Compliance
- **Multiple Wipe Algorithms**: DoD 5220.22-M, NIST 800-88, Gutmann 35-pass, Random data overwrite
- **HPA/DCO Detection**: Hidden Protected Area and Device Configuration Overlay handling
- **Admin Privilege Management**: Secure privilege escalation for system-level operations
- **Audit Logging**: Comprehensive logging with optional blockchain verification
- **JWT Authentication**: Secure token-based authentication with bcrypt password hashing

### 🚀 Cross-Platform Support
- **Windows Desktop**: Native Windows application with admin privilege handling
- **Android Mobile**: Native Android app with Device Admin API integration
- **Flutter Frontends**: Modern, responsive UI for both platforms
- **Platform-Specific Optimizations**: Tailored wipe engines for each platform

### 🔄 Advanced Operations
- **Scheduled Wipes**: Immediate or future wipe scheduling with APScheduler
- **Dry-Run Mode**: Safe testing without data destruction
- **Multi-Device Tracking**: Real-time device coordination and status monitoring
- **Remote Wipe Operations**: Cross-device wipe coordination
- **WebSocket Support**: Real-time notifications and status updates

### 🐳 Deployment & Scalability
- **Docker Support**: Containerized deployment with Docker Compose
- **Cloud Ready**: Production-ready configuration with environment variables
- **Health Monitoring**: Built-in health checks and monitoring endpoints
- **Scalable Architecture**: Microservices architecture for enterprise deployment

## 🛠️ Tech Stack

### Backend Technologies
- **FastAPI**: High-performance Python web framework
- **SQLAlchemy**: Database ORM with SQLite (local) and PostgreSQL (server)
- **JWT + bcrypt**: Secure authentication and password hashing
- **WebSockets**: Real-time communication
- **APScheduler**: Task scheduling and automation
- **Web3.py**: Blockchain integration for compliance

### Frontend Technologies
- **Flutter**: Cross-platform UI framework
- **Material Design**: Modern Android UI components
- **Windows Desktop**: Native Windows application support
- **Provider**: State management
- **HTTP Client**: API communication

### Platform-Specific Libraries
- **Windows**: `pywin32` for Windows API integration
- **Android**: `pyjnius`, `kivy` for Android-specific operations
- **File Operations**: `path_provider`, `file_picker` for cross-platform file handling

## 🚀 Quick Start

### Prerequisites
- **Python 3.9+** with pip
- **Flutter SDK** (latest stable version)
- **Docker & Docker Compose** (for containerized deployment)
- **Git** for version control

### Local Development Setup

#### 1. Clone the Repository
```bash
git clone <repository-url>
cd datawiping
```

#### 2. Backend Setup

**Windows Backend:**
```bash
cd backend_windows
pip install -r requirements.txt
python -m uvicorn app.main:app --host 0.0.0.0 --port 8010 --reload
```

**Android Backend:**
```bash
cd backend_android
pip install -r requirements.txt
python -m uvicorn app.main:app --host 0.0.0.0 --port 8001 --reload
```

#### 3. Frontend Setup

**Windows Frontend:**
```bash
cd frontend_windows
flutter pub get
flutter run -d windows
```

**Android Frontend:**
```bash
cd frontend_android
flutter pub get
flutter run -d android
```

### 🐳 Docker Deployment

#### Prerequisites
- Docker 24+
- Docker Compose v2

#### Build and Run
```bash
# Build all services
docker compose build

# Start services in background
docker compose up -d

# View logs
docker compose logs -f
```

#### Service Endpoints
- **Android Backend**: `http://localhost:8001/` (health: `/health`)
- **Windows Backend**: `http://localhost:8010/` (health: `/health`)

#### Configuration
Create `.env` files in backend directories to override defaults:
```bash
# backend_android/.env
SECRET_KEY=your-secret-key-here
LOG_LEVEL=INFO
DRY_RUN_ENABLED=true
HPA_DCO_DETECTION_ENABLED=true
```

## 📱 Building Applications

### Android APK
```bash
cd frontend_android
flutter build apk --release
# Output: build/app/outputs/flutter-apk/app-release.apk
```

### Windows Executable
```bash
cd frontend_windows
flutter build windows --release
# Output: build/windows/runner/Release/
```

### Backend Executables
```bash
# Windows Backend
cd backend_windows
pyinstaller --onefile app/main.py --name SecureWipeApp-Windows

# Android Backend
cd backend_android
pyinstaller --onefile app/main.py --name SecureWipeApp-Android
```

## 🔧 Configuration

### Environment Variables

#### Backend Configuration
| Variable | Description | Default |
|----------|-------------|---------|
| `SECRET_KEY` | JWT secret key | `change-this-in-production` |
| `LOG_LEVEL` | Logging level | `INFO` |
| `DRY_RUN_ENABLED` | Enable dry-run mode | `true` |
| `HPA_DCO_DETECTION_ENABLED` | Enable HPA/DCO detection | `true` |
| `WEBSOCKET_ENABLED` | Enable WebSocket support | `true` |
| `DEVICE_ADMIN_ENABLED` | Enable device admin (Android) | `true` |
| `ROOT_REQUIRED_FOR_SYSTEM_WIPE` | Require root for system wipe | `true` |

#### Database Configuration
| Variable | Description | Default |
|----------|-------------|---------|
| `DATABASE_URL` | Database connection string | `sqlite:///./secure_wipe_[platform].db` |
| `POSTGRES_URL` | PostgreSQL URL (server) | `postgresql://user:pass@localhost/db` |

## 📚 API Documentation

### Interactive Documentation
- **Windows Backend**: `http://localhost:8010/docs`
- **Android Backend**: `http://localhost:8001/docs`

### Key Endpoints

#### Authentication
- `POST /auth/login` - User login
- `POST /auth/register` - User registration
- `POST /auth/refresh` - Token refresh

#### Device Management
- `GET /devices/` - List devices
- `POST /devices/register` - Register device
- `PUT /devices/{device_id}` - Update device
- `DELETE /devices/{device_id}` - Remove device

#### Wipe Operations
- `POST /wipe/start` - Start wipe operation
- `GET /wipe/status/{operation_id}` - Get wipe status
- `POST /wipe/schedule` - Schedule wipe operation
- `POST /wipe/cancel` - Cancel wipe operation

#### Audit & Logging
- `GET /audit/logs` - Get audit logs
- `POST /audit/verify` - Verify blockchain certificate

## 🔒 Security Considerations

This application handles sensitive data destruction operations. Please review the security documentation:

- **[SECURITY.md](docs/SECURITY.md)** - Security guidelines and best practices
- **[AUDIT_GUIDE.md](docs/AUDIT_GUIDE.md)** - Audit and compliance information
- **[WORKFLOW.md](docs/WORKFLOW.md)** - Operational workflows

### Production Deployment Checklist
- [ ] Change default `SECRET_KEY` values
- [ ] Configure HTTPS reverse proxy
- [ ] Restrict CORS and TrustedHost settings
- [ ] Set up proper logging and monitoring
- [ ] Configure database backups
- [ ] Enable audit logging
- [ ] Set up blockchain integration (if required)

## 🧪 Testing

### Running Tests
```bash
# Backend tests
cd backend_windows && python -m pytest
cd backend_android && python -m pytest

# Frontend tests
cd frontend_windows && flutter test
cd frontend_android && flutter test
```

### Test Coverage
- Unit tests for all backend services
- Integration tests for API endpoints
- Frontend widget tests
- End-to-end testing scenarios

## 📖 Development Workflow

### Project Structure
```
datawiping/
├── backend_android/          # Android backend service
│   ├── app/                  # FastAPI application
│   ├── Dockerfile           # Container configuration
│   └── requirements.txt     # Python dependencies
├── backend_windows/          # Windows backend service
│   ├── app/                  # FastAPI application
│   ├── Dockerfile           # Container configuration
│   └── requirements.txt     # Python dependencies
├── frontend_android/         # Android Flutter app
│   ├── lib/                  # Dart source code
│   └── pubspec.yaml         # Flutter dependencies
├── frontend_windows/         # Windows Flutter app
│   ├── lib/                  # Dart source code
│   └── pubspec.yaml         # Flutter dependencies
├── docs/                     # Documentation
├── scripts/                  # Utility scripts
├── tests/                    # Integration tests
└── docker-compose.yml       # Container orchestration
```

### Development Commands
```bash
# Start all services for development
docker compose up -d

# Run specific backend
cd backend_windows && python -m uvicorn app.main:app --reload

# Run Flutter app
cd frontend_android && flutter run

# Build release versions
cd frontend_android && flutter build apk --release
cd frontend_windows && flutter build windows --release
```

## 🤝 Contributing

We welcome contributions! Please follow these guidelines:

1. **Fork the repository** and create a feature branch
2. **Follow the coding standards** and add tests for new features
3. **Update documentation** for any API or configuration changes
4. **Submit a pull request** with a clear description of changes

### Development Setup
1. Set up local development environment
2. Run tests to ensure everything works
3. Make your changes with proper test coverage
4. Update documentation as needed
5. Submit pull request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

- **Documentation**: Check the `docs/` directory for detailed guides
- **Issues**: Report bugs and feature requests via GitHub Issues
- **Security**: Report security vulnerabilities privately to the maintainers

## 🎯 Roadmap

### Upcoming Features
- [ ] iOS support
- [ ] Enhanced blockchain integration
- [ ] Advanced scheduling options
- [ ] Multi-language support
- [ ] Enhanced reporting and analytics

### Known Limitations
- Android app requires Device Admin permissions
- Windows app requires administrator privileges for system-level operations
- Blockchain integration is optional and requires external setup

---

**⚠️ Important**: This application performs irreversible data destruction operations. Always test in dry-run mode first and ensure you have proper backups before running actual wipe operations.
# Gone

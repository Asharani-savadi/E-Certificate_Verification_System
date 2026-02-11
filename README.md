# E-Certificate Verification System

A comprehensive digital certificate verification platform built with React, Node.js (Express), and MySQL. The system enables institutions to issue, manage, and verify digital certificates with comprehensive role-based access control, JWT authentication, and secure password management.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Architecture & Modules](#architecture--modules)
- [Tech Stack](#tech-stack)
- [Installation & Setup](#installation--setup)
- [Database Schema](#database-schema)
- [API Documentation](#api-documentation)
- [Authentication & Authorization](#authentication--authorization)
- [Business Rules](#business-rules)
- [Project Structure](#project-structure)
- [Running the Application](#running-the-application)
- [Contributing](#contributing)
- [License](#license)

## 📖 Overview

The E-Certificate Verification System is a secure, scalable platform that streamlines the process of issuing, managing, and verifying digital certificates. With role-based access control and comprehensive audit trails, the system ensures that only authorized institutions can issue certificates and that verification processes are transparent and trustworthy.

### Key Use Cases:
- Educational institutions issuing graduation certificates
- Professional organizations issuing certifications
- Corporate training programs issuing completion certificates
- Government bodies issuing credentials
- Third-party verification of issued certificates

## ✨ Features

### Core Features
- **Secure Authentication**: JWT-based authentication with refreshable tokens
- **Role-Based Access Control (RBAC)**: Three user roles (Admin, Institution, User) with granular permissions
- **Certificate Management**: Full CRUD operations for digital certificates
- **Template Management**: Reusable certificate templates for institutions
- **Institution Verification**: Only approved institutions can issue certificates
- **Certificate Verification**: Public verification endpoint for certificate authenticity
- **Certificate Revocation**: Revoked certificates cannot be verified
- **User Account Management**: Complete user lifecycle management

### Security Features
- **Password Hashing**: bcrypt for secure password storage
- **JWT Tokens**: Secure token-based authentication with expiration
- **Role-Based Endpoints**: Protected routes based on user roles
- **Input Validation**: Comprehensive data validation
- **Error Handling**: Centralized error handling and logging
- **CORS Protection**: Cross-origin request handling

### Admin Module
- Dashboard with system statistics
- User management (create, update, delete, list)
- Institution management and approval
- Certificate monitoring
- System audit logs
- Reports and analytics

### Institution Module
- Manage institutional profile
- Issue certificates to users
- View issued certificates
- Manage certificate templates
- Revoke certificates if needed
- View verification requests

### User Module
- Register and manage account
- View issued certificates
- Download certificates
- Share certificate verification link
- View personal dashboard

### Auth Module
- User registration (User role)
- Institution registration (Institution role)
- Admin login
- JWT token generation and validation
- Token refresh functionality
- Password reset functionality
- Email verification (optional)

### Verification Module
- Public certificate verification endpoint
- Verify certificate authenticity
- Check certificate status (active, revoked, expired)
- Detailed certificate information
- Verification audit trail

## 🏗️ Architecture & Modules

### Module Breakdown

```
┌─────────────────────────────────────────────────┐
│         Frontend (React)                         │
│  ┌──────────────────────────────────────────┐   │
│  │  Admin Dashboard | Institution Portal    │   │
│  │  User Dashboard | Public Verification    │   │
│  └──────────────────────────────────────────┘   │
└─────────────────────────────────────────────────┘
                       ↓ REST APIs
┌─────────────────────────────────────────────────┐
│         Backend (Node.js/Express)               │
│  ┌────────────┬────────────┬────────────────┐   │
│  │   Auth     │  Users     │  Institutions  │   │
│  │  Module    │  Module    │  Module        │   │
│  └────────────┴────────────┴────────────────┘   │
│  ┌────────────┬────────────┬────────────────┐   │
│  │Certificates│ Verification│  Templates    │   │
│  │  Module    │   Module   │  Module        │   │
│  └────────────┴────────────┴────────────────┘   │
└─────────────────────────────────────────────────┘
                       ↓
┌─────────────────────────────────────────────────┐
│         Database (MySQL)                         │
│  ┌──────────────────────────────────────────┐   │
│  │ Users | Institutions | Certificates     │   │
│  │ Templates | Roles | Audit Logs          │   │
│  └──────────────────────────────────────────┘   │
└─────────────────────────────────────────────────┘
```

### Module Responsibilities

| Module | Responsibility |
|--------|-----------------|
| **Auth** | User registration, login, JWT token management, password hashing |
| **Users** | User profile management, user data CRUD operations |
| **Institutions** | Institution registration, approval, profile management |
| **Certificates** | Certificate issuance, storage, revocation, retrieval |
| **Templates** | Certificate template creation, management, reusability |
| **Verification** | Public certificate verification, authenticity validation |

## 🛠️ Tech Stack

### Frontend
- **React** 18.x - UI library
- **React Router** - Client-side routing
- **Axios** - HTTP client
- **Material-UI / Tailwind CSS** - UI framework
- **Redux** (optional) - State management

### Backend
- **Node.js** 16.x+ - Runtime environment
- **Express** 4.x - Web framework
- **JWT** (jsonwebtoken) - Authentication
- **bcrypt** - Password hashing
- **Dotenv** - Environment variables
- **Cors** - Cross-origin handling
- **Express-validator** - Input validation

### Database
- **MySQL** 8.x - Relational database
- **Sequelize** or **Knex.js** - ORM/Query builder

### Development Tools
- **Postman** - API testing
- **MySQL Workbench** - Database management
- **VS Code** - Code editor
- **Git** - Version control

## 📦 Installation & Setup

### Prerequisites
- Node.js (v16 or higher)
- npm or yarn
- MySQL Server (v8.0 or higher)
- Git

### Backend Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/E-Certificate_Verification_System.git
   cd E-Certificate_Verification_System
   ```

2. **Install backend dependencies**
   ```bash
   cd backend
   npm install
   ```

3. **Create environment file**
   ```bash
   cp .env.example .env
   ```

4. **Configure environment variables**
   ```env
   # Server Configuration
   PORT=5000
   NODE_ENV=development
   
   # Database Configuration
   DB_HOST=localhost
   DB_PORT=3306
   DB_USER=root
   DB_PASSWORD=your_password
   DB_NAME=ecertificate_db
   
   # JWT Configuration
   JWT_SECRET=your_jwt_secret_key_here
   JWT_EXPIRE=7d
   JWT_REFRESH_SECRET=your_refresh_secret_key
   JWT_REFRESH_EXPIRE=30d
   
   # Email Configuration (Optional)
   EMAIL_USER=your_email@gmail.com
   EMAIL_PASS=your_email_password
   SMTP_HOST=smtp.gmail.com
   SMTP_PORT=587
   
   # App Configuration
   APP_URL=http://localhost:3000
   API_BASE_URL=http://localhost:5000/api
   ```

5. **Create and configure MySQL database**
   ```bash
   mysql -u root -p
   CREATE DATABASE ecertificate_db;
   USE ecertificate_db;
   ```

6. **Run database migrations** (if using migration scripts)
   ```bash
   npm run migrate
   ```

7. **Start the backend server**
   ```bash
   npm start
   # or for development with auto-reload
   npm run dev
   ```

### Frontend Setup

1. **Navigate to frontend directory**
   ```bash
   cd frontend
   npm install
   ```

2. **Create environment file**
   ```bash
   cp .env.example .env
   ```

3. **Configure environment variables**
   ```env
   REACT_APP_API_BASE_URL=http://localhost:5000/api
   REACT_APP_APP_NAME="E-Certificate Verification System"
   ```

4. **Start the React development server**
   ```bash
   npm start
   ```

The application will open at `http://localhost:3000`

## 🗄️ Database Schema

### Tables Overview

#### 1. **users** table
```sql
CREATE TABLE users (
  id INT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(255) NOT NULL,
  email VARCHAR(255) UNIQUE NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  role ENUM('admin', 'institution', 'user') DEFAULT 'user',
  institution_id INT,
  is_active BOOLEAN DEFAULT TRUE,
  is_verified BOOLEAN DEFAULT FALSE,
  verification_token VARCHAR(255),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  FOREIGN KEY (institution_id) REFERENCES institutions(id),
  INDEX idx_email (email),
  INDEX idx_role (role)
);
```

#### 2. **institutions** table
```sql
CREATE TABLE institutions (
  id INT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(255) NOT NULL UNIQUE,
  email VARCHAR(255) NOT NULL,
  phone VARCHAR(20),
  address TEXT,
  city VARCHAR(100),
  state VARCHAR(100),
  country VARCHAR(100),
  postal_code VARCHAR(20),
  website VARCHAR(255),
  license_number VARCHAR(255) UNIQUE,
  is_approved BOOLEAN DEFAULT FALSE,
  is_active BOOLEAN DEFAULT TRUE,
  approval_date DATETIME,
  approved_by INT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  FOREIGN KEY (approved_by) REFERENCES users(id),
  INDEX idx_name (name),
  INDEX idx_approved (is_approved)
);
```

#### 3. **certificates** table
```sql
CREATE TABLE certificates (
  id INT PRIMARY KEY AUTO_INCREMENT,
  certificate_id VARCHAR(255) UNIQUE NOT NULL,
  institution_id INT NOT NULL,
  user_id INT NOT NULL,
  template_id INT NOT NULL,
  title VARCHAR(255) NOT NULL,
  description TEXT,
  issue_date DATE NOT NULL,
  expiry_date DATE,
  is_revoked BOOLEAN DEFAULT FALSE,
  revoke_reason TEXT,
  revoked_at DATETIME,
  revoked_by INT,
  verification_count INT DEFAULT 0,
  file_path VARCHAR(255),
  certificate_data JSON,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  FOREIGN KEY (institution_id) REFERENCES institutions(id),
  FOREIGN KEY (user_id) REFERENCES users(id),
  FOREIGN KEY (template_id) REFERENCES templates(id),
  FOREIGN KEY (revoked_by) REFERENCES users(id),
  INDEX idx_certificate_id (certificate_id),
  INDEX idx_user_id (user_id),
  INDEX idx_institution_id (institution_id),
  INDEX idx_is_revoked (is_revoked)
);
```

#### 4. **templates** table
```sql
CREATE TABLE templates (
  id INT PRIMARY KEY AUTO_INCREMENT,
  institution_id INT NOT NULL,
  name VARCHAR(255) NOT NULL,
  description TEXT,
  html_template LONGTEXT NOT NULL,
  css_styles LONGTEXT,
  fields JSON,
  is_active BOOLEAN DEFAULT TRUE,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  FOREIGN KEY (institution_id) REFERENCES institutions(id),
  INDEX idx_institution_id (institution_id)
);
```

#### 5. **audit_logs** table
```sql
CREATE TABLE audit_logs (
  id INT PRIMARY KEY AUTO_INCREMENT,
  user_id INT,
  action VARCHAR(255) NOT NULL,
  entity_type VARCHAR(100),
  entity_id INT,
  changes JSON,
  ip_address VARCHAR(45),
  user_agent TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (user_id) REFERENCES users(id),
  INDEX idx_user_id (user_id),
  INDEX idx_action (action)
);
```

#### 6. **verification_logs** table
```sql
CREATE TABLE verification_logs (
  id INT PRIMARY KEY AUTO_INCREMENT,
  certificate_id INT NOT NULL,
  verified_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  ip_address VARCHAR(45),
  user_agent TEXT,
  status ENUM('valid', 'revoked', 'expired', 'not_found') NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (certificate_id) REFERENCES certificates(id),
  INDEX idx_certificate_id (certificate_id),
  INDEX idx_status (status)
);
```

## 🔌 API Documentation

### Base URL
```
http://localhost:5000/api
```

### Authentication Endpoints

#### 1. Register User
```
POST /auth/register
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "SecurePassword123!"
}

Response (201):
{
  "success": true,
  "message": "User registered successfully",
  "data": {
    "id": 1,
    "name": "John Doe",
    "email": "john@example.com",
    "role": "user"
  }
}
```

#### 2. Register Institution
```
POST /auth/register-institution
Content-Type: application/json

{
  "name": "MIT",
  "email": "admin@mit.edu",
  "password": "SecurePassword123!",
  "phone": "+1-234-567-8900",
  "address": "77 Massachusetts Ave",
  "city": "Cambridge",
  "state": "MA",
  "country": "USA",
  "postal_code": "02139",
  "license_number": "LIC123456"
}

Response (201):
{
  "success": true,
  "message": "Institution registered successfully",
  "data": {
    "id": 1,
    "name": "MIT",
    "email": "admin@mit.edu",
    "is_approved": false
  }
}
```

#### 3. Login
```
POST /auth/login
Content-Type: application/json

{
  "email": "john@example.com",
  "password": "SecurePassword123!"
}

Response (200):
{
  "success": true,
  "message": "Login successful",
  "data": {
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "user": {
      "id": 1,
      "name": "John Doe",
      "email": "john@example.com",
      "role": "user"
    }
  }
}
```

#### 4. Refresh Token
```
POST /auth/refresh
Content-Type: application/json

{
  "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}

Response (200):
{
  "success": true,
  "data": {
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
  }
}
```

### User Endpoints

#### 1. Get All Users (Admin Only)
```
GET /users
Authorization: Bearer <token>

Response (200):
{
  "success": true,
  "data": [
    {
      "id": 1,
      "name": "John Doe",
      "email": "john@example.com",
      "role": "user",
      "is_active": true
    }
  ],
  "pagination": {
    "total": 100,
    "page": 1,
    "limit": 10
  }
}
```

#### 2. Get User by ID
```
GET /users/:id
Authorization: Bearer <token>

Response (200):
{
  "success": true,
  "data": {
    "id": 1,
    "name": "John Doe",
    "email": "john@example.com",
    "role": "user",
    "is_active": true,
    "created_at": "2024-01-15T10:30:00Z"
  }
}
```

#### 3. Update User
```
PUT /users/:id
Authorization: Bearer <token>
Content-Type: application/json

{
  "name": "Jane Doe",
  "phone": "+1-234-567-8900"
}

Response (200):
{
  "success": true,
  "message": "User updated successfully",
  "data": {
    "id": 1,
    "name": "Jane Doe",
    "email": "john@example.com",
    "role": "user"
  }
}
```

#### 4. Delete User (Admin Only)
```
DELETE /users/:id
Authorization: Bearer <token>

Response (200):
{
  "success": true,
  "message": "User deleted successfully"
}
```

### Institution Endpoints

#### 1. Get All Institutions
```
GET /institutions
Authorization: Bearer <token>

Query Parameters:
- approved: boolean (filter by approval status)
- page: number
- limit: number

Response (200):
{
  "success": true,
  "data": [
    {
      "id": 1,
      "name": "MIT",
      "email": "admin@mit.edu",
      "is_approved": true,
      "is_active": true,
      "created_at": "2024-01-10T10:30:00Z"
    }
  ]
}
```

#### 2. Get Institution by ID
```
GET /institutions/:id
Authorization: Bearer <token>

Response (200):
{
  "success": true,
  "data": {
    "id": 1,
    "name": "MIT",
    "email": "admin@mit.edu",
    "phone": "+1-234-567-8900",
    "address": "77 Massachusetts Ave",
    "city": "Cambridge",
    "state": "MA",
    "country": "USA",
    "license_number": "LIC123456",
    "is_approved": true,
    "is_active": true
  }
}
```

#### 3. Approve Institution (Admin Only)
```
PUT /institutions/:id/approve
Authorization: Bearer <token>
Content-Type: application/json

{}

Response (200):
{
  "success": true,
  "message": "Institution approved successfully",
  "data": {
    "id": 1,
    "name": "MIT",
    "is_approved": true,
    "approval_date": "2024-01-20T10:30:00Z"
  }
}
```

### Certificate Endpoints

#### 1. Issue Certificate (Institution Only)
```
POST /certificates
Authorization: Bearer <token>
Content-Type: application/json

{
  "user_id": 5,
  "template_id": 1,
  "title": "Bachelor of Computer Science",
  "description": "Degree completion certificate",
  "issue_date": "2024-01-20",
  "expiry_date": "2034-01-20"
}

Response (201):
{
  "success": true,
  "message": "Certificate issued successfully",
  "data": {
    "id": 1,
    "certificate_id": "CERT-MIT-2024-001",
    "user_id": 5,
    "institution_id": 1,
    "title": "Bachelor of Computer Science",
    "issue_date": "2024-01-20",
    "is_revoked": false
  }
}
```

#### 2. Get All Certificates
```
GET /certificates
Authorization: Bearer <token>

Query Parameters:
- institution_id: number
- user_id: number
- is_revoked: boolean
- page: number
- limit: number

Response (200):
{
  "success": true,
  "data": [
    {
      "id": 1,
      "certificate_id": "CERT-MIT-2024-001",
      "title": "Bachelor of Computer Science",
      "institution_id": 1,
      "user_id": 5,
      "issue_date": "2024-01-20",
      "is_revoked": false
    }
  ]
}
```

#### 3. Get Certificate by ID
```
GET /certificates/:id
Authorization: Bearer <token>

Response (200):
{
  "success": true,
  "data": {
    "id": 1,
    "certificate_id": "CERT-MIT-2024-001",
    "title": "Bachelor of Computer Science",
    "institution_id": 1,
    "user_id": 5,
    "issue_date": "2024-01-20",
    "expiry_date": "2034-01-20",
    "is_revoked": false,
    "verification_count": 42
  }
}
```

#### 4. Update Certificate (Institution Only)
```
PUT /certificates/:id
Authorization: Bearer <token>
Content-Type: application/json

{
  "title": "Master of Computer Science",
  "description": "Updated degree certificate"
}

Response (200):
{
  "success": true,
  "message": "Certificate updated successfully",
  "data": {
    "id": 1,
    "certificate_id": "CERT-MIT-2024-001",
    "title": "Master of Computer Science"
  }
}
```

#### 5. Revoke Certificate (Institution Only)
```
PUT /certificates/:id/revoke
Authorization: Bearer <token>
Content-Type: application/json

{
  "reason": "Certificate issued by mistake"
}

Response (200):
{
  "success": true,
  "message": "Certificate revoked successfully",
  "data": {
    "id": 1,
    "certificate_id": "CERT-MIT-2024-001",
    "is_revoked": true,
    "revoke_reason": "Certificate issued by mistake"
  }
}
```

#### 6. Delete Certificate (Admin Only)
```
DELETE /certificates/:id
Authorization: Bearer <token>

Response (200):
{
  "success": true,
  "message": "Certificate deleted successfully"
}
```

### Verification Endpoints

#### 1. Verify Certificate (Public - No Auth Required)
```
GET /verify/:certificate_id
Content-Type: application/json

Response (200):
{
  "success": true,
  "data": {
    "certificate_id": "CERT-MIT-2024-001",
    "title": "Bachelor of Computer Science",
    "institution_name": "MIT",
    "user_name": "John Doe",
    "issue_date": "2024-01-20",
    "expiry_date": "2034-01-20",
    "is_valid": true,
    "status": "active",
    "verified_at": "2024-01-25T14:30:00Z"
  }
}
```

#### 2. Get Certificate Verification History (Admin/Institution)
```
GET /verification-logs/:certificate_id
Authorization: Bearer <token>

Response (200):
{
  "success": true,
  "data": [
    {
      "id": 1,
      "certificate_id": 1,
      "verified_at": "2024-01-25T14:30:00Z",
      "status": "valid",
      "ip_address": "192.168.1.1"
    }
  ]
}
```

### Template Endpoints

#### 1. Create Template (Institution Only)
```
POST /templates
Authorization: Bearer <token>
Content-Type: application/json

{
  "name": "Bachelor Degree",
  "description": "Standard bachelor degree template",
  "html_template": "<html>...</html>",
  "css_styles": "body { font-family: Arial; }",
  "fields": ["name", "degree", "issue_date"]
}

Response (201):
{
  "success": true,
  "message": "Template created successfully",
  "data": {
    "id": 1,
    "name": "Bachelor Degree",
    "institution_id": 1,
    "is_active": true
  }
}
```

#### 2. Get All Templates (Institution Only)
```
GET /templates
Authorization: Bearer <token>

Response (200):
{
  "success": true,
  "data": [
    {
      "id": 1,
      "name": "Bachelor Degree",
      "description": "Standard bachelor degree template",
      "is_active": true
    }
  ]
}
```

#### 3. Update Template (Institution Only)
```
PUT /templates/:id
Authorization: Bearer <token>
Content-Type: application/json

{
  "name": "Updated Bachelor Degree"
}

Response (200):
{
  "success": true,
  "message": "Template updated successfully"
}
```

#### 4. Delete Template (Institution Only)
```
DELETE /templates/:id
Authorization: Bearer <token>

Response (200):
{
  "success": true,
  "message": "Template deleted successfully"
}
```

## 🔐 Authentication & Authorization

### JWT Token Structure

**Access Token** (expires in 7 days):
```json
{
  "id": 1,
  "email": "john@example.com",
  "role": "user",
  "institution_id": 1,
  "iat": 1674067200,
  "exp": 1674672000
}
```

**Refresh Token** (expires in 30 days):
```json
{
  "id": 1,
  "email": "john@example.com",
  "iat": 1674067200,
  "exp": 1676659200
}
```

### Role-Based Access Control (RBAC)

| Feature | Admin | Institution | User |
|---------|-------|-------------|------|
| Manage Users | ✅ | ❌ | ❌ |
| Approve Institutions | ✅ | ❌ | ❌ |
| Issue Certificates | ❌ | ✅ | ❌ |
| Revoke Certificates | ❌ | ✅ | ❌ |
| View Own Certificates | ✅ | ✅ | ✅ |
| Verify Certificates | ✅ | ✅ | ✅ |
| Create Templates | ❌ | ✅ | ❌ |
| View Audit Logs | ✅ | ❌ | ❌ |
| Delete Certificates | ✅ | ❌ | ❌ |

### Authentication Flow

```
1. User/Institution registers via /auth/register
2. Request access via /auth/login with credentials
3. Server validates credentials and returns JWT tokens
4. Client stores accessToken and refreshToken
5. Client adds accessToken to Authorization header: "Bearer <token>"
6. Server validates token on each request
7. On token expiry, client uses refreshToken to get new accessToken
8. User logs out by deleting stored tokens
```

### Password Security

All passwords are hashed using **bcrypt** with a salt round of 10:

```javascript
const hashedPassword = await bcrypt.hash(plainPassword, 10);
const isPasswordValid = await bcrypt.compare(plainPassword, hashedPassword);
```

## 📋 Business Rules

### Certificate Rules

1. **Unique Certificate ID**
   - Format: `CERT-{INSTITUTION_CODE}-{YEAR}-{SEQUENCE}`
   - Example: `CERT-MIT-2024-001`
   - Must be globally unique across the system
   - Cannot be duplicated or reused

2. **Institution Approval**
   - Only approved institutions can issue certificates
   - New institution registrations require admin approval
   - Unauthorized institutions cannot create certificates
   - Attempting to issue from unapproved institution returns error

3. **Certificate Revocation**
   - Revoked certificates show status "revoked" in verification
   - Revoked certificates cannot be modified
   - Revocation requires a reason to be documented
   - Revocation is permanent and tracked in audit logs

4. **Certificate Expiry**
   - Optional expiry date can be set during issuance
   - Expired certificates show status "expired" in verification
   - Users receive notifications before expiry (if implemented)
   - Expired certificates can still be verified but show expiry status

5. **Certificate Verification**
   - Public verification endpoint accessible without authentication
   - Verification logs track all verification requests
   - Returns certificate status: active, revoked, or expired
   - Includes institution name, issue date, and expiry date

### User Rules

1. **Registration**
   - Email must be unique
   - Password must meet complexity requirements
   - User role is assigned during registration
   - Email verification may be required

2. **User Roles**
   - **Admin**: System administrator with full access
   - **Institution**: Organization issuing certificates
   - **User**: Individual receiving certificates

3. **Access Control**
   - Users can only access their own data
   - Institutions can only manage their own certificates
   - Admins have system-wide access

### Institution Rules

1. **Registration**
   - Requires unique license number
   - Requires valid contact information
   - Must be approved by admin before issuing
   - Approval status tracked with approval date

2. **Certificate Issuance**
   - Only approved institutions can issue
   - Can only issue to registered users
   - Must use valid templates
   - Automatic audit trail creation

## 📁 Project Structure

```
E-Certificate_Verification_System/
├── backend/
│   ├── config/
│   │   ├── database.js
│   │   └── environment.js
│   ├── controllers/
│   │   ├── authController.js
│   │   ├── userController.js
│   │   ├── institutionController.js
│   │   ├── certificateController.js
│   │   ├── templateController.js
│   │   └── verificationController.js
│   ├── models/
│   │   ├── User.js
│   │   ├── Institution.js
│   │   ├── Certificate.js
│   │   ├── Template.js
│   │   ├── AuditLog.js
│   │   └── VerificationLog.js
│   ├── routes/
│   │   ├── authRoutes.js
│   │   ├── userRoutes.js
│   │   ├── institutionRoutes.js
│   │   ├── certificateRoutes.js
│   │   ├── templateRoutes.js
│   │   └── verificationRoutes.js
│   ├── middleware/
│   │   ├── authenticate.js
│   │   ├── authorize.js
│   │   ├── errorHandler.js
│   │   └── validation.js
│   ├── utils/
│   │   ├── generateCertificateId.js
│   │   ├── tokenUtils.js
│   │   ├── emailService.js
│   │   └── logger.js
│   ├── .env.example
│   ├── app.js
│   ├── server.js
│   └── package.json
│
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── Auth/
│   │   │   │   ├── Login.js
│   │   │   │   ├── Register.js
│   │   │   │   └── RegisterInstitution.js
│   │   │   ├── Admin/
│   │   │   │   ├── Dashboard.js
│   │   │   │   ├── UserManagement.js
│   │   │   │   ├── InstitutionApproval.js
│   │   │   │   └── AuditLogs.js
│   │   │   ├── Institution/
│   │   │   │   ├── Dashboard.js
│   │   │   │   ├── IssueCertificate.js
│   │   │   │   ├── ManageCertificates.js
│   │   │   │   └── ManageTemplates.js
│   │   │   ├── User/
│   │   │   │   ├── Dashboard.js
│   │   │   │   ├── MyCertificates.js
│   │   │   │   └── Profile.js
│   │   │   ├── Public/
│   │   │   │   ├── Verification.js
│   │   │   │   └── VerificationResult.js
│   │   │   └── Common/
│   │   │       ├── Navbar.js
│   │   │       ├── Sidebar.js
│   │   │       └── ProtectedRoute.js
│   │   ├── services/
│   │   │   ├── authService.js
│   │   │   ├── userService.js
│   │   │   ├── institutionService.js
│   │   │   ├── certificateService.js
│   │   │   ├── templateService.js
│   │   │   └── verificationService.js
│   │   ├── pages/
│   │   │   ├── LoginPage.js
│   │   │   ├── AdminDashboard.js
│   │   │   ├── InstitutionDashboard.js
│   │   │   ├── UserDashboard.js
│   │   │   └── PublicVerification.js
│   │   ├── App.js
│   │   ├── index.js
│   │   └── App.css
│   ├── public/
│   │   └── index.html
│   ├── .env.example
│   ├── package.json
│   └── README.md
│
├── docs/
│   ├── API_DOCUMENTATION.md
│   ├── DATABASE_SCHEMA.md
│   ├── INSTALLATION.md
│   └── DEPLOYMENT.md
│
├── .gitignore
├── README.md
└── package.json
```

## 🚀 Running the Application

### Development Mode

1. **Terminal 1 - Start Backend Server**
   ```bash
   cd backend
   npm run dev
   # Server running on http://localhost:5000
   ```

2. **Terminal 2 - Start Frontend Development Server**
   ```bash
   cd frontend
   npm start
   # Application running on http://localhost:3000
   ```

### Production Mode

1. **Build Frontend**
   ```bash
   cd frontend
   npm run build
   ```

2. **Start Backend in Production**
   ```bash
   cd backend
   NODE_ENV=production npm start
   ```

### Testing

```bash
# Run backend tests
cd backend
npm test

# Run frontend tests
cd frontend
npm test
```

## 🧪 Testing with Postman

1. Import the Postman collection (available in `/docs`)
2. Set up environment variables for your instance
3. Test each endpoint according to role-based access

## 📊 Example Workflows

### Admin Workflow
1. Login as admin
2. Approve pending institutions
3. Monitor certificate issuances
4. View audit logs and analytics
5. Manage users and institutions

### Institution Workflow
1. Register institution (pending approval)
2. Wait for admin approval
3. Create certificate templates
4. Issue certificates to registered users
5. Monitor issued certificates
6. Revoke certificates if needed

### User Workflow
1. Register as user
2. Search for issued certificates
3. View certificate details
4. Share certificate verification link
5. Download certificate (optional)

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Development Guidelines
- Follow the project structure
- Write meaningful commit messages
- Add comments for complex logic
- Test your changes before submitting PR
- Update documentation as needed

## 📞 Support & Contact

For issues, questions, or suggestions:
- Open an issue on GitHub
- Contact the development team
- Check the documentation first

## 🔒 Security Considerations

- Never commit `.env` files
- Rotate JWT secrets regularly
- Use HTTPS in production
- Validate all user inputs
- Use prepared statements to prevent SQL injection
- Implement rate limiting for APIs
- Enable CORS only for trusted domains
- Keep dependencies updated
- Use environment-specific configurations

---

**Last Updated**: February 12, 2026
**Version**: 1.0.0
**Status**: Ready for Development
# Tsinda Backend

## Description
Tsinda Backend is the server-side component of the driving theory learning platform. It provides a robust API for managing users, courses, exams, and content delivery in both English and Kinyarwanda. The backend is built with Node.js, Express.js, and MongoDB, following RESTful API principles and implementing secure authentication mechanisms.

## Figma mockups Designs 
[Figma mockups Designs ](https://www.figma.com/design/kWFcPt7KHLj4x8RpGrmE1B/Tsindacyane-design?node-id=137-1540&t=xxx4bHJQMv6MQDoL-1)

## DEMO Video ||  Tsinda Initial software product/solution demonstration
[Demo Video ](https://youtu.be/5EhafmftfNw)

## GitHub Repository || The Reason why I created two separate repository is to facilitate in the deploymentof the web application
[Link to Frontend Repository](https://github.com/eldadgishinge/tsinda_front_end)

[Link to Backend Repository](https://github.com/eldadgishinge/tsinda---backend)

## Table of Contents
- [Features](#features)
- [Architecture Overview](#architecture-overview)
- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Installation & Setup](#installation--setup)
- [Environment Configuration](#environment-configuration)
- [Database Setup](#database-setup)
- [API Documentation](#api-documentation)
- [Testing](#testing)
- [Development Workflow](#development-workflow)
- [Deployment](#deployment)
- [Security](#security)
- [Performance](#performance)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [Contact](#contact)

## Features
- **User Authentication**: JWT-based authentication with Google OAuth support
- **Multi-language Support**: API endpoints for English and Kinyarwanda content
- **Course Management**: CRUD operations for educational courses
- **Exam System**: Comprehensive exam creation and management
- **File Upload**: Secure file handling with validation
- **Email Integration**: Automated email notifications
- **Real-time Updates**: WebSocket support for live updates
- **Admin Dashboard**: Backend support for admin functionalities
- **Progress Tracking**: User progress and assessment tracking
- **Content Management**: Dynamic content delivery system

## Architecture Overview
The backend follows the MVC (Model-View-Controller) architecture pattern:

```
src/
├── controllers/     # Business logic handlers
├── models/         # Database schemas and models
├── routes/         # API endpoint definitions
├── middleware/     # Custom middleware functions
├── services/       # Reusable business logic
├── config/         # Configuration files
├── tests/          # Test files
└── app.js          # Main application entry point
```

### Key Components:
- **Models**: Mongoose schemas that define the data structure
- **Controllers**: Handle business logic and API responses
- **Routes**: Define API endpoints and connect them to controllers
- **Middleware**: Handle cross-cutting concerns like authentication and validation
- **Services**: Contain reusable business logic

## Tech Stack

### Core Technologies
- **Node.js** (v18+) - JavaScript runtime
- **Express.js** (v4.18+) - Web application framework
- **MongoDB** (v6+) - NoSQL database
- **Mongoose** (v7+) - MongoDB object modeling

### Authentication & Security
- **JWT** (jsonwebtoken) - Token-based authentication
- **Passport.js** - Authentication middleware
- **bcryptjs** - Password hashing
- **express-validator** - Input validation
- **cors** - Cross-origin resource sharing

### File Handling
- **Multer** - File upload middleware
- **uuid** - Unique identifier generation
- **Cloudinary** - Cloud file storage

### Development Tools
- **nodemon** - Development server with auto-restart
- **dotenv** - Environment variable management
- **express-session** - Session management

### Testing
- **Jest** - Testing framework
- **Supertest** - HTTP assertion library
- **mongodb-memory-server** - In-memory MongoDB for testing

### Email Services
- **Nodemailer** - Email sending functionality

## Prerequisites

Before setting up the backend, ensure you have the following installed:

### Required Software
- **Node.js** (v18.0.0 or higher)
  ```bash
  # Check Node.js version
  node --version
  ```
- **npm** (v8.0.0 or higher)
  ```bash
  # Check npm version
  npm --version
  ```
- **MongoDB** (v6.0 or higher)
  ```bash
  # For Ubuntu/Debian
  sudo apt-get install mongodb
  
  # For macOS (using Homebrew)
  brew install mongodb/brew/mongodb-community
  
  # For Windows
  # Download from https://www.mongodb.com/try/download/community
  ```

### Optional but Recommended
- **Git** - Version control
- **Postman** or **Insomnia** - API testing
- **MongoDB Compass** - Database GUI
- **VS Code** - Code editor with Node.js extensions

## Installation & Setup

### Step 1: Clone the Repository
```bash
# Clone the backend repository
git clone https://github.com/eldadgishinge/tsinda---backend.git

# Navigate to the project directory
cd tsinda---backend
```

### Step 2: Install Dependencies
```bash
# Install all dependencies
npm install

# Or if you prefer yarn
yarn install
```

### Step 3: Environment Configuration
```bash
# Copy the environment example file
cp env.example .env

# Edit the .env file with your configuration
nano .env
```

### Step 4: Database Setup
```bash
# Start MongoDB service
# Ubuntu/Debian
sudo systemctl start mongod

# macOS
brew services start mongodb/brew/mongodb-community

# Windows
# MongoDB should start automatically as a service
```

### Step 5: Start the Development Server
```bash
# Start the development server
npm run dev

# The server will start on http://localhost:5000
```

## Environment Configuration

Create a `.env` file in the root directory with the following variables:

```env
# Server Configuration
PORT=5000
NODE_ENV=development

# MongoDB Connection
MONGODB_URI=mongodb://localhost:27017/tsinda-cyane

# JWT Configuration
JWT_SECRET=your_super_secret_jwt_key_here
SESSION_SECRET=your_session_secret_key_here

# Google OAuth (Optional - for Google login)
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret

# Frontend URL (for CORS and redirects)
FRONTEND_URL=http://localhost:3000

# Email Configuration (Optional - for email notifications)
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USER=your_email@gmail.com
EMAIL_PASS=your_app_password

# Cloudinary Configuration (Optional - for file uploads)
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
```

### Environment Variables Explanation:

- **PORT**: The port on which the server will run (default: 5000)
- **NODE_ENV**: Environment mode (development/production)
- **MONGODB_URI**: MongoDB connection string
- **JWT_SECRET**: Secret key for JWT token generation
- **SESSION_SECRET**: Secret key for session management
- **GOOGLE_CLIENT_ID/SECRET**: Google OAuth credentials
- **FRONTEND_URL**: Frontend application URL for CORS
- **EMAIL_***: Email service configuration
- **CLOUDINARY_***: Cloud storage configuration

## Database Setup

### MongoDB Installation

#### Ubuntu/Debian:
```bash
# Import MongoDB public GPG key
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -

# Create list file for MongoDB
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list

# Update package database
sudo apt-get update

# Install MongoDB
sudo apt-get install -y mongodb-org

# Start MongoDB
sudo systemctl start mongod

# Enable MongoDB to start on boot
sudo systemctl enable mongod
```

#### macOS:
```bash
# Install MongoDB using Homebrew
brew tap mongodb/brew
brew install mongodb-community

# Start MongoDB service
brew services start mongodb/brew/mongodb-community
```

#### Windows:
1. Download MongoDB Community Server from [MongoDB Download Center](https://www.mongodb.com/try/download/community)
2. Run the installer and follow the setup wizard
3. MongoDB will be installed as a Windows service

### Database Initialization

The application will automatically create the necessary collections when it starts. However, you can manually create some initial data:

```bash
# Connect to MongoDB shell
mongosh

# Switch to your database
use tsinda-cyane

# Create initial admin user (optional)
db.users.insertOne({
  email: "admin@tsinda.com",
  password: "$2a$10$hashedpassword",
  role: "admin",
  isVerified: true
})
```

## API Documentation

### Base URL
```
http://localhost:5000/api
```

### Authentication Endpoints

#### Register User
```http
POST /api/auth/signup
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "password123",
  "firstName": "John",
  "lastName": "Doe",
  "phone": "+250123456789"
}
```

#### Login User
```http
POST /api/auth/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "password123"
}
```

#### Verify Email
```http
POST /api/auth/verify
Content-Type: application/json

{
  "email": "user@example.com",
  "verificationCode": "123456"
}
```

### Course Endpoints

#### Get All Courses
```http
GET /api/courses
Authorization: Bearer <jwt_token>
```

#### Create Course (Admin Only)
```http
POST /api/courses
Authorization: Bearer <jwt_token>
Content-Type: application/json

{
  "title": "Driving Theory Basics",
  "description": "Learn the fundamentals of driving theory",
  "categoryId": "category_id_here",
  "language": "en",
  "content": "Course content here..."
}
```

### Exam Endpoints

#### Get All Exams
```http
GET /api/exams
Authorization: Bearer <jwt_token>
```

#### Create Exam (Admin Only)
```http
POST /api/exams
Authorization: Bearer <jwt_token>
Content-Type: application/json

{
  "title": "Basic Driving Test",
  "description": "Test your driving knowledge",
  "duration": 30,
  "passingScore": 70,
  "questions": ["question_id_1", "question_id_2"]
}
```

### File Upload Endpoints

#### Upload File
```http
POST /api/upload
Authorization: Bearer <jwt_token>
Content-Type: multipart/form-data

file: <file_data>
```

## Testing

### Running Tests

```bash
# Run all tests
npm test

# Run tests in watch mode
npm run test:watch

# Run tests with coverage
npm run test:coverage

# Generate test summary
npm run test:summary
```

### Test Structure
```
tests/
├── auth.test.js           # Authentication tests
├── basic.test.js          # Basic API tests
├── endpoints-summary.test.js # Endpoint summary tests
├── enrollments.test.js    # Enrollment tests
├── exam-attempts.test.js  # Exam attempt tests
├── exams.test.js          # Exam tests
├── questions.test.js      # Question tests
├── setup.js              # Test setup
└── test-summary.js       # Test summary generator
```

### Writing Tests

Example test structure:
```javascript
describe('Auth Endpoints', () => {
  describe('POST /api/auth/signup', () => {
    it('should create a new user', async () => {
      const response = await request(app)
        .post('/api/auth/signup')
        .send({
          email: 'test@example.com',
          password: 'password123',
          firstName: 'Test',
          lastName: 'User'
        });
      
      expect(response.status).toBe(201);
      expect(response.body).toHaveProperty('token');
    });
  });
});
```

## Development Workflow

### Available Scripts

```bash
# Development
npm run dev          # Start development server with nodemon
npm start           # Start production server

# Testing
npm test            # Run all tests
npm run test:watch  # Run tests in watch mode
npm run test:coverage # Run tests with coverage

# Database
npm run db:seed     # Seed database with sample data
npm run db:reset    # Reset database
```

### Code Style Guidelines

1. **Use ES6+ features** (arrow functions, destructuring, etc.)
2. **Follow async/await pattern** for asynchronous operations
3. **Implement proper error handling** with try-catch blocks
4. **Use meaningful variable and function names**
5. **Add JSDoc comments** for complex functions
6. **Follow the existing project structure**

### Git Workflow

```bash
# Create a new feature branch
git checkout -b feature/new-feature

# Make your changes
# ... edit files ...

# Add and commit changes
git add .
git commit -m "feat: add new feature description"

# Push to remote
git push origin feature/new-feature

# Create Pull Request on GitHub
```

### Code Quality

- Use ESLint for code linting
- Write unit tests for new features
- Ensure all tests pass before committing
- Follow the established API patterns
- Document new endpoints

## Deployment

### Production Environment Setup

#### 1. Server Requirements
- **OS**: Ubuntu 20.04 LTS or higher
- **RAM**: Minimum 2GB (4GB recommended)
- **Storage**: 20GB minimum
- **Node.js**: v18+ installed
- **MongoDB**: v6+ installed
- **Nginx**: For reverse proxy
- **PM2**: For process management

#### 2. Server Setup

```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install Node.js
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs

# Install MongoDB
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
sudo apt-get update
sudo apt-get install -y mongodb-org

# Install Nginx
sudo apt install nginx

# Install PM2 globally
sudo npm install -g pm2
```

#### 3. Application Deployment

```bash
# Clone the repository
git clone https://github.com/eldadgishinge/tsinda---backend.git
cd tsinda---backend

# Install dependencies
npm install

# Create production environment file
cp env.example .env
nano .env

# Build the application (if needed)
npm run build

# Start with PM2
pm2 start app.js --name "tsinda-backend"

# Save PM2 configuration
pm2 save

# Setup PM2 to start on boot
pm2 startup
```

#### 4. Nginx Configuration

Create `/etc/nginx/sites-available/tsinda-backend`:

```nginx
server {
    listen 80;
    server_name your-domain.com;

    location / {
        proxy_pass http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_cache_bypass $http_upgrade;
    }
}
```

Enable the site:
```bash
sudo ln -s /etc/nginx/sites-available/tsinda-backend /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx
```

#### 5. SSL Certificate (Let's Encrypt)

```bash
# Install Certbot
sudo apt install certbot python3-certbot-nginx

# Obtain SSL certificate
sudo certbot --nginx -d your-domain.com

# Test automatic renewal
sudo certbot renew --dry-run
```

### Docker Deployment (Alternative)

#### Dockerfile
```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

COPY . .

EXPOSE 5000

CMD ["npm", "start"]
```

#### Docker Compose
```yaml
version: '3.8'
services:
  backend:
    build: .
    ports:
      - "5000:5000"
    environment:
      - NODE_ENV=production
      - MONGODB_URI=mongodb://mongo:27017/tsinda-cyane
    depends_on:
      - mongo
    restart: unless-stopped

  mongo:
    image: mongo:6
    ports:
      - "27017:27017"
    volumes:
      - mongo_data:/data/db
    restart: unless-stopped

volumes:
  mongo_data:
```

Deploy with Docker:
```bash
# Build and run with Docker Compose
docker-compose up -d

# View logs
docker-compose logs -f
```

## Security

### Security Implementations

1. **Input Validation**
   - Express-validator for request validation
   - Sanitization of user inputs
   - SQL injection prevention

2. **Authentication & Authorization**
   - JWT-based authentication
   - Password hashing with bcrypt
   - Role-based access control
   - Session management

3. **Data Protection**
   - CORS configuration
   - Rate limiting
   - XSS protection
   - CSRF protection

4. **File Security**
   - File type validation
   - Size limits
   - Secure file naming
   - Virus scanning (optional)

### Security Best Practices

```javascript
// Example of secure middleware
const rateLimit = require('express-rate-limit');

const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100 // limit each IP to 100 requests per windowMs
});

app.use('/api/', limiter);
```

### Environment Security

- Never commit `.env` files
- Use strong, unique secrets
- Rotate secrets regularly
- Use environment-specific configurations

## Performance

### Performance Optimizations

1. **Database Optimization**
   - Proper indexing
   - Query optimization
   - Connection pooling
   - Caching strategies

2. **Application Optimization**
   - Response compression
   - Static file serving
   - Memory management
   - Load balancing

3. **Monitoring**
   - Application metrics
   - Error tracking
   - Performance monitoring
   - Log aggregation

### Performance Monitoring

```bash
# Monitor application performance
pm2 monit

# View application logs
pm2 logs tsinda-backend

# Monitor system resources
htop
```

## Troubleshooting

### Common Issues

#### 1. Port Already in Use
```bash
# Kill process using port 5000
npx kill-port 5000

# Or find and kill the process
lsof -ti:5000 | xargs kill -9
```

#### 2. MongoDB Connection Issues
```bash
# Check MongoDB status
sudo systemctl status mongod

# Start MongoDB if stopped
sudo systemctl start mongod

# Check MongoDB logs
sudo journalctl -u mongod
```

#### 3. Permission Issues
```bash
# Fix file permissions
sudo chown -R $USER:$USER /path/to/project

# Fix npm permissions
sudo chown -R $USER:$USER ~/.npm
```

#### 4. Memory Issues
```bash
# Check memory usage
free -h

# Restart PM2 processes
pm2 restart all

# Clear npm cache
npm cache clean --force
```

### Debug Mode

```bash
# Start in debug mode
DEBUG=* npm run dev

# Or with specific debug namespace
DEBUG=app:*,auth:* npm run dev
```

### Logs

```bash
# View application logs
pm2 logs tsinda-backend

# View error logs
pm2 logs tsinda-backend --err

# View MongoDB logs
sudo tail -f /var/log/mongodb/mongod.log
```

## Contributing

### Development Setup

1. **Fork the repository**
2. **Clone your fork**
   ```bash
   git clone https://github.com/your-username/tsinda---backend.git
   cd tsinda---backend
   ```
3. **Create a feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```
4. **Make your changes**
5. **Write tests for new features**
6. **Run tests**
   ```bash
   npm test
   ```
7. **Commit your changes**
   ```bash
   git add .
   git commit -m "feat: add your feature description"
   ```
8. **Push to your fork**
   ```bash
   git push origin feature/your-feature-name
   ```
9. **Create a Pull Request**

### Code Review Guidelines

- Ensure all tests pass
- Follow the established code style
- Add appropriate documentation
- Include relevant screenshots for UI changes
- Update API documentation if needed

### Issue Reporting

When reporting issues, please include:
- Operating system and version
- Node.js version
- MongoDB version
- Steps to reproduce
- Expected vs actual behavior
- Error logs (if applicable)

## Contact

For questions, support, or contributions:

- **Email**: e.gishinge@alustudent.com
- **GitHub Issues**: [Create an issue](https://github.com/eldadgishinge/tsinda---backend/issues)
- **Project Repository**: [Backend Repository](https://github.com/eldadgishinge/tsinda---backend)

---

**Note**: This is a comprehensive guide for setting up and maintaining the Tsinda Backend. For the most up-to-date information, always refer to the latest documentation and release notes.
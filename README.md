# BIG Language LMS

A full-stack Learning Management System (LMS) built with React, Node.js, Express, and PostgreSQL. Features role-based authentication for Admins (Trainers) and Students, course management, and SCORM file support.

## Features

- 🔐 **Role-based Authentication** (Admin/Student)
- 📚 **Course Management** (Upload, Assign, Track)
- 👥 **User Management** (Admin can view all users)
- 📊 **Progress Tracking** (Monitor student progress)
- 🎓 **SCORM Support** (Upload SCORM packages)
- 📱 **Responsive Design** (Works on all devices)

## Tech Stack

### Frontend
- React 18
- React Router DOM
- Tailwind CSS
- Vite

### Backend
- Node.js
- Express.js
- PostgreSQL
- JWT Authentication
- Bcrypt (Password hashing)
- Multer (File uploads)

## Prerequisites

Before you begin, ensure you have the following installed:
- **Node.js** (v18 or higher) - [Download](https://nodejs.org/)
- **PostgreSQL** (v14 or higher) - [Download](https://www.postgresql.org/download/)
- **npm** or **yarn** (comes with Node.js)

## Installation & Setup

### 1. Clone the Repository

```bash
git clone <your-repo-url>
cd BIG_LMS-dev
```

### 2. Install Dependencies

#### Install Backend Dependencies
```bash
cd server
npm install
```

#### Install Frontend Dependencies
```bash
cd ../client
npm install
```

### 3. Database Setup

#### Start PostgreSQL Service
Make sure PostgreSQL is running on your system.

**Windows:**
- Search for "Services" in Start Menu
- Find "postgresql-x64-18" (or your version)
- Click "Start"

**macOS/Linux:**
```bash
sudo service postgresql start
# or
brew services start postgresql
```

#### Configure Database Connection

1. Navigate to `server/.env` file
2. Update the following variables with your PostgreSQL credentials:

```env
PORT=5000
DB_USER=postgres
DB_PASSWORD=your_postgres_password
DB_HOST=localhost
DB_PORT=5433
DB_NAME=lms_db
JWT_SECRET=supersecretkey123
```

> **Note:** Change `DB_PORT` to `5432` if that's your PostgreSQL port. Update `DB_PASSWORD` with your actual PostgreSQL password.

#### Create Database and Tables

Run the database setup script:

```bash
cd server
node scripts/setupDatabase.js
```

You should see output like:
```
Database lms_db created successfully.
Users table created/verified.
Courses table created/verified.
Enrollments table created/verified.
```

### 4. Run the Application

#### Start Backend Server
```bash
cd server
npm run dev
```

The server will start on `http://localhost:5000`

#### Start Frontend (in a new terminal)
```bash
cd client
npm run dev
```

The frontend will start on `http://localhost:5173` (or another port if 5173 is busy)

### 5. Access the Application

Open your browser and navigate to:
```
http://localhost:5173
```

## Usage Guide

### First Time Setup

1. **Sign Up as Admin:**
   - Go to `/signup`
   - Fill in your details
   - Select **"Trainer (Admin)"** as role
   - Click Sign Up

2. **Sign Up as Student:**
   - Create another account
   - Select **"Student"** as role

3. **Login as Admin:**
   - Go to `/login`
   - Select **"Trainer (Admin)"** role
   - Enter credentials

4. **Upload a Course:**
   - Navigate to Admin Dashboard
   - Fill in course title and description
   - Upload a SCORM zip file (or any .zip file for testing)
   - Click "Upload Course"

5. **Assign Course to Student:**
   - Select a user from the dropdown
   - Select a course from the dropdown
   - Click "Assign Course"

6. **Login as Student:**
   - Logout and login as Student
   - Go to "My Courses" from sidebar
   - View assigned courses

## Project Structure

```
BIG_LMS-dev/
├── client/                 # Frontend (React + Vite)
│   ├── src/
│   │   ├── components/    # Reusable components
│   │   ├── pages/         # Page components
│   │   ├── layouts/       # Layout components
│   │   ├── utils/         # Utility functions
│   │   └── assets/        # Images, icons, etc.
│   ├── package.json
│   └── vite.config.js
│
├── server/                # Backend (Node.js + Express)
│   ├── routes/           # API routes
│   ├── middleware/       # Auth middleware
│   ├── scripts/          # Database setup scripts
│   ├── uploads/          # Uploaded SCORM files
│   ├── db.js            # Database connection
│   ├── index.js         # Server entry point
│   ├── .env             # Environment variables
│   └── package.json
│
└── README.md
```

## API Endpoints

### Authentication
- `POST /api/auth/signup` - Register new user
- `POST /api/auth/login` - Login user

### Courses
- `GET /api/courses` - Get all courses
- `GET /api/courses/:id` - Get single course
- `POST /api/courses/upload` - Upload course (Admin only)
- `POST /api/courses/assign` - Assign course to user (Admin only)

### Users
- `GET /api/users` - Get all users (Admin only)
- `GET /api/users/my-courses` - Get assigned courses (Student)

## Environment Variables

Create a `.env` file in the `server` directory:

```env
PORT=5000
DB_USER=postgres
DB_PASSWORD=your_password
DB_HOST=localhost
DB_PORT=5433
DB_NAME=lms_db
JWT_SECRET=your_secret_key_here
```

## Troubleshooting

### Database Connection Error
- Ensure PostgreSQL is running
- Check if the port in `.env` matches your PostgreSQL port
- Verify username and password are correct

### Port Already in Use
- Change `PORT` in `server/.env`
- Or kill the process using that port

### Token is not valid
- Log out and log back in to get a fresh token
- Tokens expire after 24 hours

### SCORM Files Not Playing
- Currently, SCORM files are stored but not extracted/played
- This feature is planned for future implementation

## Future Enhancements

- [ ] SCORM content extraction and playback
- [ ] Real-time progress tracking
- [ ] Quiz and assessment features
- [ ] Certificate generation
- [ ] Email notifications
- [ ] Advanced analytics dashboard

## License

This project is licensed under the ISC License.

## Support

For issues or questions, please create an issue in the repository.

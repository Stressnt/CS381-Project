**CS381 / CS472 – Web Application Development Project**  
Yanbu Industrial College | Topic 5: Lost & Found

---

## Project Overview

A full-stack web application allowing YIC students and staff to report lost items,
post found items, submit claims, and receive notifications — with admin approval flow.

---

## Tech Stack

| Layer     | Technology                     |
|-----------|--------------------------------|
| Frontend  | HTML5 (semantic), CSS3, ES6 JS |
| Backend   | PHP 8.0+ with PDO              |
| Database  | MySQL 5.7+                     |
| Icons     | Font Awesome 6 (CDN)           |
| Fonts     | Google Fonts – Inter (CDN)     |

**No frameworks used** — 100% vanilla code as per project requirements.

---

## Features

### Student Role
- Register & login with secure sessions
- Report lost or found items with image upload
- Browse & search items by type, category, status
- Submit claims for found items
- View claim status (pending / approved / rejected)
- Receive notifications on claim updates
- Edit and delete own items

### Admin Role
- Admin dashboard with live statistics
- Approve or reject claims with optional notes
- Auto-notifies claimant on decision
- Marks item as "claimed" when a claim is approved
- View and manage all items (change status, delete)
- User management overview

### Security Implemented
- CSRF tokens on all forms
- Password hashing with bcrypt (cost 12)
- PDO prepared statements (SQL injection prevention)
- `htmlspecialchars()` on all output (XSS prevention)
- Session fixation prevention (`session_regenerate_id`)
- HttpOnly session cookies
- Server-side file upload validation (type + size)
- Role-based access control

---

## Setup Instructions

### 1. Requirements
- PHP 8.0 or higher (with PDO MySQL extension)
- MySQL 5.7+ or MariaDB 10+
- Apache or Nginx with PHP support
- **Recommended:** XAMPP / WAMP / MAMP for local development

### 2. Installation Steps

```bash
# 1. Clone / copy the project into your web server root
#    e.g. for XAMPP: C:/xampp/htdocs/lost-found/

# 2. Create the database
mysql -u root -p < database.sql

# 3. Configure DB connection
# Edit: config/db.php
# Change DB_USER and DB_PASS to match your MySQL credentials
```

### 3. Database Configuration

Open `config/db.php` and update:

```php
define('DB_HOST', 'localhost');
define('DB_NAME', 'yic_lost_found');
define('DB_USER', 'root');       // ← your MySQL username
define('DB_PASS', '');           // ← your MySQL password
```

### 4. Uploads Folder

Ensure the `uploads/items/` folder is writable:

```bash
chmod 755 uploads/
chmod 755 uploads/items/
```

### 5. Access the Application

Open your browser and navigate to:
```
http://localhost/lost-found/
```

---

## Login Credentials (Demo)

| Role    | Email                  | Password    |
|---------|------------------------|-------------|
| Admin   | admin@yic.edu.sa       | Password123 |
| Student | ahmed@yic.edu.sa       | Password123 |
| Student | sara@yic.edu.sa        | Password123 |
| Student | omar@yic.edu.sa        | Password123 |

---

## File Structure

```
lost-found/
├── config/
│   └── db.php              # PDO database connection
├── includes/
│   ├── auth.php            # Auth helpers, CSRF, flash messages
│   ├── header.php          # Global navbar + flash messages
│   └── footer.php          # Global footer
├── css/
│   └── style.css           # All styles (~700 lines, responsive)
├── js/
│   └── main.js             # Client-side JS (nav, forms, preview)
├── uploads/
│   └── items/              # Uploaded item images
├── admin/
│   ├── dashboard.php       # Admin overview + stats
│   ├── items.php           # Manage all items
│   ├── claims.php          # Approve/reject claims
│   └── users.php           # View all users
├── index.php               # Home page (hero, stats, recent items)
├── login.php               # Login form
├── register.php            # Registration form
├── logout.php              # Session destroy
├── items.php               # Browse + search + filter
├── item-detail.php         # Single item + claim submission
├── report.php              # Report/edit item (with image upload)
├── dashboard.php           # Student dashboard
├── notifications.php       # Notification center
├── database.sql            # Schema + seed data
└── README.md               # This file
```

---

## Database Schema

### Tables

| Table         | Purpose                                      |
|---------------|----------------------------------------------|
| users         | Registered users (students & admins)         |
| items         | Lost / Found item reports                    |
| claims        | Student claims on found items                |
| notifications | In-app notifications for users               |

---

## AI Disclosure

This project was developed with assistance from Claude (Anthropic). AI was used to:
- Generate boilerplate PHP/HTML/CSS code structures
- Suggest security best practices (CSRF, PDO, bcrypt)
- Review and improve code organization

All code was reviewed, understood, and customized by the student group.

---

## Challenges

- Implementing CSRF protection correctly across all forms
- Managing session security (fixation prevention)
- Handling file uploads safely (server-side validation)
- Building responsive CSS without any framework

---

## Future Improvements

- Email notifications via PHP Mailer
- Google Maps integration for item locations
- Image compression on upload
- Real-time chat between reporter and claimant
- QR code generation for item tags
- PWA support for mobile push notifications

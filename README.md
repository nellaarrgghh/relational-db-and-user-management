# Student Management Web Application

A PHP and MySQL-based student management system featuring authentication, role-based access control (Admin & Staff), and relational database operations (CRUD) with foreign keys.

## Student Identity

| Name | NRP |
| :--- | :--- |
| Naila Sa'ada Cahyani | 5025251258 |

---

## Project Structure

```text
student-app/
├── auth.php        # Session guard and role helper functions (is_admin, require_admin)
├── config.php      # Database connection configuration (MySQL/MariaDB via mysqli)
├── create.php      # Form to insert new student records with dynamic majors dropdown
├── db_school.sql   # Complete database schema and initial seed data
├── delete.php      # Admin-restricted student deletion handler
├── edit.php        # Pre-populated form to update student records
├── index.php       # Protected dashboard listing students with INNER JOIN to majors
├── login.php       # Authentication form with password hashing verification
├── logout.php      # Session destruction and logout handler
├── navbar.php      # Reusable navigation bar with role-aware links and user badge
├── README.md       # Project documentation and setup instructions
└── users.php       # Admin-only user management interface to create and list users
```

---

## Default Test Credentials

The database dump includes pre-seeded accounts:

| Username | Password | Role | Access / Permissions |
| :--- | :--- | :--- | :--- |
| **admin** | `admin123` | `admin` | Full access: View, Add, Edit, Delete students; Access User Management |
| **staff** | `staff123` | `staff` | Limited access: View, Add, Edit students (cannot delete or manage users) |

---

## Database Setup & Import

1. **Start Apache and MySQL** via the XAMPP Control Panel.
2. **Import Database:**
   - **Option A (phpMyAdmin):**
     1. Open your browser and navigate to `http://localhost/phpmyadmin`.
     2. Click on the **Import** tab.
     3. Choose `db_school.sql` from the `student-app/` directory.
     4. Click **Import** / **Go** at the bottom.
   - **Option B (Command Line / Terminal):**
     ```bash
     mysql -u root -p < db_school.sql
     ```
     *(If running default XAMPP without a MySQL password, press Enter when prompted).*

The SQL file automatically creates the `db_school` database if it doesn't already exist and sets up:
- **`majors` table:** `id` (PK), `name` (unique).
- **`students` table:** `id` (PK), `nim`, `name`, `major_id` (foreign key referencing `majors(id)` with `ON DELETE RESTRICT`).
- **`users` table:** `id` (PK), `username` (unique), `password` (bcrypt hash), `role` (`ENUM('admin', 'staff')`).
- Initial seed data for majors, sample students, and default user accounts.

---

## How to Run

1. Place the `student-app` directory inside your XAMPP web root (`htdocs`):
   - **macOS:** `/Applications/XAMPP/xamppfiles/htdocs/student-app`
   - **Windows:** `C:\xampp\htdocs\student-app`
   - **Linux:** `/opt/lampp/htdocs/student-app`
2. Open your web browser and go to:
   ```
   http://localhost/student-app/login.php
   ```
3. Log in with the `admin` or `staff` credentials provided above.

# Final Internship Project: Online Library Management System

📚 A comprehensive web application developed with CodeIgniter 4 for efficient library management. This platform allows administrators and users to manage books, members, and borrowings intuitively and securely.

**Duration:** September 7, 2025 - September 10, 2025  
**Contributor:** Abel KPOKOUTA

## ✨ Features

### 👥 User Management
- Secure registration and authentication with email validation
- Distinct roles: Administrators, Students, Teachers, Professors, and Librarians
- Management of activation status and subscription expiration
- Personalized dashboards based on role and status
- Password recovery system

### 📖 Book Management
- Complete book catalog with cover images
- Advanced search and filtering system by title, author, category, ISBN
- Stock management (total quantity and available copies)
- Detailed information: title, author, ISBN, category, description, publication year
- Full CRUD operations (Create, Read, Update, Delete)

### 🔄 Borrowing Management
- Borrowing system with start date, expected return date, and actual return date
- Real-time tracking of borrowing status (pending, active, returned, overdue, cancelled)
- Automatic notifications for late returns
- Complete transaction history with notes
- Borrowing extension management

## 🛠️ Technologies Used

- **Backend:** CodeIgniter 4 (PHP 7.4+)
- **Frontend:** HTML5, CSS3, JavaScript, Bootstrap
- **Database:** MySQL 5.7+
- **Security:** Data validation, CSRF protection, password hashing (bcrypt)

## 📦 Project Structure

```
Gestion-Bibliotheque/
├── app/
│   ├── Config/
│   │   ├── Database.php
│   │   └── Routes.php
│   ├── Controllers/
│   │   ├── Auth.php
│   │   ├── Books.php
│   │   ├── Loans.php
│   │   └── Users.php
│   ├── Models/
│   │   ├── UserModel.php
│   │   ├── BookModel.php
│   │   └── LoanModel.php
│   ├── Views/
│   │   ├── auth/
│   │   ├── books/
│   │   ├── loans/
│   │   ├── users/
│   │   └── dashboard/
│   └── Libraries/
├── public/
│   └── assets/
│       ├── css/
│       ├── js/
│       ├── images/
│       └── uploads/books/
├── system/
└── writable/
```

## 🗃️ Database Structure

### Table users

```sql
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    email VARCHAR(255) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    phone VARCHAR(20),
    address TEXT,
    date_of_birth DATE,
    
    -- NOUVEAU : Type de statut avec plus d'options
    status ENUM('student', 'teacher', 'professor', 'librarian', 'professional', 'other') DEFAULT 'student',
    
    -- NOUVEAU : Informations spécifiques selon le statut
    student_id VARCHAR(50),              -- Numéro d'étudiant
    institution VARCHAR(255),            -- Université/École/Entreprise
    specialization VARCHAR(255),         -- Domaine d'études/spécialisation
    professional_title VARCHAR(100),     -- Titre professionnel
    
    role ENUM('admin', 'user') DEFAULT 'user',
    is_active TINYINT(1) DEFAULT 0,
    membership_expiry DATE,              -- NOUVEAU : Date d'expiration d'adhésion
    activation_code VARCHAR(32),
    reset_token VARCHAR(32),
    reset_expires DATETIME,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    
    -- Index pour les nouveaux champs
    INDEX idx_email (email),
    INDEX idx_role (role),
    INDEX idx_status (status),
    INDEX idx_institution (institution),
    INDEX idx_membership_expiry (membership_expiry),
    INDEX idx_active (is_active)
);
```

### Books Table

```sql
CREATE TABLE books (
    id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(255) NOT NULL,
    author VARCHAR(255) NOT NULL,
    isbn VARCHAR(20) UNIQUE,
    category VARCHAR(100),
    description TEXT,
    publish_year YEAR,
    publisher VARCHAR(255),
    quantity INT DEFAULT 1,
    available INT DEFAULT 1,
    cover_image VARCHAR(255),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Loans Table

```sql
CREATE TABLE loans (
    id INT PRIMARY KEY AUTO_INCREMENT,
    book_id INT NOT NULL,
    user_id INT NOT NULL,
    loan_date DATE NOT NULL,
    due_date DATE NOT NULL,
    return_date DATE NULL,
    status ENUM('pending', 'active', 'returned', 'overdue', 'cancelled') DEFAULT 'pending',
    notes TEXT,
    created_by INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (book_id) REFERENCES books(id) ON DELETE CASCADE,
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```

---

**10/09/2025 au 11/09/2025**

*Mise au point de tout les options du dashbord des administrateur*

- Gestion des livres en temps réels. ;
- Gestion des Membres en temps réels. (Utilisateur comme administrateurs) ( CRED ) en temps réels;
- Gestion des Emprunts en temps réels;
- Gestion des Retards en temps réels;
- Option "Parametre" mise en place ;
- Option "Deconnexion admin";


*Mise au point de tout les options du dashbord des utilisateur*

- ✅ Statistiques réelles de ses emprunts

- ✅ Liste de ses emprunts en cours avec images

- ✅ Livres disponibles avec images

- ✅ Interface complète et professionnelle


- ✅ Tableau de bord avec statistiques

- ✅ Catalogue des livres disponibles avec recherche

- ✅ Historique des emprunts

- ✅ Détails des emprunts avec progression

- ✅ Interface responsive et professionnelle

- ✅ Système de filtrage et recherche

**12/09/2025 au 14/09/2025**

- Mise en forme Responsive de l'interface Uitlisateur ...
- Mise en forme Responsive de l'interface Administrateur ...

**Contributeur de ces modifications : Abel KPOKOUTA**
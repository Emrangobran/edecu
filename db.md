**-- 1. جدول المستخدمين (الأساس)**

**CREATE TABLE users (**

    **id SERIAL PRIMARY KEY,**

    **full\_name VARCHAR(100) NOT NULL,**

    **email VARCHAR(150) UNIQUE NOT NULL,**

    **password\_hash VARCHAR(255) NOT NULL,**

    **role VARCHAR(20) CHECK (role IN ('student', 'instructor', 'admin')) DEFAULT 'student',**

    **avatar\_url TEXT,**

    **created\_at TIMESTAMP DEFAULT CURRENT\_TIMESTAMP**

**);**



**-- 2. جدول الدورات (يربط الدورة بالمدرب)**

**CREATE TABLE courses (**

    **id SERIAL PRIMARY KEY,**

    **instructor\_id INT REFERENCES users(id) ON DELETE CASCADE,**

    **title VARCHAR(200) NOT NULL,**

    **description TEXT,**

    **thumbnail\_url TEXT,**

    **price DECIMAL(10, 2) DEFAULT 0.00,**

    **is\_published BOOLEAN DEFAULT FALSE,**

    **created\_at TIMESTAMP DEFAULT CURRENT\_TIMESTAMP**

**);**



**-- 3. جدول التسجيل (يربط الطالب بالدورة)**

**CREATE TABLE enrollments (**

    **id SERIAL PRIMARY KEY,**

    **student\_id INT REFERENCES users(id) ON DELETE CASCADE,**

    **course\_id INT REFERENCES courses(id) ON DELETE CASCADE,**

    **enrolled\_at TIMESTAMP DEFAULT CURRENT\_TIMESTAMP,**

    **progress INT DEFAULT 0 -- نسبة التقدم المئوية**

**);**




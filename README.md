
# Project Title

A brief description of what this project does and who it's for

# 🏦 Axis Bank Enterprise Banking System  

> **A Full-Stack Java EE Web Application (JSP + Servlets + JDBC + MySQL)**  
> Built with clean MVC architecture, real-time alerts, validations, and role-based access.  
> Designed and developed by **Vamshi Prasad Goteti**  

---

## 📘 Overview  

The **Axis Bank Enterprise Banking System** is an enterprise-grade, full-stack Java web application designed to simulate a real-world banking management system.  
It enables employees and customers to securely manage accounts, perform deposits and withdrawals, track transactions, and handle user authentication and authorization efficiently.

This project demonstrates **end-to-end Java Full Stack development** using **JSP, Servlets, JDBC, MySQL**, and **Bootstrap 5**, focusing on modular design, security, and clean user experience.

---

## 🧱 Architecture  

### 🧩 MVC (Model–View–Controller) Pattern


- **Model** – Java Beans like `Customers`, `Accounts`, and `Transactions` represent data entities.  
- **View** – JSP pages display dynamic content using attributes passed from servlets.  
- **Controller** – Java Servlets process user requests, perform logic, and forward data to JSPs.  

---

## 🧰 Tech Stack  

| Layer | Technologies |
|-------|--------------|
| **Frontend** | JSP, HTML5, CSS3, Bootstrap 5, SweetAlert2, Chart.js |
| **Backend** | Java Servlets, JDBC |
| **Database** | MySQL |
| **Server** | Apache Tomcat 9+ |
| **IDE** | Eclipse / IntelliJ IDEA |
| **Version Control** | Git & GitHub |
| **Architecture Pattern** | MVC |

---

## 📂 Project Structure  
```bash
AxisBank-Enterprise/
│
├── src/com/Banking/
│   ├── Accounts.java
│   ├── Customers.java
│   ├── Transactions.java
│   ├── Users.java
│   ├── DbConnection.java
│   ├── LoginServlet.java
│   ├── CustomerServlet.java
│   ├── EditCustomerServlet.java
│   ├── CreateNewCustomer.java
│   ├── DeleteCustomerServlet.java
│   ├── DepositServlet.java
│   ├── WithdrawServlet.java
│   ├── StatementServlet.java
│   ├── EditProfile.java
│   ├── EditPassword.java
│   └── LogoutServlet.java
│
├── WebContent/
│   ├── login.jsp
│   ├── EmployeeDashboard.jsp
│   ├── CustomerDashboard.jsp
│   ├── EditProfile.jsp
│   ├── EditPassword.jsp
│   ├── deposit.jsp
│   ├── withdraw.jsp
│   ├── statement.jsp
│   │
│   └── assets/
│       ├── css/
│       ├── js/
│       └── images/
│
└── WEB-INF/
    └── web.xml

---

## 🧩 Core Modules  

### 👨‍💼 Employee Module  
- Add/Edit/Delete Customers  
- Manage Customer Accounts  
- Perform Deposits/Withdrawals  
- Generate Transaction Statements  
- Edit Profile and Change Password  
- View KPI metrics via Chart.js  

### 👩‍💻 Customer Module  
- Secure Login  
- View Account Details & Balances  
- Deposit or Withdraw Money  
- Generate Transaction Statements  
- Manage Personal Profile  

---

## 🔐 Authentication & Authorization  

### 1️⃣ Authentication  
- Handled by `LoginServlet.java`  
- Validates credentials from the `users` table.  
- Uses `HttpSession` to maintain login state.  
- Redirects users based on role:
  - Employee → `EmployeeDashboard.jsp`
  - Customer → `CustomerDashboard.jsp`
- Invalid credentials trigger a SweetAlert2 error popup.

### 2️⃣ Authorization  
- Employees: Full access to management, CRUD, transactions.  
- Customers: Limited access (only their accounts).  
- Unauthorized users redirected to login.  
- Sessions auto-expire after 30 minutes of inactivity.

---

## 🔁 Request–Response Lifecycle Example  

### Deposit Operation Flow  
deposit.jsp → POST /DepositServlet
↓
DepositServlet.java:
1️⃣ Validate input amount
2️⃣ Update balance via JDBC
3️⃣ Log transaction in DB
4️⃣ Forward to JSP with success message
↓
SweetAlert2 popup → Redirects back to dashboard

### Edit Customer Flow  

EditCustomer.jsp → POST /EditCustomerServlet
↓
EditCustomerServlet.java:
1️⃣ Validate updated info
2️⃣ Execute SQL UPDATE
3️⃣ Forward result to JSP
↓
SweetAlert2 → "Customer Updated Successfully"

---

## ⚙️ Servlet Operations  

| Servlet | Description |
|----------|-------------|
| **LoginServlet** | Authenticates users & manages sessions |
| **CustomerServlet** | Displays all customers for employee |
| **CreateNewCustomer** | Adds new customer + creates account |
| **EditCustomerServlet** | Updates existing customer info |
| **DeleteCustomerServlet** | Deletes customer and related accounts |
| **DepositServlet** | Performs deposits and updates balance |
| **WithdrawServlet** | Withdraws funds with validations |
| **StatementServlet** | Fetches transaction history |
| **EditProfile** | Allows employee to update profile |
| **EditPassword** | Handles password change logic |
| **LogoutServlet** | Invalidates session and redirects to login |

---

## ✅ Validations  

| Type | Description |
|------|--------------|
| **Form Validation (Frontend)** | Required fields, input length, email/phone regex |
| **Backend Validation (Servlets)** | Checks for null, empty, or invalid data |
| **Amount Validation** | Deposit/withdraw amounts must be > 0 |
| **Balance Validation** | Prevents overdrafts (balance < withdraw amount) |
| **Session Validation** | Prevents access to dashboards without active login |
| **Password Validation** | Matches old password, new passwords must match |
| **Database Validation** | Uses `PreparedStatement` to prevent SQL Injection |
| **Duplicate Prevention** | Checks existing customer emails before insert |
| **Error Handling** | SweetAlert2 for user-friendly messages |

---

## 🗃 Database Schema  

### 🧍 users  
| Column | Type | Description |
|---------|------|-------------|
| user_id | INT (PK) | Auto Increment |
| username | VARCHAR | Login Email |
| password | VARCHAR | Hashed Password |
| role | VARCHAR | “employee” or “customer” |
| created_at | TIMESTAMP | Creation Timestamp |

### 👥 customers  
| Column | Type | Description |
|---------|------|-------------|
| cust_id | INT (PK) | Unique ID |
| cust_name | VARCHAR | Full Name |
| email | VARCHAR | Unique Email |
| mob_no | VARCHAR | Contact Number |
| address | VARCHAR | Address |
| created_at | TIMESTAMP | Created Timestamp |

### 💳 accounts  
| Column | Type | Description |
|---------|------|-------------|
| account_id | INT (PK) | Unique Account ID |
| cust_id | INT (FK) | Customer Link |
| account_type | VARCHAR | Savings/Current |
| balance | DECIMAL | Current Balance |
| created_at | TIMESTAMP | Opened Date |

### 💸 transactions  
| Column | Type | Description |
|---------|------|-------------|
| transaction_id | INT (PK) | Unique Transaction ID |
| account_id | INT (FK) | Related Account |
| type | VARCHAR | Deposit/Withdraw |
| amount | DECIMAL | Transaction Amount |
| description | VARCHAR | Transaction Notes |
| transaction_date | TIMESTAMP | Date & Time |

---

## 🔄 ER Diagram  

```mermaid
erDiagram
    USERS ||--o{ CUSTOMERS : manages
    CUSTOMERS ||--o{ ACCOUNTS : owns
    ACCOUNTS ||--o{ TRANSACTIONS : records

    USERS {
        int user_id
        string username
        string password
        string role
    }
    CUSTOMERS {
        int cust_id
        string cust_name
        string email
        string mob_no
        string address
    }
    ACCOUNTS {
        int account_id
        int cust_id
        string account_type
        decimal balance
    }
    TRANSACTIONS {
        int transaction_id
        int account_id
        string type
        decimal amount
        string description
    }
🧮 Data Flow (Frontend → Backend)
Stage	Description
1. JSP Form Submission	User inputs data (e.g., deposit.jsp)
2. Servlet Controller	Captures parameters, validates, executes SQL
3. Model Interaction	Uses JDBC to communicate with MySQL
4. Response Forwarding	Uses request.setAttribute() and RequestDispatcher.forward()
5. JSP Rendering	Displays results dynamically
6. SweetAlert2 Feedback	Popups show user-friendly confirmations/errors
🧾 Setup & Installation
Prerequisites


JDK 11+


Apache Tomcat 9+


MySQL 8+


MySQL Connector JAR


Eclipse IDE


Steps


Clone the repository
git clone https://github.com/Vmshibharadwaj19/AxisBank-Enterprise.git



Import into Eclipse as Dynamic Web Project


Add MySQL Connector JAR to WebContent/WEB-INF/lib


Configure DB credentials in DbConnection.java
public static final String url = "jdbc:mysql://localhost:3306/bankdb";
public static final String user = "root";
public static final String pwd = "yourpassword";



Run the project on Tomcat Server


Access via:
http://localhost:8080/AxisBank/login.jsp




📸 Interface Overview
PageDescriptionLogin.jspAuthentication form with SweetAlert2 feedbackEmployeeDashboard.jspKPI metrics, charts, quick actionsCustomerDashboard.jspUser-friendly summary of customer accountDeposit.jsp / Withdraw.jspSecure transaction pagesStatement.jspView transaction historyEditProfile.jspUpdate user detailsChangePassword.jspPassword validation and update

🔮 Future Enhancements


Migrate backend to Spring Boot REST APIs


Implement JWT Authentication


Add Email/SMS Transaction Alerts


Introduce Two-Factor Authentication (2FA)


Deploy via Docker + AWS EC2


Add Admin Analytics Dashboard



👨‍💻 Author
Vamshi Prasad Goteti
📍 Bangalore, India
📧 vamshibharadwaj19@gmail.com
🐙 GitHub – Vmshibharadwaj19
🔗 LinkedIn – vamshi-prasad-goteti


💬 “An enterprise-level Java banking solution built with JSP, Servlets, and MySQL — showcasing professional-grade full-stack development and clean MVC architecture.”


---

✅ **How to use:**
1. Copy everything between the triple backticks (` ```markdown ... ``` `).  
2. Paste into a file named `README.md` in your project root.  
3. Commit and push to GitHub.  
4. GitHub will render it beautifully with headings, tables, and mermaid diagrams.  

Would you like me to now generate the **SQL schema file (`bankdb.sql`)** that matches all the tables and relationships in this README?



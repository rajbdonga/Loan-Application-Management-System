# LAMS - Loan Application Management System
## ASP.NET Core MVC | Role-Based Access | MySQL (XAMPP)

---

## PROJECT STRUCTURE

```
LAMS/
├── Controllers/
│   ├── AccountController.cs     → Login, Register, Logout
│   ├── HomeController.cs        → Dashboard (Client & Staff)
│   ├── LoanApplicationController.cs  → Client: Apply, My Applications, Details
│   └── StaffController.cs       → BankStaff: All Apps, Details, Review
├── Models/
│   ├── ApplicationUser.cs       → Extended Identity User
│   ├── LoanApplication.cs       → Loan entity model
│   └── ViewModels/ViewModels.cs → Login, Register, Review VMs
├── Data/
│   └── ApplicationDbContext.cs  → EF Core DbContext
├── Views/
│   ├── Account/                 → Login, Register, AccessDenied
│   ├── Home/                    → ClientDashboard, StaffDashboard
│   ├── LoanApplication/         → Apply, MyApplications, Details
│   ├── Staff/                   → AllApplications, Details, Review
│   └── Shared/_Layout.cshtml   → Common layout with navbar
├── wwwroot/css/site.css
├── Program.cs                   → App setup + Role seeding
├── appsettings.json             → DB connection string
└── LAMSDB_Setup.sql             → Manual DB reference
```

---

## ROLES

| Role       | Access                                              |
|------------|-----------------------------------------------------|
| Client     | Apply for loan, view own applications & status      |
| BankStaff  | View all applications, approve/reject with remarks  |

---

## SETUP STEPS

### Step 1 – Prerequisites
- .NET 8 SDK
- XAMPP (MySQL running on port 3306)
- Visual Studio 2022 or VS Code

### Step 2 – Database
1. Start XAMPP → Start **Apache** + **MySQL**
2. Open **phpMyAdmin** → http://localhost/phpmyadmin
3. Create empty database named **LAMSDB**

### Step 3 – Run Project

```bash
cd LAMS

# Restore NuGet packages
dotnet restore

# Create EF Core migration
dotnet ef migrations add InitialCreate

# Apply migration (creates all tables in LAMSDB)
dotnet ef database update

# Run the app
dotnet run
```

### Step 4 – Open Browser
```
http://localhost:5000
```

---

## DEFAULT CREDENTIALS

| Role      | Email             | Password   |
|-----------|-------------------|------------|
| BankStaff | staff@gmail.com    | Staff@123  |
| Client    | Register yourself | (any 6+ chars) |

> Staff account is auto-created on first run via seed in Program.cs

---

## FEATURES

### Client
- Register & Login
- Apply for loan (Personal/Home/Education/Business/Vehicle)
- Track application status (Pending / Approved / Rejected)
- View bank's remarks after review

### Bank Staff
- Login with staff credentials
- View all client applications
- Filter by status (All / Pending / Approved / Rejected)
- Approve or Reject with remarks
- View client details alongside application

---

## TECH STACK

| Layer       | Technology                            |
|-------------|---------------------------------------|
| Framework   | ASP.NET Core 8 MVC                    |
| Auth        | ASP.NET Core Identity (Role-based)    |
| Database    | MySQL (XAMPP) via Pomelo EF Provider  |
| ORM         | Entity Framework Core 8               |
| UI          | Bootstrap 5 + Bootstrap Icons         |
| Runtime     | .NET 8                                |

---

## TROUBLESHOOTING

**Error: Unable to connect to MySQL**
→ Make sure XAMPP MySQL is running on port 3306
→ Check `appsettings.json` connection string

**Error: dotnet ef not found**
→ Run: `dotnet tool install --global dotnet-ef`

**Password issues**
→ appsettings.json me MySQL root password set karo agar XAMPP me password hai
→ `"Password=your_password_here;"`

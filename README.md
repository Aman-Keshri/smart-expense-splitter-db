# 🗄️ Smart Expense Splitter Database

A modern, normalized SQL Server database for tracking group expenses, settlements, and financial insights.

![Database Banner](https://via.placeholder.com/1200x300/4285f4/ffffff?text=Smart+Expense+Splitter+Database)

## 📊 Overview

This repository contains the complete database schema, scripts, and documentation for the Smart Expense Splitter application. The database is designed with modern best practices including normalization, referential integrity, soft deletes, and efficient indexing.

## 🏗️ Schema Overview

The database consists of several interconnected tables that manage the following entities:

- **Users** - Account information and authentication
- **Groups** - Collection of users who share expenses
- **GroupMembers** - Many-to-many relationship between users and groups
- **ExpenseCategories** - Types of expenses (e.g., Food, Transportation)
- **Expenses** - Individual expense records
- **ExpenseParticipants** - Who shares in each expense and by how much
- **Receipts** - Images/documents related to expenses
- **Settlements** - Records of payments between users
- **InsightTypes** - Categories of AI-generated insights
- **Insights** - AI-generated tips and observations
- **NotificationTypes** - Categories of notifications
- **Notifications** - Alerts and messages for users

## 📝 Entity Relationship Diagram

![ER Diagram](https://via.placeholder.com/800x600/4285f4/ffffff?text=ER+Diagram)

▶️ [View Interactive ER Diagram](https://dbdiagram.io/d/your-diagram-link)

## 🚀 Getting Started

### Prerequisites
- SQL Server 2019+ (any edition) or SQL Server Docker container
- SQL Server Management Studio (SSMS) or Azure Data Studio

### Setup Instructions

#### Option 1: Direct SQL Script Execution
1. Clone this repository
2. Connect to your SQL Server instance using SSMS
3. Run the script from `scripts/create-database.sql`
4. Run the script from `scripts/seed-data.sql` (optional - for sample data)

#### Option 2: Docker Setup
```bash
# Pull SQL Server Docker image
docker pull mcr.microsoft.com/mssql/server:2019-latest

# Run SQL Server container
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=YourStr0ngP@ssw0rd" -p 1433:1433 --name sqlserver -d mcr.microsoft.com/mssql/server:2019-latest

# Execute script (from repository root directory)
docker exec -i sqlserver /opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P YourStr0ngP@ssw0rd -i ./scripts/create-database.sql
```

### Connection String
```
Server=localhost,1433;Database=SmartExpenseSplitter;User ID=sa;Password=YourStr0ngP@ssw0rd;TrustServerCertificate=True;
```

## 📂 Repository Structure

```
/
├── scripts/                    # SQL Scripts
│   ├── create-database.sql     # Full database creation script
│   ├── seed-data.sql           # Sample data for testing
│   ├── migrations/             # Version-specific migrations
│   └── stored-procedures/      # Stored procedures (if any)
├── diagrams/                   # Database diagrams
│   ├── er-diagram.png          # Entity relationship diagram
│   └── er-diagram.dbml         # dbdiagram.io source file
├── docs/                       # Documentation
│   ├── schema.md               # Detailed schema documentation
│   └── data-dictionary.md      # Column descriptions and constraints
└── README.md                   # This file
```

## 🔍 Key Design Features

### Soft Delete Pattern
- All major tables include an `IsActive` flag for "soft" deletion, preserving data for analytics and auditing.

### Normalization
- The schema follows 3NF (Third Normal Form) to minimize redundancy while maintaining data integrity.

### Indexing Strategy
- Primary keys are indexed by default
- Foreign keys are indexed to improve join performance
- Additional indexes on commonly queried columns

### Data Integrity
- Foreign key constraints maintain referential integrity
- Check constraints ensure valid data ranges
- Unique constraints prevent duplicate records

## 📊 Database Tables

### Users
Stores user account information.
| Column | Type | Description |
|--------|------|-------------|
| UserId | INT (PK) | Unique identifier |
| UserName | NVARCHAR(100) | User's display name |
| Email | NVARCHAR(255) | Unique email address |
| PasswordHash | NVARCHAR(255) | Hashed password |
| IsActive | BIT | Soft delete flag |
| CreatedOn | DATETIME | Account creation timestamp |

### Groups
Represents expense sharing groups.
| Column | Type | Description |
|--------|------|-------------|
| GroupId | INT (PK) | Unique identifier |
| GroupName | NVARCHAR(100) | Name of the group |
| CreatedBy | INT (FK) | User who created the group |
| IsActive | BIT | Soft delete flag |
| CreatedOn | DATETIME | Group creation timestamp |

*Additional table definitions truncated for brevity. See full documentation in docs/schema.md*

## 🔄 Migration Strategy

For deploying database changes:

1. **Development**: Direct script execution or Entity Framework migrations
2. **Staging/Production**: Controlled migration scripts with versioning
3. **Backup**: Always backup before migration

## 🧪 Testing

- Sample test data provided in `scripts/seed-data.sql`
- Unit tests for stored procedures in `tests/` directory
- Integration test instructions in `docs/testing.md`

## 📱 Applications Using This Database

- [Smart Expense Splitter API](https://github.com/your-username/smart-expense-splitter-api)
- [Smart Expense Splitter UI](https://github.com/your-username/smart-expense-splitter-ui)
- [Notifications Microservice](https://github.com/your-username/smart-expense-splitter-notifications)

## 🌱 Development and Contribution

Contributions welcome! Please follow these steps:
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Create a pull request

Please follow our naming conventions and include proper documentation for any changes.

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 📚 Additional Resources

- [SQL Server Documentation](https://docs.microsoft.com/en-us/sql/sql-server)
- [Database Normalization Guide](https://www.guru99.com/database-normalization.html)
- [SQL Server Performance Tuning](https://www.mssqltips.com/sql-server-categories/9/performance-tuning/)

---

**Created with ❤️ by Aman-Keshri**

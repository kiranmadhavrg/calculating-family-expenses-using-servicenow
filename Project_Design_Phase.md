# Project Design Phase

## Introduction
The Project Design Phase focuses on creating the actual data model, configurations, and automation logic in ServiceNow. This includes creating tables, fields, relationships, and business rules.

### Step 3: Creation of Family Expenses Table
- Navigate to All → Tables → New.
- Enter details: **Label:** Family Expenses, **Name:** Auto-Populated, **New Menu Name:** Family Expenditure.
- Save the configuration.

### Step 4: Creation of Columns (Fields)
- Add fields under Columns:
  1. Number (String)
  2. Date (Date)
  3. Amount (Integer)
  4. Expense Details (String, Max Length: 800)
- Save the configuration.

### Step 5: Making Number Field Auto-Number
- Open the Number field → Enable Advanced View.
- Set **Dynamic Default Value:** Get Next Padded Number.
- Create a Number Maintenance entry for Family Expenses with prefix **MFE**.

### Step 6: Configure the Form
- Navigate to All → Family Expenses → Form Design.
- Make **Number** Read-only and **Date, Amount** Mandatory.
- Save the configuration.

### Step 7: Create Daily Expenses Table
- Navigate to All → Tables → New.
- Enter details: **Label:** Daily Expenses, Add Module to Menu: Family Expenditure.
- Save configuration.

### Step 8: Create Columns for Daily Expenses
- Add fields under Columns:
  1. Number (String)
  2. Date (Date)
  3. Expense (Integer)
  4. Family Member Name (Reference)
  5. Comments (String, Max Length: 800)
- Save configuration.

### Step 9: Configure the Form
- Make **Number** Read-only and **Date, Family Member Name** Mandatory.
- Save the configuration.

### Step 10: Relationship Creation
- Go to All → Relationships → New.
- **Name:** Daily Expenses, **Applies to Table:** Family Expenses, **Daily Expenses Table:** Daily Expenses.
- Save configuration.

### Step 11: Configure Related List
- Open Family Expenses → Configure → Related Lists.
- Add **Daily Expenses** to the related area.
- Save configuration.

### Step 12: Business Rule Creation
- Create a Business Rule under System Definition → Business Rules.
- Name: **Family Expenses BR**, Table: **Daily Expenses**.
- Select **Insert** and **Update** triggers.
- Configure logic to automatically calculate and update Family Expenses totals when a Daily Expense is added or updated.

### Step 13: Relationship Configuration
- Modify Daily Expenses Relationship.
- Apply a query linking **u_date** of Daily Expenses with Family Expenses.

## Architecture and Workflow
The system architecture connects two primary tables — Family Expenses and Daily Expenses — through a one-to-many relationship. When a Daily Expense record is added, the Business Rule updates the total amount in the Family Expenses table.

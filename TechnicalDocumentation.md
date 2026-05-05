# BudgetTracker Technical Documentation

## Overview
BudgetTracker is a comprehensive Power Apps solution for expense management and budget tracking. It includes both a user-friendly Canvas App for day-to-day expense submission and monitoring, and a Model-Driven App for administrative data management. The solution uses custom Dataverse entities, PCF controls for enhanced UI, and Power Automate workflows for automation.

## Architecture

### Technology Stack
- **Frontend**: Power Apps Canvas App (Power Fx) and Model-Driven App (Unified Interface)
- **Backend**: Microsoft Dataverse (Common Data Service)
- **Custom Controls**: Power Apps Component Framework (PCF) with React and Material-UI
- **Automation**: Power Automate workflows
- **Authentication**: Microsoft 365 / Azure AD

### Solution Structure
- **BudgetTrackerApp**: Main solution containing entities, workflows, app modules, and forms
- **BudgetTrackerPCF**: Solution containing custom PCF controls
- **CanvasApp**: The main canvas application with screens and components

## Data Model

### Entities

#### hh_Expenses
- **Purpose**: Stores individual expense records
- **Key Fields**:
  - ExpenseTitle: Title of the expense
  - Amount: Monetary value
  - Description: Detailed description
  - ExpenseStatus: Status (Pending, Approved, Rejected)
  - SubmittedDate: When the expense was submitted
  - ApprovalDate: When approved/rejected
  - ApprovedBy: User who approved
  - Category: Expense category
  - Department: Associated department
- **Relationships**:
  - Belongs to Department
  - Belongs to Category
  - Has many Notifications

#### hh_Budgets
- **Purpose**: Annual department budgets
- **Key Fields**:
  - BudgetName: Name of the budget
  - TotalBudget: Budget amount
  - Year: Budget year
  - Department: Associated department
  - BudgetStatus: Status of the budget

#### hh_Departments
- **Purpose**: Organizational departments
- **Key Fields**:
  - DepartmentName: Name of the department
  - BusinessUnit: Associated business unit
  - Supervisor: Department supervisor (lookup to Users)

#### hh_Categories
- **Purpose**: Expense categories
- **Key Fields**: Category definitions (specific fields not detailed in analysis)

#### hh_Notifications
- **Purpose**: Notification records for expense status changes
- **Relationships**: Linked to Expenses

## Application Screens

### scrExpense (Finance Overview)
- **Purpose**: Main dashboard showing budget status and recent expenses
- **Features**:
  - Budget cards (Total Budget, Approved Expenses, Pending Expenses, Balance)
  - Expense list with filtering
  - New expense creation modal
  - Responsive design with mobile support
  - Dark mode support

### scrReport (Reports)
- **Purpose**: Reporting and analytics (Supervisor access only)
- **Features**: Detailed expense reports and analytics

### scrSearch (Search)
- **Purpose**: Advanced search and filtering of expenses
- **Features**: Search functionality across expense records

## Model-Driven App

### Hospital Budget Management
- **Type**: Model-Driven App (Unified Interface)
- **Purpose**: Administrative interface for managing budget data
- **Client Type**: Web/Mobile (Unified Interface)
- **Included Entities**:
  - System Users
  - hh_Budgets
  - hh_Categories
  - hh_Departments
  - hh_Expenses
  - hh_Notifications
- **Included Views**: All standard and custom views for the entities
- **Forms**: Entity-specific forms for data entry and management
- **Navigation**: Sitemap-based navigation for easy access to different entities

The Model-Driven App provides a data-centric interface for administrators and supervisors to manage budget and expense data using standard Dataverse forms and views, complementing the Canvas App's user-friendly dashboard experience.

## Key Features

### Responsive Design
- Breakpoints: SM (<850px), MD (850-1000px), LG (1000-1400px), XL (>1400px)
- Adaptive layouts and font sizes
- Mobile-specific navigation

### Dark Mode
- Global dark mode toggle
- Consistent theming across components

### User Roles
- **Employees**: Can submit expenses, view own expenses
- **Supervisors**: Can approve/reject expenses, access reports
- Role-based access control

### Budget Management
- Department-specific annual budgets
- Real-time balance calculations
- Expense approval workflow

## Business Logic

### Global Variables (App.fx.yaml)
- `gblCurrentDepartment`: Currently selected department
- `gblCurrentBudget`: Current year's budget for department
- `gblTotalExpenseApproved`: Sum of approved expenses
- `gblTotalExpensePending`: Sum of pending expenses
- `gblTotalSaldo`: Remaining budget
- `gblExpensePrecent`: Budget utilization percentage

### Collections
- `ColMain_Employee`: Licensed users
- `ColMain_Expense`: All expenses
- `ColMain_Department`: Departments
- `ColMain_Category`: Categories
- `ColMain_Notification`: Notifications

## Workflows

### New Expense Notification
- **Trigger**: Expense created/modified
- **Action**: Send email notification to supervisor

### Expense Resolution Notification
- **Trigger**: Expense approved/rejected
- **Action**: Notify submitter of status change

### Manager Approval
- **Purpose**: Handles approval process and field locking

### Lock Approved
- **Purpose**: Locks approved expense records from editing

## PCF Controls

### UI Library Controls
- **CanvasButtonMui**: Material-UI styled button
- **CanvasChartPieRechart**: Pie chart component
- **CanvasCheckboxMui**: Material-UI checkbox
- **CanvasDatepickerMui**: Date picker
- **CanvasSnackbarMuiV2**: Notification snackbar
- **CanvasStepperMui**: Stepper component
- **CanvasMuiInput**: Material-UI input field

All controls support theming, dark mode, and responsive design.

## Security and Permissions

### Data Access
- Users can only see expenses from their department
- Supervisors have elevated access
- Field-level security on sensitive data

### Authentication
- Integrated with Microsoft 365
- User context available via User() function

## Deployment

### Solution Packages
- Managed solutions for production deployment
- Unmanaged for development

### Dependencies
- Microsoft Dataverse
- Power Apps license
- Office 365 for notifications

## Development Notes

### Power Fx Patterns
- Extensive use of variables for responsive design
- Collection-based data management
- Formula-driven UI properties

### Component Architecture
- Reusable components for consistent UI
- Component libraries for complex controls

### Data Relationships
- Lookup fields for referential integrity
- Cascading updates via workflows

## Future Enhancements

Based on the codebase analysis:
- Enhanced reporting capabilities
- Advanced analytics and dashboards
- Integration with external financial systems
- Mobile app development
- AI-powered expense categorization

## Conclusion

BudgetTracker is a comprehensive expense management solution built on the Microsoft Power Platform. It demonstrates best practices in low-code development, responsive design, and business process automation. The modular architecture with custom controls and workflows provides a scalable foundation for organizational expense tracking.</content>
<parameter name="filePath">c:\Users\MayckellPerez\Documents\Practices\BudgetTracker\TechnicalDocumentation.md
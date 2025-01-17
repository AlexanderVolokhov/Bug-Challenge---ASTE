# Paylocity Benefits Dashboard application - QA Bug Reports

This repository contains **UI and functional bug reports** found in a **Sample Benefits Dashboard** application. The application allows an employer to add, edit, and delete employees and their dependents, while previewing benefits costs.

## Overview

- **Application Purpose**  
  The app provides a preview of employee benefit costs. Employers can:
  1. **Add Employees**  
  2. **Edit Employees**  
  3. **Delete Employees**  

- **Key Assumptions**  
  - All employees are paid \$2,000 per paycheck before deductions.  
  - There are 26 paychecks in a year.  
  - The cost of benefits is \$1,000/year per employee.  
  - Each dependent incurs a \$500/year cost.  

- **User Stories & Acceptance Criteria** (Gherkin-style)  
  - **Scenario 1: Add Employee**  
    ```
    GIVEN an Employer
      AND I am on the Benefits Dashboard page
    WHEN I select Add Employee
    THEN I should be able to enter employee details
      AND the employee should save
      AND I should see the employee in the table
      AND the benefit cost calculations are correct
    ```
  - **Scenario 2: Edit Employee**  
    ```
    GIVEN an Employer
      AND I am on the Benefits Dashboard page
    WHEN I select the Action Edit
    THEN I can edit employee details
      AND the data should change in the table
    ```
  - **Scenario 3: Delete Employee**  
    ```
    GIVEN an Employer
      AND I am on the Benefits Dashboard page
    WHEN I click the Action X
    THEN the employee should be deleted
    ```

## Bugs Discovered

We (QA Team) have created separate issues (GitHub Issues) for each bug:

1. **[UI-001] Name Fields Reversed**  
   - The table displays the employee’s `firstName` under the “Last Name” column, and `lastName` under “First Name.”  

2. **[UI-002] Intermittent 401 on /Prod/api/employees + Missing Logout Button Post-Error**  
   - The `/Prod/api/employees` endpoint sometimes returns `401 Unauthorized` or `403 Forbidden` due to missing or expired credentials in the front-end request.  
   - **HAR File**: See `auth-issue.har` for detailed request/response logs.

3. **[UI-003] Table Layout Bug on Smaller Screens (Desktop & Mobile) — Actions Column Cut Off**  
   - The right side of the table (including the Actions column) is truncated or hidden when viewed on a narrow window, preventing the user from seeing edit/delete icons.

4. **[UI-004] Favicon 403 Error**  
   - A `403 Forbidden` appears in the console when the browser automatically requests `favicon.ico`.


## How to View and Reproduce Bugs

1. **Clone or Access the Repo**  
   - Go to the Issues tab to see a list of open bugs.  
   - Each issue has a **title**, **description**, **reproduction steps**, **expected vs. actual results**, and any **attachments** (screenshots, HAR files).

2. **Screenshots & HAR Files**  
   - We’ve included **screenshots** in each issue so you can visualize the UI error.  
   - For **[UI-002] Authorization Issue**, we attached a `HAR` file demonstrating both **failing (401)** and **successful (200)** requests with the proper **Basic Auth** header using Postman.

3. **Testing the Bugs**  
   - Launch the Sample Benefits Dashboard application (if you have the environment).  
   - Use **DevTools (Network tab)** in your browser to confirm you see the same behavior (missing auth header, truncated table, reversed columns, etc.).  
   - If you have Postman, replicate the successful request with `Authorization: Basic <base64EncodedCreds>` to confirm the server returns `200 OK`.

4. **Re-Testing After Fixes**  
   - When a developer **fixes** an issue, they will reference the GitHub issue in their Pull Request using `Fixes #<issue_number>`.  
   - Once merged, the issue automatically closes, and you can **re-test** in the staging environment to confirm the bug is resolved.

## Contributing

- **Reporting New Bugs**  
  - If you discover additional issues, please open a new GitHub Issue with clear steps to reproduce, screenshots, and environment details.

- **Contact**  
  - If you have any questions about these bug reports, ping the QA team on Slack/ MS Teams or create a comment on the relevant GitHub Issue.


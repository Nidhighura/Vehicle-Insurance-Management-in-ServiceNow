**Vehicle Insurance Management System** is a platform designed to automate and streamline the management of vehicle insurance processes. It enables organizations to handle policy creation, renewals, claims, document storage, and approvals through a centralized digital workflow. The system provides automated notifications for policy expiry and renewals, along with dashboards and reports for real-time monitoring. By replacing manual processes, it improves efficiency, ensures compliance, and enhances transparency in managing vehicle insurance activities. 🚗📊

[Business Objectives](#business-objectives)
[Execution](#Execution)
[ Data Architecture](#DataArchitecture)



## Business Objectives 

The main objective of implementing Vehicle Insurance Management in ServiceNow is to make the vehicle insurance process digital and automated. This will help the organization manage insurance requests more easily and efficiently.

The system will reduce manual work by allowing users to submit insurance requests online instead of using paper or manual processes. It will also help in processing requests faster and making approvals and renewals quicker.

All insurance records will be stored in one centralized system, making it easier to track and manage them. Standardized workflows will also ensure that all required documents and procedures are followed properly.

Overall, this system will improve transparency, reduce errors, save time, and ensure that all vehicle insurance processes follow the required legal and organizational policies. 🚗📄



## Execution

The implementation of the Vehicle Insurance Management solution in ServiceNow will follow a structured roadmap divided into key milestones to ensure smooth development, testing, and deployment. The roadmap includes catalog creation, form configuration, approval workflow integration, testing, and final deployment.

### Catalog Creation
The first milestone focuses on creating a structured and user-friendly service catalog for vehicle insurance services. This includes identifying different insurance request types such as new policy requests, policy renewals, and claims. Appropriate catalog categories and service items will be defined, and catalog items will be created with clear titles and descriptions. Collaboration with fleet administrators and approval teams will ensure the accuracy of information and alignment with existing ITSM service structures.

### Form Setup
In this stage, dynamic forms will be designed to collect all necessary insurance request details. Catalog item forms will be built using variables to capture information such as vehicle details, policy type, insurer information, and policy expiry date. Dynamic field visibility will be implemented based on the type of request, and mandatory fields will be configured to ensure complete and accurate submissions. These forms will also align with automation processes and document validation requirements.

### Approval Integration
This milestone focuses on automating approval workflows for insurance-related actions. Approval chains will be defined, such as approvals from team managers or designated approval officers. The workflows will be configured using Flow Designer in ServiceNow. Additionally, audit logs and automated email notifications will be enabled to maintain transparency and proper tracking of approval activities.

### Testing
During the testing phase, the complete lifecycle of insurance requests will be validated. Unit testing will be performed for each catalog item, and end-to-end scenarios such as new policy requests, renewals, and claims will be simulated. Approvals, task creation, notifications, and document handling will be verified. User Acceptance Testing (UAT) will be conducted with stakeholders, and any identified defects will be documented and resolved.

### Deployment
The final milestone involves deploying the vehicle insurance management solution into the production environment. A deployment checklist will be finalized, and workflows along with catalog items will be migrated to production. After deployment, system performance and user feedback will be monitored. Training sessions will be conducted for users and processing teams, and proper support and maintenance processes will be established to ensure smooth system operation.



# Data Architecture


    ┌─────────────────────────────────────────────────────────┐
    │                     USER (Employee)                     │
    │        Submits Vehicle Insurance Request via            │
    │            Service Portal / Service Catalog             │
    └──────────────────────────┬──────────────────────────────┘
                               │
                               ▼
                  ┌────────────────────────────┐
                  │      Catalog Item          │
                  │  "Vehicle Insurance       │
                  │   Request Form"           │
                  └─────────────┬─────────────┘
                                │ creates
                                ▼
                  ┌────────────────────────────┐
                  │       Request (REQ)        │
                  │   Top‑Level Request        │
                  └─────────────┬─────────────┘
                                │ generates
                                ▼
                  ┌────────────────────────────┐
                  │     Requested Item (RITM)  │
                  │ Vehicle Insurance Request  │
                  └─────────────┬─────────────┘
                                │ triggers
                                ▼
                  ┌────────────────────────────┐
                  │        Flow Designer       │
                  │ "Vehicle Insurance Flow"   │
                  └─────────────┬─────────────┘
                                │
                 ┌──────────────┼───────────────┐
                 ▼              ▼               ▼
           Manager Approval   Policy Check    Document Upload
                │                 │                 │
                ▼                 ▼                 ▼
          Approved? ──────────────┘           Store Documents
            │
       ┌────┴─────┐
       ▼          ▼
    Approved    Rejected
       │            │
       ▼            ▼
    Create Task   Notify User
    for Insurance Close Request
    Team
       │
       ▼
    Policy Created / Updated
       │
       ▼
    Notification Sent to Employee
       │
       ▼
    Request Closed / Completed
    



## Automation Logics

### Policy Expiry Auto Calculation
When a new insurance policy is created, the system automatically calculates the policy expiry date based on the policy start date.
```javascript
(function executeRule(current, previous) {

    if (current.start_date) {
        var expiry = new GlideDateTime(current.start_date);
        expiry.addYears(1);
        current.expiry_date = expiry;
    }

})(current, previous);
```

### Automatic PDF Generation
When a policy record is saved, the system automatically generates a PDF document containing the policy details and attaches it to the record.
```javascript
(function executeRule(current, previous) {

    var pdf = new GlidePDFGenerationAPI();
    pdf.createPDF(current.sys_id, "insurance_policy_pdf");

})(current, previous);
```

### Automation 3: Renewal Expiry Auto Population
When a renewal request is created, the system automatically calculates the new expiry date based on the renewal start date.
```javascript
(function executeRule(current, previous) {

    if (current.renewal_start_date) {
        var newExpiry = new GlideDateTime(current.renewal_start_date);
        newExpiry.addYears(1);
        current.new_expiry_date = newExpiry;
    }

})(current, previous);
```

## Business Rules 

Business Rules are implemented in the Vehicle Insurance Management System to automate system behavior, enforce business logic, and maintain data consistency. These rules run on the server side whenever a record is created, updated, or modified. By using Business Rules, the system ensures that insurance policies and claim records are processed automatically without requiring manual intervention.

###  UI Policy Configuration on Claims Table for Section Visibility

In this subtask, a UI Policy is configured on the Claims Data table to control the visibility of form sections based on the approval status selected by the user.

#### Scenario:
If the Approval Status is set to "Approved", the Claim Settlement Details section should become visible so that the settlement information can be entered.

#### Implementation Steps:

Navigate to UI Policies in ServiceNow.

Click New to create a new UI Policy.

Select the Table as Claims Data.

Provide an appropriate Short Description.

Set the Condition as Approval Status is Approved.

Save the UI Policy.

In the UI Policy Actions related list, create a new action.

Select the Claim Settlement Details section.

Set Visible = True.

Save and test the UI Policy on the Claims form.

This configuration ensures that settlement details are only visible when the claim has been approved.

### UI Policy Configuration on Claims Table for Fields Visibility

This subtask focuses on controlling the visibility of specific fields on the Claims form based on user selections.

#### Scenario:
If the Approval Status is set to "Rejected", the Reason for Rejection field should appear so that the admin can provide a valid reason for rejecting the claim.

#### Implementation Steps:

Navigate to UI Policies in ServiceNow.

Click New to create a new UI Policy.

Select the Table as Claims Data.

Provide an appropriate Short Description.

Set the Condition as Approval Status is Rejected.

Save the UI Policy.

In the UI Policy Actions related list, click New.

Select the Reason for Rejection field.

Set Visible = True.

Save and test the UI Policy on the Claims form.

This configuration ensures that the rejection reason is captured whenever a claim is rejected, improving transparency and record accuracy.


# Phase 3: UI/UX Development & Customization
# Phase 3 – UI/UX Development & Validations

In this phase, the user interface and form validations were implemented in ServiceNow for the **Vehicle Insurance Claim** catalog item.

## Catalog Item
Vehicle Insurance Claim

## Variables Created

The following variables were created for the claim form:

1. Policy Number (Single Line Text)
2. Vehicle Number (Single Line Text)
3. Accident Date (Date)
4. Accident Description (Multi Line Text)
5. Upload Damage Photo (Attachment)
6. Chassis Number (Single Line Text)
7. Engine Number (Single Line Text)
8. Driving License (Single Line Text)
9. Email Address (Single Line Text)
10. Mobile Number (Single Line Text)

---

# Catalog Client Script Validations

## Validation 1 – Mobile Number Validation
Ensures the user enters a valid 10 digit mobile number.

## Validation 2 – Email Validation
Validates the email format.

## Validation 3 – Chassis Number Validation
Ensures the chassis number length is valid.

## Validation 4 – Engine Number Validation
Checks the engine number format.

## Validation 5 – Driving License Validation
Validates the driving license number.

## Validation 6 – Vehicle Number Validation
Checks the vehicle number format.

## Validation 7 – Policy Number Validation
Ensures policy number is valid.

## Validation 8 – Accident Date Validation
Prevents selecting a future date.

## Validation 9 – Accident Description Required
Ensures description is entered before submission.

## Validation 10 – Email Required
Email field must not be empty.

## Validation 11 – Mobile Required
Mobile number must be entered.

## Validation 12 – Policy Required
Policy number must be filled.

## Validation 13 – Vehicle Required
Vehicle number must be filled before submission.

---

# Technologies Used

- ServiceNow
- Catalog Items
- Catalog Variables
- Catalog Client Scripts
- JavaScript


# Phase 4: Data Migration& Security Controls

## Data Handling
In this phase, all customer-related data such as New Client registrations, Policy Renewals, and Insurance Claims are stored in their respective database tables. This ensures proper organization and structured management of information within the Vehicle Insurance Management System.

To automate the data handling process, Process Automation techniques are implemented using ServiceNow Catalog Items. The variables entered by users through the catalog forms are automatically captured and mapped to the corresponding custom tables: New Clients Data, Renewal Data, and Claims Data. This approach helps in maintaining accurate records and simplifies data tracking and management.

###  Creation of Flow using Flow Designer Tool

In this subtask, a Flow is created using the ServiceNow Flow Designer to automate the process of capturing user input from catalog items and storing it in the appropriate custom tables.

The Flow Designer helps automate backend processes without requiring complex scripting. It connects catalog item submissions with database operations, ensuring that all submitted data is properly recorded in the system.
<img width="975" height="404" alt="image" src="https://github.com/user-attachments/assets/6257e43b-f89f-4228-99d8-31c8710ba37a" />
<img width="975" height="567" alt="image" src="https://github.com/user-attachments/assets/9e0ffacd-e08d-41d1-9a23-e63584f91efd" />



###  Configuring Trigger Conditions

The trigger condition defines when the flow should start executing. In this project, the flow is triggered whenever a user submits a catalog item related to vehicle insurance services.

For example:

When a user submits a New Insurance Request

When a user submits a Policy Renewal Request

When a user submits a Claim Request

Once the catalog item is submitted, the flow is automatically triggered to process the captured information.
<img width="1600" height="592" alt="image" src="https://github.com/user-attachments/assets/fc9d29ba-16fc-4cf5-8835-ff03d7a34f6f" />


###  Configuring Actions

After the trigger condition is met, the system performs specific actions within the flow. These actions are responsible for storing the submitted data in the respective custom tables.

The actions configured in the flow include:

Creating a new record in the appropriate table (New Clients Data, Renewal Data, or Claims Data).

Mapping catalog variables to table fields.

Saving customer details, policy information, and claim details into the database.

This automated process ensures that all data entered by users is accurately recorded, reducing manual work and improving overall system efficiency.
<img width="1289" height="725" alt="image" src="https://github.com/user-attachments/assets/bdf6507a-ae8b-4165-9333-c24a7e1ec9db" />
<img width="1284" height="651" alt="image" src="https://github.com/user-attachments/assets/c2c5a465-60c7-434b-8e32-8c380ddc127e" />

## Access Control

Access control is implemented in the Vehicle Insurance Management System to ensure data security and protect sensitive information. Users or clients are allowed to submit requests such as New Insurance Registration, Policy Renewal, and Claims through the catalog interface. However, they are not granted direct access to the underlying database tables.

To enforce this restriction and maintain secure data handling, Access Control Rules (ACLs) are configured within ServiceNow. These rules control the read, write, create, and delete permissions for records and fields based on the roles assigned to users. This ensures that only authorized users, such as administrators, can view or modify the data stored in the database tables.

### User Creation

In this subtask, user accounts are created in the ServiceNow system to allow individuals to access the application based on their responsibilities.

Steps:

Navigate to User Administration → Users.

Click on New to create a new user.

Enter the required details such as User Name, Email ID, and Department.

Save the user record.

Assign appropriate roles to the user based on their access level.

This step ensures that every person accessing the system has a unique user account.

### Role Creation

Roles are created to define different levels of access within the system. Each role determines what actions a user can perform.

Steps:

Navigate to User Administration → Roles.

Click New to create a new role.

Provide a Role Name and description.

Save the role.

Assign the role to users who require that level of access.

For example:

Admin Role – Full access to tables and records

Client/User Role – Access only to submit catalog requests

#### Subtask 3: ACL Creation

Access Control Rules (ACLs) are configured to restrict or grant permissions to specific tables, records, or fields.

Steps:

Navigate to System Security → Access Control (ACL).

Click New to create a new ACL rule.

Select the Table Name (e.g., Claims Data, Renewal Data, New Clients Data).

Define the Operation such as Read, Write, Create, or Delete.

Specify the Roles that are allowed to perform the operation.

Save and test the ACL rule.

By implementing ACLs, the system ensures that only authorized users can access sensitive insurance data, while regular users can interact with the system only through the catalog interface.

## Data Integrity
Data integrity is maintained in the Vehicle Insurance Management System by implementing field validation rules and automation mechanisms. These measures ensure that the data entered into the system is accurate, complete, and reliable.

Mandatory fields are enforced on the client side to prevent users from submitting incomplete forms. This ensures that important information such as customer details, policy information, and claim data is always captured.

In addition, automation is implemented to send reminders to clients regarding important events such as policy expiry or renewal dates. This is achieved through Scheduled Jobs, Events, and Email Notifications in ServiceNow. These automated processes help keep users informed and ensure timely actions without manual intervention.

### 1. Creation of Events in ServiceNow

In this subtask, system events are created to trigger notifications when specific actions occur within the application.

Steps:

Navigate to System Policy → Events → Registry.

Click New to create a new event.

Provide the Event Name and description.

Save the event.

These events act as triggers that initiate notifications or automated actions within the system.

### 2. Configuration of Notifications using Event in ServiceNow

Notifications are configured to automatically send emails to users when specific events are triggered.

Steps:

Navigate to System Notification → Email → Notifications.

Click New to create a notification.

Provide a Notification Name and description.

Select the Table related to the notification.

In the When to Send section, choose the event created earlier.

Configure the Recipients such as clients or administrators.

Define the Email Subject and Message.

Save and test the notification.

This ensures that users receive timely alerts and updates.

### 3. Creation of Email Script for Dynamic Links

Email scripts are created to generate dynamic links within email notifications. These links allow users to directly navigate to the relevant form or record in the system.

Steps:

Navigate to System Notification → Email → Email Scripts.

Click New to create an email script.

Write the script to generate a dynamic URL that redirects the user to the required form.

Save the email script.

Attach the script to the notification email template.

This feature improves user convenience by allowing quick access to the required records directly from email.

### 4. Configure Scheduled Jobs to Automate Email Reminders

Scheduled Jobs are configured to automatically trigger reminder emails at specific intervals.

Steps:

Navigate to System Definition → Scheduled Jobs.

Click New to create a scheduled job.

Define the schedule (daily, weekly, or monthly).

Configure the script or condition to check for policy expiry or renewal dates.

Trigger the appropriate event to send reminder notifications.

Save and test the scheduled job.

This automation ensures that clients receive timely reminders about policy renewals and other important updates.


# Phase 5: Deployment, Documentation & Final Presentation

## Reporting & Dashboards

Reporting and Dashboards are used in the Vehicle Insurance Management System to visualize and analyze important data related to insurance policies, renewals, and claims. Reports help administrators monitor system activities, track policy records, and make data-driven decisions. Dashboards provide a centralized view where multiple reports can be displayed together for quick insights.

### Dashboard Creation in ServiceNow

In this activity, a dashboard is created to display reports related to insurance data.

Steps:

Navigate to the ServiceNow Home Page.
Click on the All Menu.
Type Dashboard in the search bar.
Navigate to Usage and Governance → Dashboards.
Click on the New button to create a new dashboard.
Provide the Name as Insurance Data Reports.
Save the dashboard.
This dashboard will be used to display multiple reports related to the Vehicle Insurance Management System.

### Reports Creation in ServiceNow

In this activity, a report is created to visualize data stored in the custom tables.

Steps:

Navigate to the ServiceNow Home Page.

Click on the All Menu.

Type Reports in the search bar.

Navigate to Usage and Governance → Reports.

Click on the New button to create a new report.

Provide the Name as New Policies Data.

Select Data Source as Table.

Choose the Table as New Clients Data.

Click Next.

Select the Report Type as Bar Chart.

Open the Configure tab.

Select the Group By and Additional Group By fields as required.

Save and Run the Report.

After generating the report, it can be added to the previously created dashboard Insurance Data Reports so that administrators can easily view policy data in a graphical format.

## Troubleshooting


During the development and implementation of the Vehicle Insurance Management System in ServiceNow, certain issues may occur related to forms, automation, notifications, or system performance. Troubleshooting helps identify and resolve these issues to ensure the system functions smoothly and efficiently.

Below are some common problems encountered during the project along with their possible solutions.

### 1. Form & Field Issues

Sometimes fields may not appear on the form or may not behave as expected.

##### Possible Causes:

Incorrect field configuration

UI Policy conditions not applied correctly

Fields not added to the form layout

##### Solution:

Verify the Form Layout configuration.

Check UI Policies and Client Scripts affecting the field.

Ensure the field is added to the correct section of the form.

### 2. Business Rule / Workflow Errors

Automation scripts such as Business Rules or Flows may fail to execute correctly.

##### Possible Causes:

Incorrect script logic

Business rule conditions not met

Flow Designer trigger not configured properly

##### Solution:

Check the Business Rule script syntax.

Verify the trigger conditions in Flow Designer.

Use System Logs to identify errors.

### 3. Notification Issues

Sometimes email notifications may not be triggered or delivered to users.

##### Possible Causes:

Incorrect event configuration

Notification conditions not satisfied

Email settings not configured properly

##### Solution:

Verify the Event Registry configuration.

Ensure the notification is linked to the correct event.

Check the email logs to confirm whether the notification was sent.

### 4. Data & Security Issues

Users may face access problems or may not be able to view records.

##### Possible Causes:

Access Control Rules (ACLs) restricting permissions

Incorrect role assignment

Field-level security restrictions

##### Solution:

Verify ACL configurations.

Ensure the user has the correct roles assigned.

Test permissions using impersonation.

### 5. Performance / UI Issues

Slow loading forms or interface problems may affect user experience.

##### Possible Causes:

Too many client scripts or UI policies

Large data records

Network or browser-related issues

##### Solution:

Optimize client scripts and UI policies.

Reduce unnecessary fields or scripts on the form.

Clear browser cache and check system performance.

### 6. Common Debugging Tips

To resolve issues effectively, developers can use the following debugging techniques:

Check System Logs for error messages.

Use Script Debugger to analyze script execution.

Verify Flow Designer execution logs.

Test changes in a development environment before deployment.

Use impersonation to test user access and permissions.

## Adherence to Timelines

Adhering to project timelines is essential for the successful implementation of the Vehicle Insurance Management System. Each phase of the project is carefully planned and executed within defined schedules to ensure smooth development, testing, and deployment. Proper coordination, regular reviews, and progress tracking help maintain project efficiency and avoid delays.

### 1. Requirement Gathering Phase

In this phase, all functional and technical requirements related to the Vehicle Insurance Management System are collected and finalized within the agreed timeline.

Key activities include:

Identifying system requirements for vehicle registration, policy management, and claims processing.

Conducting review sessions with stakeholders to validate requirements.

Documenting all requirements clearly to avoid rework during later phases.

### 2. Design & Configuration Phase

During this phase, the system design and configuration are completed according to predefined milestones.

Key activities include:

Designing forms for Vehicle Details, Policy Information, Claims, and Payment Data.

Configuring ServiceNow components such as tables, UI policies, catalog items, and workflows.

Implementing workflows for policy issuance, renewal processing, and expiry reminders within the planned sprint duration.

### 3. Development & Scripting Phase

In this phase, automation and system logic are developed using ServiceNow scripting and configuration tools.

Key activities include:

Implementing Business Rules, Client Scripts, and Flow Designer automations.

Following coding standards to ensure maintainable and efficient code.

Performing unit testing immediately after implementing each automation component to detect issues early.

### 4. Testing Phase

The testing phase ensures that the system functions correctly before deployment.

Key activities include:

Executing functional test cases to verify system features.

Conducting User Acceptance Testing (UAT) to validate system behavior from a user perspective.

Logging and resolving defects within the defined Service Level Agreement (SLA) to maintain project timelines.

### 5. Deployment Phase

This phase involves moving the completed solution to the production environment.

Key activities include:

Raising change requests for deployment within the scheduled release window.

Performing pre-deployment validation to ensure readiness.

Conducting post-deployment smoke testing to confirm that the system works as expected.

### 6. Communication & Tracking

Effective communication and monitoring help ensure that the project remains on schedule.

Key activities include:

Conducting regular project stand-up meetings and progress reviews.

Tracking tasks and milestones using tools such as project trackers, Agile boards, or spreadsheets.

Updating the project status regularly to reflect progress against deadlines.

### 7. Risk & Mitigation

Potential risks that may affect the project timeline are identified early and managed effectively.

Examples include:

Delays in requirement approvals

Testing bottlenecks

Configuration or integration issues

Mitigation strategies such as buffer timelines, parallel task execution, and early stakeholder involvement help keep the project on track.

### 8. Documentation Deliverables

Proper documentation is maintained throughout the project lifecycle to ensure smooth knowledge transfer and system maintenance.

Deliverables include:

Technical documentation describing system configuration and automation.

Troubleshooting guides for resolving common issues.

User training materials and guides provided before the system goes live.

## Innovation

To improve the system functionality, an automated email reminder feature can be implemented. This feature will automatically notify users before their vehicle insurance policy expires so that they can renew the policy on time.

## Document Functional Overview

The Vehicle Insurance Management System is designed to streamline and automate the management of vehicle insurance policies, renewals, and claims within the organization. The system provides a centralized platform that improves operational efficiency, enhances customer experience, and ensures accurate data handling.

Key functional benefits of the system include:

#### 1. Reduced Manual Effort

The system automates various processes such as policy registration, policy renewal, claim submission, and approval workflows. Automation through Business Rules, Flow Designer, and scheduled jobs significantly reduces manual work and improves operational efficiency.

#### 2. Improved Customer Experience

Customers can easily submit new insurance requests, renewal requests, and claim applications through the self-service interface. Automated notifications and reminders keep users informed about important events such as policy expiry and claim status updates, providing a smooth and proactive user experience.

#### 3. Increased Data Accuracy

Data validation rules, mandatory fields, and restricted inputs ensure that all required information is captured correctly. This reduces the chances of incomplete or incorrect data being stored in the system and helps maintain data integrity.

#### 4. Enhanced Decision-Making

The system provides dashboards and reports that allow administrators to analyze policy data, claim records, and customer activity. These insights help management make informed decisions and monitor the overall performance of the insurance management process.



## Explanation Clarity

The system workflow is designed in a clear and structured way so that users can easily understand how insurance policies are created, managed, and renewed. Each automation process such as expiry calculation, PDF generation, and renewal processing is implemented with clear business logic to ensure smooth system operation.

## Scalability & Future Plan

The system is designed to be scalable so that additional features can be added in the future. In upcoming updates, features such as advanced reporting, AI-based claim analysis, and integration with external insurance databases can be implemented to enhance the overall functionality of the system.


# Phase 6: QA & UAT Testing Results

#Renewal Policy User’s Testing
The system manages vehicle insurance policy renewals by tracking policy expiry dates and automatically generating renewal records. It sends advance notifications to users so they can take timely action before the policy expires. The renewal information is checked for accuracy and then updated in the system, ensuring continuous insurance coverage and proper compliance with policy requirement
subtask 1 : catlog testing
Here is a short explanation for Catalog Testing in ServiceNow that you can use in your report:

Catalog Testing:
Catalog Testing is performed to verify that the service catalog items in ServiceNow work correctly and provide the expected services to users. It checks whether catalog forms, fields, and workflows function properly when a user submits a request. During testing, different inputs are entered to ensure validations, approvals, and request generation work as expected. This testing ensures that users can easily request services through the catalog and that the system processes those requests accurately and efficiently.
<img width="1600" height="706" alt="1000197911" src="https://github.com/user-attachments/assets/b178fe63-fadc-4777-b4df-ac501d00a7a4" />
<img width="1260" height="648" alt="1000197909" src="https://github.com/user-attachments/assets/426ed286-76f2-47b4-9162-02a695962532" />
<img width="1295" height="660" alt="1000197910" src="https://github.com/user-attachments/assets/86c632de-7e65-4b54-b225-ce96c7800359" />

subtask 2 :Database Tables Testing
Database Tables Testing:
Database Tables Testing is done to check whether all data is correctly stored and updated in the system database. It verifies that records such as policy details, customer information, expiry dates, and renewal status are properly inserted and maintained in the tables of ServiceNow. This testing ensures data accuracy, consistency, and reliable system performance.
<img width="1600" height="576" alt="1000197918" src="https://github.com/user-attachments/assets/fed9c6dd-3b1d-48d8-9c44-f6a34324d3e7" />
<img width="1600" height="724" alt="1000197912" src="https://github.com/user-attachments/assets/276df4a0-020d-46fe-98ec-b9d26e3fd888" />
subtask 3 :Emails Testing

Email Testing is performed to verify that the system sends correct email notifications to users. It checks whether alerts related to policy renewal, expiry reminders, and other updates are generated properly in ServiceNow. This testing ensures that the email content, subject, and recipient details are accurate and that notifications are delivered on time.
<img width="1600" height="576" alt="1000197918" src="https://github.com/user-attachments/assets/58c694f0-ef82-492b-bcc2-2e02420dde80" />
<img width="1327" height="810" alt="1000197919" src="https://github.com/user-attachments/assets/1d7658c5-0b9a-4071-aa0d-d0731b640fa0" />

subtasks 4 : Reminder’s Email Testing
Reminder’s Email Testing is performed to ensure that automatic reminder emails are sent to users before the insurance policy expires. It verifies that the reminder notifications generated in ServiceNow contain correct policy details and are delivered to the right recipients at the scheduled time. This helps users take timely action for policy renewal.

<img width="1600" height="686" alt="1000197920" src="https://github.com/user-attachments/assets/3840a84f-1cc1-48c6-8658-86cfbaec49e1" />
<img width="1319" height="676" alt="1000197921" src="https://github.com/user-attachments/assets/30caad39-0f4a-48b7-9453-d4d58c78df6b" />

# Phase 7: Conclusion

The Vehicle Insurance Management System built on ServiceNow simplifies the process of managing vehicle insurance policies, renewals, and claims. It allows users to register vehicles, view policy details, track expiry dates, and receive automatic renewal reminders. The system improves transparency, reduces manual work, and helps manage insurance operations more efficiently through automated workflows and real-time reports.

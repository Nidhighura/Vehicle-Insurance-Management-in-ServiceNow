# Phase 1: Requirement Analysis & Planning

## Business Objectives 

The main objective of implementing Vehicle Insurance Management in ServiceNow is to make the vehicle insurance process digital and automated. This will help the organization manage insurance requests more easily and efficiently.

The system will reduce manual work by allowing users to submit insurance requests online instead of using paper or manual processes. It will also help in processing requests faster and making approvals and renewals quicker.

All insurance records will be stored in one centralized system, making it easier to track and manage them. Standardized workflows will also ensure that all required documents and procedures are followed properly.

Overall, this system will improve transparency, reduce errors, save time, and ensure that all vehicle insurance processes follow the required legal and organizational policies. 🚗📄

## Functional Scope

The Vehicle Insurance Management System is designed to automate and streamline the management of vehicle insurance policies within an organization.

The system allows users to:

* Create and manage vehicle insurance policies
* Track policy start and expiry dates
* Submit insurance claims
* Upload and manage policy documents
* Receive automated notifications for policy expiry and renewal
* Generate PDF documents for insurance records
* Implement approval workflows for claims
* Manage renewal of expired policies

This system reduces manual work, improves efficiency, and ensures better tracking of insurance activities.
This system reduces manual work, improves efficiency, and ensures better tracking of insurance activities.

Stakeholder Mapping – Vehicle Insurance Management

The Vehicle Insurance Management solution implemented in ServiceNow involves several key stakeholders who play important roles in the insurance request and management process. Each stakeholder has specific responsibilities, expectations, and benefits from the automation of the system.

<img width="1442" height="1339" alt="image" src="https://github.com/user-attachments/assets/3e555663-20cc-4561-9dbc-a11a5f2a171f" />


## Execution Roadmap

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

# Phase 2: Backend Development & Configurations

## Data Architecture

###  1. New Insurance Data Table
    
  ####  Creation of Table
        · Navigate to: System Definition > Tables.
        
        · Click New to create a new table.
        
        · Fill in Table Information:
        
        ·     Name: u_insurance_clients_data
        
        ·     Label: Insurance clients Data
        
        · Click Submit to create the table.
        <img width="975" height="383" alt="image" src="https://github.com/user-attachments/assets/16bfadab-273f-4749-b5f7-eeb470b437c3" />
        <img width="975" height="425" alt="image" src="https://github.com/user-attachments/assets/415d52f4-32dd-4ce3-97ba-7836cf8655b0" />
        <img width="1600" height="371" alt="image" src="https://github.com/user-attachments/assets/1c07a696-abbe-40ca-b327-430ac91b8813" />
        
      ####   Creation of fields
        ·   In ServiceNow, fields are created at the table level. To create a field, you first need to identify the table where the field will reside.
        
        1.   In the Application Navigator (left-side panel), type Tables in the search bar.
        
        2.   Under System Definition, click Tables. This will take you to a list of all tables in the system.
        
        Select the Table to Add the Field
        
        ·     From the list of tables, search for and select the table you want to add a field to. For example, if you want to add a field to the Insurance clients Data                   table:
        
        1.   Type "Insurance clients Data" in the search box or scroll through the list.
        
        2.   Click on the Insurance clients Data table name. You’ll now see a list of all fields (columns) associated with the Insurance clients Data table.
        
        Open the Table's Columns
        
        ·   After selecting the table, you'll be brought to a view that lists all the columns (fields) that currently exist on that table.
        
        · To create a new field (column), go to the Columns tab (this is where all fields for the selected table are listed).
        
        Create a New Field
        
        1.   In the Columns tab, click the New button located at the top-right corner of the page to create a new field.
        
        2.   You’ll now be prompted with a form where you need to define the new field. The following fields need to be filled out:
        
      ####  Define Field Properties
        Fill in the following details for your new field:
        
        1. Column Label (Field Label)
        
        ·     Description: This is the name that will be displayed on the forms, lists, and records.
        
        ·     Example: Candidate Name-String Type
        
        2. Column Name
        
        ·     Description: This is the internal name of the field and is auto-generated based on the column label. It should be unique for each field. Do not manually edit                this unless necessary.
        
        ·     Example: candidate_name
        
        ·     Description: The type of field determines the kind of data it will store. You need to choose the correct type based on the data you want to store (e.g., text,               number, date, etc.). Some of the most common types include:
        
        o   String: For short text values (e.g., name, description).
        
        o   Integer: For numbers without decimals (e.g., age, number of items).
        
        o   Choice: A dropdown list of options.
        
        o   Reference: A field that links to another table (e.g., linking to a User table).
        
        o   Boolean: A true/false checkbox.
        
        o   Date: For a date picker field.
        
        o   Date/Time: For both date and time.
        
        ·     Example: String, Choice, Reference
        
        3.  Max Length (Optional)
        
        ·     Description: If you are creating a string-type field, you can specify the maximum length of the text allowed.
        
        ·     Example: 255 characters (default length for a string field).
        
        4. Mandatory
        
        ·     Description: Check this box if the field should be required when creating or updating records.
        
        ·     Example: For a "Customer Name" field, this might be required.
        
        5. Default Value (Optional)
        
        ·     Description: You can set a default value for the field if desired. This value will appear automatically when creating a new record.
        
        ·     Example: Set the default value to "New Customer" for a "Customer Name" field.
        
        6. Read-Only
        
        ·     Description: Check this box if the field should be read-only (users cannot modify its value). This is commonly used for calculated or system-generated fields.
        
        ·     Example: "Created Date" or "Record Number".
        
        7: Save the Field
        
        ·     Once you’ve configured all the necessary field properties, click Submit or Save to create the field.
        
        ·     After saving, ServiceNow will create the new field and add it to the list of columns for the selected table.
        
        <img width="1351" height="785" alt="image" src="https://github.com/user-attachments/assets/719a3297-8fef-48dc-b569-e11fec1721f4" />
        <img width="1380" height="505" alt="image" src="https://github.com/user-attachments/assets/f14de952-2da7-4dd2-b27e-7c6703df3b6e" />
        
      ####  Add the Field to a Form (Optional)
        After creating the field, you may want to add it to a form so that users can view or update it.
        
        1.   To do this, navigate to System UI > Forms in the application navigator.
        
        2.   Select the form you want to modify (e.g., Incident form).
        
        3.   Open the Form Designer (click on the "Design" icon).
        
        4.   From the Field Navigator on the left side, search for the new field you created.
        
        5.   Drag the field onto the form layout where you want it to appear.
        
        6.   Click Save or Publish to apply the changes.
        
        Test the New Field
        
        ·    Go to a record in the table where the field was added (e.g., create a new incident or record).
        
        ·     Check if the new field appears on the form.
        
        ·     Verify the field behaves as expected (e.g., required, read-only, etc.).
        
        Key Field Types in ServiceNow:
        
        ·     String: Short text input (e.g., a name, description).
        
        ·     Integer: Whole numbers.
        
        ·     Choice: Dropdown list with predefined options.
        
        ·     Reference: A reference field to another table (e.g., referencing an User table).
        
        ·     Date: A date picker.
        
        ·     Date/Time: A combination of date and time.
        
        ·     Boolean: Checkbox (True/False).
        
        ·     Currency: Currency field with monetary values.
        
       ####  Creation of Sections using Form Designer 
        Navigate to the Table/Form
        
        Go to the table where you want to add a section (Insurance clients Data).
        
        Open any record from that table.
        
        Open Form Design
        
        Right-click on the form header.
        
        Select Configure → Form Design.
        
        This opens the Form Design editor.
        
        Add a Section
        
        In the Form Design editor, click the + Section button (usually on the top left).
        
        A new section placeholder will appear on your form layout.
        
        You can drag and drop it where you want.
        
        Configure Section Properties
        
        Click on the newly created section.
        
        On the right-hand side, set:
        
        Label → The section names (Policy Details, Vehicle Details).
        
        Columns → Choose 1, 2, or 3 column layout depending on how you want fields displayed.
        
        Tab (optional) → If you want this section to appear under a separate tab on the form.
        
        Add Fields to the Section
        
        From the Available Fields list on the left, drag and drop the fields into your new section.
        
        You can also create new fields directly from here by clicking + Field.
        
        Reorder Sections
        
        Drag the section up or down to reorder it within the form.
        
        You can also drag fields between sections if needed.
        
        Save & Publish
        
        Once your layout is ready, click Save or Publish.
        
        Your new section will now appear on the form
        <img width="1495" height="781" alt="image" src="https://github.com/user-attachments/assets/14b233b3-5af9-4648-bc89-f57dbfed8f44" />

### 2. Renewal Data Table

  #### Creation of Table
    · Navigate to: System Definition > Tables.
    
    · Click New to create a new table.
    
    · Fill in Table Information:
    
    ·     Name: u_renewal_data
    
    ·     Label: Renewal Data
    
    · Click Submit to create the table.
   Fields to Create in the Renewal Data Table
   <img width="1052" height="911" alt="image" src="https://github.com/user-attachments/assets/1a8d1ceb-b4e7-4f77-b8de-1711988d776f" />

   
### 3. Claims Data Table
    #### Creation of Table
        · Navigate to: System Definition > Tables.        
        · Click New to create a new table.        
        · Fill in Table Information:        
            · Name: u_claims_data            
            · Label: Claims Data            
            · Click Submit to create the table.






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



## Innovation

To improve the system functionality, an automated email reminder feature can be implemented. This feature will automatically notify users before their vehicle insurance policy expires so that they can renew the policy on time.

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

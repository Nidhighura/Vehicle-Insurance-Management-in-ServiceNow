
## Data Architecture

  1. New Insurance Data Table
    
     Activity 1: Creation of Table
        · Navigate to: System Definition > Tables.
        
        · Click New to create a new table.
        
        · Fill in Table Information:
        
        ·     Name: u_insurance_clients_data
        
        ·     Label: Insurance clients Data
        
        · Click Submit to create the table.
        <img width="975" height="383" alt="image" src="https://github.com/user-attachments/assets/16bfadab-273f-4749-b5f7-eeb470b437c3" />
        <img width="975" height="425" alt="image" src="https://github.com/user-attachments/assets/415d52f4-32dd-4ce3-97ba-7836cf8655b0" />
        <img width="1600" height="371" alt="image" src="https://github.com/user-attachments/assets/1c07a696-abbe-40ca-b327-430ac91b8813" />
        Activity 2: Creation of fields
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
        
        Activity 3: Define Field Properties
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
        Activity 4:  Add the Field to a Form (Optional)
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
        
        Activity 5:  Creation of Sections using Form Designer 
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

2. Renewal Data Table
   Activity 1: Creation of Table
    · Navigate to: System Definition > Tables.
    
    · Click New to create a new table.
    
    · Fill in Table Information:
    
    ·     Name: u_renewal_data
    
    ·     Label: Renewal Data
    
    · Click Submit to create the table.
   Fields to Create in the Renewal Data Table
   <img width="1052" height="911" alt="image" src="https://github.com/user-attachments/assets/1a8d1ceb-b4e7-4f77-b8de-1711988d776f" />

   
3. Claims Data Table
     Activity 1: Creation of Table
        · Navigate to: System Definition > Tables.        
        · Click New to create a new table.        
        · Fill in Table Information:        
            · Name: u_claims_data            
            · Label: Claims Data            
            · Click Submit to create the table.






## Automation Logics

### Automation 1: Policy Expiry Auto Calculation
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

### Automation 2: Automatic PDF Generation
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

In this project, Business Rules are implemented to automate key processes, maintain data integrity, and ensure compliance within the Vehicle Insurance Management System. Business Rules run on the server side and are triggered automatically whenever a record is inserted, updated, or deleted in the system.

Several important Business Rules are used in this project. These include automatically setting the insurance policy expiry date based on the policy start date, sending reminders to users for upcoming policy renewals, validating claim details before submission, automatically assigning claim approvals to the appropriate authority, and updating the status of policies and claims based on system actions.

By implementing these Business Rules, the system reduces manual effort, minimizes errors, and ensures that all data related to vehicle insurance policies and claims remains accurate and consistent across the platform.



## Innovation

To improve the system functionality, an automated email reminder feature can be implemented. This feature will automatically notify users before their vehicle insurance policy expires so that they can renew the policy on time.
## Explanation Clarity

The system workflow is designed in a clear and structured way so that users can easily understand how insurance policies are created, managed, and renewed. Each automation process such as expiry calculation, PDF generation, and renewal processing is implemented with clear business logic to ensure smooth system operation.
## Scalability & Future Plan

The system is designed to be scalable so that additional features can be added in the future. In upcoming updates, features such as advanced reporting, AI-based claim analysis, and integration with external insurance databases can be implemented to enhance the overall functionality of the system.

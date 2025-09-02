# Salesforce MCP Server - Prompts

This guide provides sample prompts demonstrating how to interact with various MCP tools. Each tool is listed with a brief description and example prompts to illustrate its functionality.


## 🛡️ Safety & Best Practices

* **Request Focused Assistance:** When prompting Claude, instruct the MCP to only focus on what you've specifically asked for. This prevents unintended actions and keeps responses relevant.
* **Always Request Confirmation:** Tell Claude to always ask for explicit confirmation before making any changes to your Salesforce org. This provides an important safety check before modifications are applied.
* **Request Action Plans:** Ask Claude to create and present a plan of proposed changes before executing them. This allows you to review and approve the specific actions that will be taken in your org.
* **APEX Coding**: If you are asking it to write APEX code or LWC's, just add a line telling it not to attempt any deployments, unless you are using an IDE which can do so.
* **Example Prompt:** "Please analyze my custom objects, but before making any changes, show me a plan of what you're proposing to modify and wait for my approval."



## salesforce_apex_deploy  

**NOTE:** This Apex deploy will only work in an IDE with AI capabilty ie Cursor, VSCODE with MCP Enabled tooling.

Use following prompt as one big prompt for custoer to deploy your classes.

-  Please use sf apex generate class to deploy the apex classes
- Advise Cursor to create a proper Class Name: AccountMonthlyProcessor
- File Location: force-app/main/default/classes/
- Deployment Target: My Salesforce org with alias 'trailblaze'
- Generate the class file and its meta.xml using Salesforce CLI
- Verify the file contents and Deploy the class to my org
- Use this guide for connected apps deployment [agentforce.md](https://github.com/iimransarwar/mcp-server-salesforce/blob/main/agentforce.md)

## salesforce_apex_test_runner

**Description:**  
Executes Apex unit tests within Salesforce. You can dynamically run tests, retrieve execution results, and check code coverage. Useful for validating code quality and deployment readiness.

**Operations:**
- `runTests`: Execute Apex test classes dynamically
- `getTestResults`: Retrieve test execution results
- `getCoverage`: Get code coverage information for a class
- `getOrgWideCoverage`: Get organization-wide code coverage metrics

**Example Prompts:**

```
"Run all tests in the MyApexTestClass and show me the results."
"Get the code coverage for OpportunityTrigger to ensure it meets deployment standards."
"Execute dynamic Apex tests for the custom functionality."
"Run tests for only the billing-related classes."
"Check if our Apex classes meet the 75% code coverage requirement for deployment."
"Get the test results for the job I just ran with ID '707xx000000001A'."
"Run all local tests in the org and report on failures."
"What's our organization-wide code coverage percentage?"
```

## salesforce_bulk_dml_records

**Description:**  
Performs bulk data manipulation using Salesforce Bulk API 2.0. This tool supports operations like bulk insert, update, delete, upsert, and job status checks. It is ideal for handling large volumes of records efficiently.

**Operations:**
- `bulkInsert`: Create many new records efficiently
- `bulkUpdate`: Modify many existing records (requires Id)
- `bulkDelete`: Remove many records (requires Id)
- `bulkUpsert`: Insert or update many records based on external ID field
- `getJobStatus`: Check the status of a previously submitted bulk job

**Example Prompts:**

```
"Bulk insert 10,000 new Account records into Salesforce."
"Update Lead statuses in bulk for our recent marketing campaign."
"Delete outdated records using a bulk job and check its status."
"Upload these 5,000 contact records using bulk API."
"Bulk upsert product inventory using external SKU field as the identifier."
"What's the status of my bulk job with ID 'a07xx00000006Gx'?"
"Create 200 new opportunity records in bulk with default values."
"Update all cases from last year to 'Closed' status using bulk operations."
```

## salesforce_cpq

**Description:**  
Manages Salesforce CPQ (Configure, Price, Quote) operations. This tool provides comprehensive functionality for the quoting process, product configuration, contracts, document generation, and approvals.

**Operations:**
- **Quote API**: Create, retrieve, update quotes and manage quoting actions
- **Configuration API**: Configure and price product bundles
- **Contract API**: Amend and renew CPQ quotes
- **Document API**: Generate and manage quote documents
- **Approvals API**: Manage the quote approval process

**Example Prompts:**

```
"Create a new quote for customer Acme Corp with standard products."
"Configure a product bundle for the networking hardware quote."
"Generate a PDF document for quote Q-12345 using our company letterhead template."
"Submit quote Q-12345 for approval to the sales manager."
"Amend the existing contract to add three new product licenses."
"Calculate pricing for this product configuration with volume discounts applied."
"Renew the customer's subscription contract with a 10% uplift."
"Get the CPQ settings for our price calculation rules."
"Update the line items on quote Q-12345 to reflect the new product versions."
"Add the Premium Support product to this quote and recalculate the price."
```

## salesforce_debug_logs

**Description:**  
Retrieves and analyzes Apex debug logs. You can fetch logs for the current day, filter by user or transaction ID, and perform log analysis to identify error messages.

**Operations:**
- `getLogs`: Retrieve Apex debug logs for the current day, optionally filtered by user or transaction ID
- `setupLogs`: Provide instructions to set up debug logs if none are found
- `analyzeLogs`: Analyze a specific log for error messages

**Example Prompts:**

```
"Retrieve all debug logs for today for user JohnDoe."
"Analyze the latest log for error messages in the Payment process."
"Provide instructions for setting up debug logs if none are found."
"Show me debug logs from transaction ID '07Lxx00000123ABC'."
"Analyze this log ID '07Lxx00000123ABC' for any exception messages."
"How do I configure debug logging for our integration user?"
"Find all errors in today's logs related to the Opportunity trigger."
"What debug level settings should I use to troubleshoot SOQL issues?"
```

## salesforce_describe_object

**Description:**  
Gets detailed schema metadata for any Salesforce object, including fields, relationships, help texts, formulas, and permission details. This helps you understand the structure of your objects.

**Parameters:**
- `objectName`: API name of the object (e.g., 'Account', 'Contact', 'Custom_Object__c')
- `outputFormat`: Output format: 'text' (default) or 'json'

**Example Prompts:**

```
"Describe the Account object and list all its fields and relationships."
"Show the detailed schema for the Opportunity object, including help texts."
"Get extended field properties for the custom object Customer_Feedback__c."
"What fields are available on the Lead object?"
"Describe the Case object in JSON format."
"Show me all lookup and master-detail relationships on the Contact object."
"What are the required fields on the Opportunity object?"
"Tell me about the field-level security settings for the custom object Project__c."
```

## salesforce_dml_records

**Description:**  
Handles basic data manipulation operations on Salesforce records such as insert, update, delete, and upsert. Ideal for standard CRUD operations.

**Operations:**
- `insert`: Create new records
- `update`: Modify existing records (requires Id)
- `delete`: Remove records (requires Id)
- `upsert`: Insert or update based on external ID field

**Example Prompts:**

```
"Insert a new Account with the name 'Acme Corp'."
"Update the Case status for record Id 003XX0000ABC."
"Delete the record with Id 500XX0000XYZ from Salesforce."
"Create a new Contact for John Doe with email john@example.com."
"Update the opportunity stage to 'Closed Won' for ID 006xx000012345."
"Upsert leads using email address as the external ID field."
"Insert three new tasks assigned to the current user."
"Create a new case and associate it with account 'Global Media'."
```

## salesforce_email_manager

**Description:**  
Manages email templates and notifications. This tool enables you to send custom emails, work with template-based emails using merge fields, and manage notification settings.

**Operations:**
- `sendEmail`: Send custom emails via API (only after confirming recipient)
- `sendTemplateEmail`: Send emails using Salesforce Email Templates with merge fields
- `listEmailTemplates`: List available email templates
- `updateEmailTemplate`: Update email template content
- `getNotificationSettings`: Fetch notification settings
- `updateNotificationSettings`: Modify notification settings

**Example Prompts:**

```
"Send a custom email to a confirmed contact using our template."
"List all available email templates in Salesforce."
"Update notification settings for the support team emails."
"Send a welcome email to new customer john@example.com after confirmation."
"Use the 'Case Resolution' template to send an email to case contact."
"What email notification settings are currently configured for our org?"
"Update the 'Invoice Reminder' email template with new payment instructions."
"Send a template-based email to opportunity contact and save it as an activity."
```

## salesforce_execute_apex

**Description:**  
Executes anonymous Apex code blocks or invokes Apex REST endpoints. This tool is useful for running quick tests or integrating custom logic dynamically.

**Operations:**
- `executeAnonymous`: Run anonymous Apex code blocks
- `apexRest`: Call Apex REST endpoints with different HTTP methods (GET, POST, PUT, PATCH, DELETE)

**Example Prompts:**

```
"Execute the anonymous Apex block to update lead statuses."
"Call the Apex REST endpoint for retrieving customer data."
"Run custom Apex logic to process bulk data operations."
"Execute this Apex code: List<Account> accts = [SELECT Id FROM Account LIMIT 5]; System.debug(accts);"
"Call the Apex REST endpoint /services/apexrest/CaseManagement/12345 with a GET request."
"Post new order data to the Apex REST endpoint /services/apexrest/OrderAPI."
"Run Apex to recalculate all opportunity amounts."
"Execute a SOQL query through anonymous Apex to find duplicate contacts."
```

## salesforce_lwc_manager

**Description:**  
Manages Lightning Web Components (LWC) by creating, updating, deleting, and fetching metadata. It streamlines deployment of LWC bundles and associated resources.

**Operations:**
- `createLWC`: Create new Lightning Web Components
- `updateLWC`: Update existing LWC files and metadata
- `deleteLWC`: Remove Lightning Web Components
- `fetchLWCMetadata`: Get metadata and dependencies for existing LWCs

**Note:** This process is sequential – first create the bundle, then add resources.

**Example Prompts:**

```
"Create a new Lightning Web Component named 'CustomDashboard'."
"Update the metadata for the existing LWC 'AccountOverview'."
"Delete the LWC that is no longer needed from the org."
"Create a new LWC called 'contactCard' with HTML, JS, and XML files."
"Update the JavaScript file in the 'opportunityList' component."
"Fetch all metadata and dependencies for the 'accountMap' LWC."
"Make this Lightning component visible in App Builder by setting isExposed to true."
"Create an LWC with data table functionality to display contacts."
```

## salesforce_manage_field

**Description:**  
Creates or modifies custom fields on any Salesforce object. It supports various field types (Text, Number, Date, etc.) and properties like required, unique, or external ID.

**Operations:**
- `create`: Create new custom fields
- `update`: Modify existing field properties

**Field Types:**
- Text, Number, Date, Lookup, Master-Detail, Picklist, MultiselectPicklist
- Checkbox, Currency, DateTime, Email, Percent, Phone
- TextArea, LongTextArea, Html, Url

**Properties:**
- Required, Unique, External ID, Length, Scale, Precision, etc.
- For relationship fields: referenceTo, relationshipName, relationshipLabel, deleteConstraint

**Example Prompts:**

```
"Add a Rating__c picklist field to the Account object."
"Modify the length of the Description field on the Opportunity object."
"Create a new lookup field from Contact to Account."
"Add a Currency field called 'Estimated_Value__c' to the Lead object."
"Create a required checkbox field on Case called 'Escalated_To_Manager__c'."
"Make the 'Product_Code__c' field an external ID and set it as unique."
"Add a multi-select picklist field 'Selected_Services__c' to the Opportunity object."
"Create a master-detail relationship from Project_Task__c to Project__c."
```

```
{
  "operation": "create",
  "objectName": "Account",
  "fieldName": "Rating28",
  "type": "Picklist",
  "label": "Rating",
  "picklistValues": [
    { "label": "Excellent", "isDefault": false },
    { "label": "Good", "isDefault": false },
    { "label": "Fair", "isDefault": false },
    { "label": "Poor", "isDefault": false }
  ],
  "updateFLS": true,
  "permissionSetName": "API_Permissions",
  "outputFormat": "text",
  "postAction": {
    "description": "After field creation, fetch the API name of the 'API_Permissions' permission set and run anonymous Apex to assign read/write permissions for field Account.Rating28__c.",
    "executeApex": true
  }
}

```

## salesforce_manage_metadata

**Description:**  
Manages custom metadata types, custom labels, and custom settings. This tool supports bulk import/export of metadata and helps maintain configuration settings across your org.

**Operations:**
- `createMetadata`: Create new custom metadata records
- `updateMetadata`: Update existing custom metadata records
- `deleteMetadata`: Remove custom metadata records
- `getMetadataRecords`: Retrieve custom metadata records
- `bulkInsertMetadata`: Add multiple custom metadata records at once
- `createCustomLabel`: Create new custom labels
- `updateCustomLabel`: Update existing custom labels
- `getCustomLabels`: Retrieve custom labels
- `createCustomSetting`: Create custom setting records
- `updateCustomSetting`: Update custom setting records
- `deleteCustomSetting`: Remove custom setting records
- `getCustomSettings`: Retrieve custom setting records

**Example Prompts:**

```
"Create a new custom metadata record for feature toggles."
"Update custom labels for our Salesforce application."
"Export the current custom settings for backup."
"Create a new entry in the Integration_Settings__mdt custom metadata type."
"Update the API_Key__c field in the Authentication_Settings__mdt record."
"Add a new custom label 'InvalidEmail' with value 'Please enter a valid email'."
"Get all records from the Feature_Flag__mdt custom metadata type."
"Create an org-level custom setting record for payment processing configuration."
"Update the user-level Custom Settings for the current user's preferences."
```

## salesforce_manage_object

**Description:**  
Creates or modifies custom objects in Salesforce. You can define new objects with fields and relationships or update existing object configurations.

**Operations:**
- `create`: Create new custom objects with fields, relationships, and settings
- `update`: Modify existing object settings, labels, sharing model

**Parameters:**
- Name field type options: Text or AutoNumber
- Sharing model options: ReadWrite, Read, Private, ControlledByParent
- Labels, descriptions, and other metadata details

**Example Prompts:**

```
"Create a custom object called Customer_Feedback__c with relevant fields."
"Update sharing settings for the Service_Request__c object."
"Modify the label of the custom object from 'Feedback' to 'Customer Feedback'."
"Create a new Project__c object with auto-number format PRJ-{0000}."
"Set the sharing model for Vendor__c object to Private."
"Update the plural label for the Expense__c object to 'Expenses'."
"Create a custom object for tracking employee certifications."
"Change the description of the Inventory__c object to clarify its purpose."
```

## salesforce_manage_security

**Description:**  
Manages Salesforce security settings such as profiles, permission sets, sharing rules, and field-level security. Essential for controlling user access and data visibility.

**Operations:**
- `assignPermissionSet`: Assign permission sets to users
- `revokePermissionSet`: Remove permission sets from users
- `createPermissionSet`: Create new permission sets
- `updatePermissionSet`: Modify existing permission sets
- `updateProfileObjectPermissions`: Adjust object permissions for profiles
- `updateProfileFieldPermissions`: Configure field-level security for profiles
- `updateOrgWideDefaults`: Change organization-wide sharing defaults
- `createSharingRule`: Establish new sharing rules
- `updateSharingRule`: Modify sharing rule criteria or access levels
- `deleteSharingRule`: Remove sharing rules
- `createPublicGroup`: Create new public groups
- `addMembersToGroup`: Add users/roles to groups
- `removeMembersFromGroup`: Remove members from groups
- `updateSessionSettings`: Configure session security settings
- `updatePasswordPolicy`: Modify password policies

**Example Prompts:**

```
"Assign the Permission Set 'Sales_Rep' to user Id 005XX0000ABC."
"Modify profile permissions to grant access to the custom object Order__c."
"Update organization-wide sharing settings for the Case object."
"Create a new permission set called 'Finance_Team' with access to the budget object."
"Set up a sharing rule to give the Support team read access to all accounts."
"Revoke API access from the 'Contractor' profile."
"Update field-level security to hide credit card fields from the Support profile."
"Create a public group for Marketing team members and add specific users."
"Configure password policy to require 12 characters and 90-day expiration."
```

## salesforce_modify_settings

**Description:**  
Performs general Salesforce administration tasks by modifying backend configuration settings. Use it to update sharing settings, email deliverability, feature toggles, and more.

**Operations:**
- `updateSharing`: Change sharing model for specific objects
- `updateSharingSettings`: Modify org-wide sharing settings
- `updateDeliverability`: Configure email deliverability status
- `toggleFeature`: Turn features on or off
- `updateSetting`: Modify various metadata settings
- `addPublicGroupMembers`: Add members to public groups
- `addQueueMembers`: Add members to queues

**Configurable Settings:**
- ChatterSettings, LightningExperienceSettings, EntitlementProcess
- EntitlementSettings, CaseSettings, LeadSettings, ActivitySettings
- KnowledgeSettings, MobileSettings, CommunitySettings/ExperienceBundle
- LiveAgentSettings, EmailAdministrationSettings, and more

**Example Prompts:**

```
"Change the sharing settings for Cases from Private to ReadWrite."
"Toggle the Chatter feature on for all users."
"Update email deliverability settings to ensure emails are sent properly."
"Enable Lightning Experience for all users in the organization."
"Update Case settings to auto-close cases after 7 days of inactivity."
"Configure Knowledge settings to allow article attachments."
"Add these three users to the Support queue for case assignment."
"Enable enhanced notes feature in the org settings."
"Update Lead settings to use auto-response rules for web-to-lead submissions."
```

## salesforce_pub_sub

**Description:**  
Manages Salesforce Pub/Sub API for event-driven integrations. This tool enables you to work with platform events and change data capture (CDC) events for real-time messaging and data synchronization.

**Operations:**
- `listEvents`: List available platform events and CDC events
- `getEventSchema`: Retrieve the schema of a specific event
- `publishEvent`: Publish events to the event bus
- `createSubscription`: Create a subscription to receive events
- `receiveEvents`: Receive events from a subscription

**Example Prompts:**

```
"List all available platform events in our Salesforce org."
"Get the schema for the Order_Processed__e event to see its structure."
"Publish a new inventory update event to the event bus."
"Create a subscription to receive Account change events in real time."
"Receive recent events from our order processing subscription."
"What CDC events are available for the Opportunity object?"
"Publish a notification event when a high-value opportunity closes."
"Subscribe to Contact change events with earliest replay option."
"Create a real-time data feed using CDC events for the Account object."
"Retrieve the last 10 events from my custom event subscription."
```

## salesforce_query_records

**Description:**  
Queries Salesforce records using SOQL, supporting parent-child and multi-level relationship queries. It allows filtering, sorting, and detailed data retrieval across objects.

**Query Types:**
1. **Parent-to-child query** (e.g., Account with Contacts):
   - objectName: "Account"
   - fields: ["Name", "(SELECT Id, FirstName, LastName FROM Contacts)"]

2. **Child-to-parent query** (e.g., Contact with Account details):
   - objectName: "Contact"
   - fields: ["FirstName", "LastName", "Account.Name", "Account.Industry"]

3. **Multiple level query** (e.g., Contact → Account → Owner):
   - objectName: "Contact"
   - fields: ["Name", "Account.Name", "Account.Owner.Name"]

4. **Related object filtering**:
   - objectName: "Contact"
   - fields: ["Name", "Account.Name"]
   - whereClause: "Account.Industry = 'Technology'"

**Tips:**
- Use dot notation for parent relationships (e.g., "Account.Name")
- Use subqueries in parentheses for child relationships (e.g., "(SELECT Id FROM Contacts)")
- Custom relationship fields end in "__r" (e.g., "CustomObject__r.Name")

**Example Prompts:**

```
"Get all Accounts created this month along with their Contacts."
"Query Opportunities over $100k with related Account details."
"Retrieve Contacts and include their Account's industry field."
"Find all Cases created last week where the Contact's Account is in the Healthcare industry."
"Get Leads with their converted Accounts and Opportunities."
"Query all Contacts where the Account owner is 'Jane Smith'."
"Find Products related to Opportunities that are Closed Won in Q1."
"Show me Accounts with more than 5 open Cases and their respective Case owners."
```

## salesforce_report_manager

**Description:**  
Manages Salesforce Reports and Dashboards. Retrieve report metadata and results, download reports, create/update reports, and schedule dashboard refreshes.

**Operations:**
- `getReportMetadata`: Retrieve report metadata structure
- `downloadExcelReport`: Download reports in Excel format
- `queryReportData`: Extract report data without saving changes
- `createReport`: Build new reports
- `updateReport`: Modify existing reports
- `getDashboardMetadata`: Get dashboard component information
- `updateDashboard`: Modify dashboard components and settings
- `createDashboard`: Create new dashboards
- `listReports`: Get available reports
- `listDashboards`: Get available dashboards
- `scheduleReport`: Set up automated report runs
- `getReportInstances`: View scheduled report history
- `listReportTypes`: Get available report types

**Example Prompts:**

```
"Fetch the sales report for Q1 and download it in Excel format."
"Create a custom report for customer service cases."
"Update the dashboard to include the latest sales metrics."
"Get the detailed metadata for the 'Monthly Sales' report."
"Run the pipeline report with a filter for deals over $50k."
"Schedule the weekly activity report to run every Monday at 8 AM."
"List all dashboards in the Sales folder."
"Create a new dashboard showing top performing salespeople and their deals."
"Query the customer satisfaction report data with this month's filter applied."
```

## salesforce_search_all

**Description:**  
Searches across multiple Salesforce objects using SOSL (Salesforce Object Search Language). It supports wildcards, filters, and advanced search options, enabling a broad search across your org.

**Search Features:**
- Wildcards: Use * and ? for partial matching
- Object-specific WHERE, ORDER BY, and LIMIT clauses
- Search scope options: ALL FIELDS, NAME FIELDS, EMAIL FIELDS, PHONE FIELDS, SIDEBAR FIELDS
- WITH clauses support: DATA CATEGORY, DIVISION, METADATA, NETWORK, PRICEBOOKID, SNIPPET, SECURITY_ENFORCED
- Access control with "updateable" and "viewable" filters

**Example Structure:**
```json
{
  "searchTerm": "John",
  "objects": [
    { 
      "name": "Account", 
      "fields": ["Name"], 
      "limit": 10 
    },
    { 
      "name": "Contact", 
      "fields": ["FirstName", "LastName", "Email"] 
    }
  ]
}
```

**Example Prompts:**

```
"Search for 'John' across Accounts and Contacts."
"Perform an advanced search for 'Cloud*' in Account names and industries."
"Find all records mentioning 'network issue' across Cases and Knowledge Articles."
"Search for 'Smith' in name fields only across all objects."
"Find 'security' in knowledge articles and include a snippet of matching text."
"Look for phone number '415*' in Contact and Lead records."
"Search for 'software' across Accounts where industry is 'Technology'."
"Find any email addresses containing 'acme.com' in Contacts and Leads."
```

## salesforce_search_objects

**Description:**  
Searches for Salesforce standard and custom objects by name pattern. This is useful when you need to identify related objects or find objects with similar names.

**Parameters:**
- `searchPattern`: The pattern to search for in object names (e.g., 'Account', 'Order', 'Custom')

**Example Prompts:**

```
"Search for objects related to 'Order' to find both Order and ServiceOrder__c."
"List all objects that have 'Account' in their name."
"Find standard and custom objects matching the pattern 'Contact'."
"What objects contain 'History' in their name?"
"Find all custom objects related to 'Project'."
"Look for any objects that might store customer data."
"Search for objects with 'Transaction' in their name."
"What objects in our org are related to 'User' entities?"
```

## salesforce_tooling_execute

**Description:**  
Executes requests via the Salesforce Tooling API for metadata operations. Run raw API calls, execute anonymous queries, and create or update metadata like Apex classes and triggers.

**Operations:**
- `execute`: Make raw API calls to Tooling API endpoints
- `query`: Run SOQL queries against Tooling API objects
- `create`: Create records via the Tooling API (ApexClass, ApexTrigger, etc.)
- `update`: Update existing records via the Tooling API
- `delete`: Delete records via the Tooling API

**Example Prompts:**

```
"Query all Apex classes using the Tooling API."
"Create a new Apex class called 'CustomHandler' via the tooling interface."
"Update metadata for a custom object using the Tooling API."
"Find all inactive workflow rules using the Tooling API."
"Create a new Apex trigger on the Account object via the Tooling API."
"Query all custom fields on the Lead object using the Tooling API."
"Delete the outdated validation rule from the Opportunity object."
"Check the status of all active validation rules in the system."
```

## salesforce_user_manager

**Description:**  
Automates user management tasks in Salesforce. Create new users, update existing ones, assign profiles or permission sets, and retrieve user details.

**Operations:**
- `createUser`: Create a new User record
- `updateUser`: Update an existing User record
- `assignProfile`: Assign a Profile to a User
- `assignPermissionSet`: Assign a Permission Set to a User
- `getUserDetails`: Retrieve User details and status

**Example Prompts:**

```
"Create a new user with the role Sales_Rep and assign the default profile."
"Update user Id 005XX0000ABC to change their email address."
"Assign the 'Marketing' Permission Set to the specified user."
"Get the details and status of user johndoe@example.com."
"Create a new user for Jane Smith with Standard User profile."
"Update the manager for user Id 005XX0000DEF to be user 005XX0000ABC."
"Assign the System Administrator profile to the specified user."
"Check if user Sarah Johnson is active and when they last logged in."
```

# salesforce_optimiser

## Description
Analyzes Salesforce orgs for best practices and optimization opportunities. This tool performs comprehensive health checks and provides actionable recommendations for improvements in various areas of your Salesforce org.

## Operations
- `runFullAnalysis`: Run a comprehensive health check across all areas
- `checkReleaseUpdates`: Identify pending release updates requiring action
- `reviewApexClasses`: Analyze Apex classes with API versions and last modified dates
- `reviewObjectLimits`: Examine object field counts and approaching limits
- `checkStorageLimits`: Evaluate data storage utilization and largest objects
- `reviewApexTestCoverage`: Assess Apex test coverage against deployment requirements
- `analyzeApiVersions`: Identify outdated API versions across components

## Example Prompts
- "Run a complete health check of my Salesforce org."
- "Check if there are any critical release updates that need my attention."
- "Review all Apex classes in the system and identify which ones are using outdated API versions."
- "Show me objects that are approaching their field limits."
- "Analyze our data storage usage and identify the largest objects."
- "Check if our test coverage meets the 75% requirement for deployment."
- "Identify components using outdated API versions that should be updated."
- "Which objects in our org have the most complex automation?"
- "Are there any critical issues that need immediate attention in our org?"
- "Generate a comprehensive optimization report with actionable recommendations."

## Parameter Options

For Full Analysis:
```json
Please run the Salesforce Optimiser tool with the following operations, make sure to run all operations listed below sequentially: 
{
  "operations": [
    "checkSecuritySettings",
    "checkProfileSettings", 
    "checkReleaseUpdates", 
	"runFullAnalysis",
  ],
  "includeDetails": true,
  "outputFormat": "json",
  "excludeManaged": true
}
After running the optimiser tool, please generate a comprehensive report in plain text with all the maximum detail you can think of.

The report should be formatted clearly with each section labeled and include any recommendations or summaries for each check and create a table for checkSecuritySettings to compare with salesforce best practices.
Goal 1: checkSecuritySettings  should be fully detailed. I want every aspect to be considered.
Goal 2: After analysis create one fully detailed report of both Health and optimization report and Security settings comparison. Everything should be in one document and in a single report.

```

For Release Updates Check:
```json
{
  "operation": "checkReleaseUpdates"
}

Prompt: Can you review all release updates and listdown the one most critical that i should be activating by calling Salesforce optimiser operation.
```

For Apex Class Review:
```json
{
  "operation": "reviewApexClasses"
}
```

For Miltiple Salesforce Limits Analysis:
```json
{
  "operation": "reviewObjectLimits"
}
```

For Test Coverage Analysis:
```json
{
  "operation": "reviewApexTestCoverage"
}
```

For API Version Analysis:
```json
{
  "operation": "analyzeApiVersions"
}
```
For Salesforce sessions/password policy Analysis:
```json
{
  "operation": "checkSecuritySettings"
}
```

For Salesforce Profile Permission  Analysis:
```json
{
  `operation`: `checkProfileSettings`,
  `outputFormat`: `json`,
  `autoFetchAll`: true,
  `includeDetails`: true
}
```

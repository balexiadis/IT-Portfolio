# Project 10: ServiceNow Incident Management & Service Catalog Lab

## Objective
Get familiar with ServiceNow ITSM workflows on a Personal Developer Instance to understand how an IT service desk handles IT incidents and requests. 

## Tools & Technologies
- ServiceNow PDI
	- User Administration
	- Incident Management
	- SLA Management 
	- Service Catalog

## Steps Taken

### Phase 1: Exploring The Dashboard 
Before building anything, I explored the instance to understand how ServiceNow is organised and where each part of the ITSM lifecycle lives.

#### 1. Navigating the Instance
The **All** menu opens the application navigator which groups the platform into applications and modules and can be filtered by name. **Workspaces** gives access to role-based dashboards. 

![ServiceNow UI](images/01-home-ui.png)

#### 2. Service Operations Workspace
Service Operations Workspace is ServiceNow's interface for service desk staff handling tickets. The widgets show my incidents, SLAs, unassigned incidents and catalog tasks, split into "Your work" and "Your team's work". It is currently empty as nothing has been raised yet.

![Service Operations Workspace home](images/02-familiar-dashboard-1.png)

#### Open Incidents
Shows open IT incident tickets and their priority from customers that need to be resolved by the IT helpdesk. For example `Unable to access the shared folder` with a `low` priority.

![Open Incidents](images/02-familiar-dashboard-2.png)

#### Resolved Incidents
Where tickets solved by the helpdesk are. Its a good place to check whether a the issue has already been fixed so the fix can be reused.

![Resolved incidents list](images/03-resolved.png)

#### Knowledge Articles
The help desk's library of troubleshooting guides. They attach articles to incidents, and users can self-serve from them. Example: the Microsoft Outlook Issues article (demo data)

![Knowledge articles list](images/04-knowledge.png)

![Microsoft Outlook Issues article](images/04-knowledge-2.png)

#### 3. Asset Workspace
The Asset Workspace is where hardware assets are tracked. The overview page flags records with missing data and links to asset requests, transfer orders and stock orders. It helps keep track of what equipment exists and where it is.

![Asset Workspace hardware asset overview](images/05-asset-workspace.png)

### Phase 2: Users, Groups, and Roles 
Before creating any tickets I set up the people and teams that would interact with them. A service desk needs someone raising incidents and someone resolving them, with different levels of access.

#### 1. Creating the Users
Since the PDI comes prefilled with various users we will use two of them: `Abel Tuter` and `Abraham Lincoln`. One will be the caller (raises the ticket and the other will be the help desk employee. 

![Users](images/06-users.png)

#### 2. Assigning Roles
`Abel Tuter` will man the help desk so is given the role `itil`. This gives him access to solve incident tickets. As Abraham Lincoln is the caller he will receive no roles and no access. 

![Roles](images/07-roles.png)

#### 3. Added to `Service Desk` Group
Added `Abel Tuter` to the existing Service Desk group. Groups are what incidents get assigned to so tickets go to a team rather than a single person. 

![Group](images/08-group.png)

### Phase 3: Incident Walkthrough
With the correct users and roles setup i walked through a simulated incident to its completion in the service operations workspace

#### 1. Impersonate Service Desk Agent
As `Abel Tuter` was given permissions to handle incident response and was added to the Service Desk group we will impersonate him to walkthrough the task.

![Abel Tuter](images/10-impersonate.png)

#### 2. Creating the Incident
Created a new "Password Reset" ticket for our caller (`Abraham Lincoln`), with category Inquiry/Help and Low impact and Medium urgency. Priority is calculated from impact and urgency rather than set by hand.

**NOTE:** I should have used the `Password Reset` category, i didn't see it. Additionally a Password reset would be categorised as a request rather than an incident however getting an understanding of the workflow was the main point of the exercise.

![New ticket](images/11-new-ticket.png)

#### 3. Assigned the Ticket
Assigned the ticket to the Service Desk group and more specifically us as the fulfiller so the ticket has a clear owner.

![Assigned ticket](images/12-assigned.png)

#### 4. Working the Ticket
When working through the ticket the service desk agent can add comments as well as change the status to something else such as `On Hold` if they are waiting for more information from the caller. On Hold also pauses the SLA timer as the delay is not on them they are awaiting a response. 

![Working ticket](images/13-working-ticket.png)

#### 5. Resolving and Closing the Ticket
Resolved it with a resolution code and resolution notes and then closed it. ServiceNow requires both before it allows resolution, which ensures every ticket has a documented fix.

![Resolved ticket](images/14-resolved.png)

Ticket is now in the resolved incidents list:

![Resolved ticket](images/14-resolved-2.png)

### Phase 4: SLA
I wanted to test how SLA's worked throughout a live incident lifecycle so i used a predefined SLA to test with.

#### 1. Picking an SLA Definition
Chose the `Priority 1 resolution (1 hour)`.It defines that Priority 1 incidents should be resolved within 1 hour:

![SLA](images/15-sla.png)

Has a pause condition of the ticket being on hold with the reason being awaiting caller:

![SLA pause](images/15-pause.png)

and stops when the incident is closed:

![SLA stop](images/15-stop.png)

#### 2. Verifying the SLA Starts
Created a new Priority 1 ticket and verified the SLA's 1 hour countdown began

![SLA timer](images/17-sla-timer.png)

#### 3. Testing the Pause
I tested that the SLA timer would pause by meeting the pause condition of setting the `State` to `On Hold` with the reason being `Awaiting Caller`

![SLA paused](images/18-sla-paused.png)

#### 4. Closing the Ticket
Resolved and closed the ticket and checked the SLA status to verify the SLA timer had finished after we completed the ticket in time

![SLA completed](images/19-sla-completed.png)

### Phase 5: Service Catalog and Approval
Incidents deal with things that are broken but a service desk also deals with requests. I wanted to walk through the flow of employee requesting something, the approver approving the request, and the service desk agent fulfilling the request. 

#### 1. Setting Up Approver Permissions
We have the employee/caller `Abraham Lincoln` and the service desk agent `Abel Tuter`. I now need to set up the `Approver`. I used the user `Adela Cervantsz` and gave her the role `approver_user` to give her those permissions.

![Approver user](images/20-approver-user.png)

#### 2. Setting Manager
I set our callers manager to `Adela Cervantsz` so that when the item is requested the person that must approve it is their manager.

![Set manager](images/21-set-manager.png)

##### 3. Ordering the Item
Impersonating the caller (`Abraham Lincoln`) I ordered an Apple iPhone 13 replacement and answered the request form.

![Order form](images/22-request-phone-1.png)

The order confirmation gave me the request number `REQ0010001`:

![Order confirmation](images/22-request-phone-2.png)

#### 4. Approving the Request
This created an approval for Abrahams manager and department head Adela as soon as the order was placed. I impersonated Adela and approved both requests (one as manager one as dept head)

![Manager approval](images/23-manager-approval.png)
![Both approvals approved](images/23-manager-head-approval.png)

#### 5. Fulfilling the Request
The managers approval triggered the fulfilment task for the service desk. (`"Please fulfill this order"`) which I closed from the Service Operations Workspace.

![Fulfilment task](images/24-abel-fulfill.png)

Closing it created the deployment task (`"Please deploy item to the user"`) which I closed in the standard UI. Each task is created only after the previous one closes.

![Deployment task](images/24-deploy.png)

#### 6. Request Completed
Once the last task closed the flow completed and the request moved to Closed Complete without any manual change.

![Completed request](images/25-request-complete.png)

## Outcome
Got hands on experience and a working understanding of the ServiceNow platform and doing things such as creating users, applying roles, handling an incident from creation to completion, tracking it against the SLA allowed time, and following a catalog request through approval and fulfilment. I gained a deep understanding of how a service desk works.

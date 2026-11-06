# Project 11: Entra ID Identity & Access Management Lab

## Objective
Get hands-on experience with Entra ID to understand how businesses manage user identities and access. This includes: creating users and groups, assigning licences, enforcing conditional access and MFA, and off-boarding users. 

## Tools & Technologies
- Microsoft 365 Admin Centre
- Microsoft Entra ID
- Conditional Access
- Multi-Factor Authentication

## Steps Taken

### 1. Setup M365 Account + Access Admin Centre
I signed up for a Microsoft 365 Business Premium Trial and logged in to the m365 admin centre which gives us access to the tools required for the lab

![M365](images/01-m365.png)

### 2. Creating Users
I created 3 new users (`Test IT, Test Finances, Test Sales`) to simulate a real business environment. I didn't assign licences on creation as i want to assign these via group membership in a later step.

![new users](images/02-new-users.png)

This same step can also be done in Entra ID admin centre and this is the tool we will be using for most steps from here.

![new users](images/02-new-users-entra.png)

### 3. Creating Groups
Created 3 new security groups (`Finance, IT, Sales`) and assigned the corresponding users to each (`Test IT` user assigned to `IT` group, etc). This will allow product licences to be assigned to members of the group rather than on an individual user account basis.

![New Group](images/03-new-groups.png)

### 4. Assigning Licences
Back in 365 Admin Centre i assigned the Microsoft 365 Business Premium licence to each of our 3 groups, IT, Finances, and Sales.

![Assigning Licence](images/04-licence.png)

This then applies the same licence to each of the members of these groups.

![Assigning Licence](images/04-licence-user.png)

### 5. Testing User Sign In 
Verified account 365 access by logging in through `portal.office.com` with `Test IT` account details. This demonstrates that the group licensing does indeed apply to members of the group.

![Verified login](images/05-verified-login.png)

## Conditional Access & MFA

### 6. Disable Security Defaults
Security Defaults can't be used alongside Conditional Access so I disabled them. I also left the option to auto-create replacement policies unticked so that testing the effect of my custom policies becomes easier, no other policies will interfere. This will leave security concerns and should not be done without exercising caution in a live business environment.

![Security Defaults](images/06-security-defaults.png)

### 7. Create Conditional Access Policy
I then created a Conditional Access Policy called `Require MFA - CA-Test` which requires multi-factor authentication for a specific group (`CA-Test`). Security Defaults applied to everyone where as with Conditional Access i can include and exclude certain users or groups.

For this policy i included the `CA-Test` group only.

![include](images/07-include.png)

I also excluded my admin account to avoid getting locked out by any misconfigurations in the policy.

![Exclude](images/07-exclude.png)

I then added the Access Control for the MFA

![Grant](images/07-grant)

### 8. Test MFA Policy
Tried logging in to the `ca.test` account to test the MFA policy. The policy worked correctly, I was prompted to set up a second factor through the Microsoft Authenticator app which is what we were looking for.

![mfa](images/08-mfa.png)

![mfa](images/08-mfa-2.png)

I also successfully set up the MFA and logged into the account 

![mfa](images/08-success.png)

### 9. Location Based Policy
I wanted to test a policy that would block access based on where the device is located. I created a location for Australia and same as before created a new policy.

![location](images/09-named-location.png)

For this one i again included the `CA-Test` group and excluded the admin account. Under `conditions` i included the location i created `Australia`

![location](images/09-conditions-location.png)

and finally under `Access Control` I blocked access. this means whn the policy is enabled users in the `CA-Test` group will be blocked from accessing, and when its disabled they will have access again`

![location](images/09-block.png)

## 10. Testing Location Based Policy
Once again i tried logging into the test account to see if the policy was working. We were denied access when logging in which confirms it is working as it should.

![location](images/10-access-blocked.png)

![location](images/10-log.png)

In order to further confirm it is our specific policy causing the rejection. I turned it off and tried logging in again. 

![location](images/10-off.png)

We were successfully able to log in proving that our specific location policy is working

![location](images/10-worked.png)

## Offboarding

## 11. Offboarding Test User
To simulate a person leaving the company i offboarded the test user `Test Sales`. 

I first deactivated the user account to stop any new sessions being created

![offboarding](images/11-account-disabled.png)

I then revoked all sessions for the user, ending any sessions they are currently logged into

![offboarding](images/11-revoke.png)

and finally removing the user from any groups they were in which removes any permissions they held from being apart of it

![offboarding](images/11-remove-group.png)

## 12. Testing Offboarded User Account
tried loggin in with the offboarded account to confirm access was denied

![offboarding](images/11-locked-account.png)

## Notes
- Security groups are what provide licences and policy to all those who are members whereas Microsoft 365 Groups create a shared mailbox and SharePoint site
- Both Entra ID admin centre and Microsoft 365 Admin Centre work on the same directory so share information. I used Entra ID for the identity and access side and 365 admin centre for the licensing side.

## Outcome
Successfully gained experience with M365 Admin Centre and Entra ID. Created several user accounts verifying they worked and were given the correct licensing based on group membership. Create Conditional Access Policies based around MFA and location. Ran through the offboarding process for a user and verified access was denied at the end.

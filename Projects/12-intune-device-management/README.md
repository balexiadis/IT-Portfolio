# Project 12: Microsoft Intune Windows Device Management Lab

## Objective
Gain experience with Microsoft Intune and how organisations use it to connect and manage Windows devices. This included, joining device to Entra ID, connecting it to Intune, enforcing both a compliance and configuration policy, and finally off boarding the device

## Tools & Technologies
- Microsoft 365 Business Premium
- M365 Admin Centre
- Entra ID
- Microsoft Intune
	- Compliance
	- Configuration
- Windows 11 Enterprise VM

## Steps Taken

### 1. Verified Intune License
I used a previous project’s account `Test IT` for this project. I ensured it had the correct licence that included Intune as accounts without it cannot enrol devices. This account has Microsoft 365 Business Premium so it does have this function.

![License](images/01-license.png)

### 2. Checked Device Join Permissions
In Entra ID, ensured that users are allowed to join devices to Microsoft Entra. If this was set to `None` joining the device in step 4 would be denied.

![device settings](images/02-allowed.png)

### 3. Configured Automatic Intune Enrolment 
Set `MDM user scope` to `Some` and selected the `IT` group which inludes our user. This allows devices connected by members of this group to automatically be enrolled in Intune. I chose to restricted it to `Some` rather than `All` to mirror an organisation doing a small scale rollout/testing.

![MDM](images/03-mdm.png)

### 4. Joined VM to Entra ID
On my Windows 11 VM i navigated to `Access Work or School` > `Connect` and selected `Join this device to Microsoft Entra ID`. Joining it through this method allows the device to be fully managed by Entra ID and Intune

![Entra ID](images/04-vm-intune.png)

I signed in as my `Test IT` account and received confirmation that it was connected to my organisation

![Success](images/04-vm-intune-2.png)

### 5. Verified in Entra ID and Intune
I then verified the connection was successful and the device was recognised in both Entra ID and Intune

![Entra ID](images/05-vm-joined.png)

![Intune](images/05-intune-device-joined.png)

### 6. Created a Compliance Policy
In the Intune admin centre i created a Compliance Policy that required devices to have a firewall, antivirus, and antispyware on it to be deemed 'Compliant'. Any devices missing one or all of these would be labelled as non-compliant immediately. 

Compliance policies essentially define what a 'healthy' device looks like within the organisation

![Compliance policy](images/06-create-policy.png)

### 7. Tested the Policy
I synced the device to from inside Intune to apply our new policy. 

![Sync](images/07-sync.png)

The individual device's compliance page then listed our policy (`Windows Compliance`) along with a default one. It also listed the `State` of the device as `Compliant` as all conditions we set were met.

![Compliant](images/08-device-compliance.png)

### 8. Forced Non-compliance
Updated the policy to also require a minimum OS version, i set this to `11.0.00000.0000`, something above our current version so that it would trigger.

![Minimum OS](images/09-update-policy.png)

After syncing the device again the device was stated as `Not Compliant` and the minimum OS version was listed as the reason why. Showing that the policy had worked.

![Minimum OS Noncompliant](images/10-not-compliant.png)

### 9. Created Configuration Profile
Created a Settings Catalog Profile that would prevent the user of the device from accessing the CMD.

Whereas Compliance Policies check the state of the device to see if it is compliant or not. Configuration Profiles actually make changes to the device and can restrict or allow certain things.

![Config profile](images/11-config-policy.png)

### 10. Verified Configuration Profile
On the Windows 11 VM attempted opening the CMD to see if the profile applied. The cmd showed a message saying it was `disabled by the administrator`

![CMD denied](images/12-cmd-denied.png)

I also checked it was successful in Intune via the Policy settings report of the individual policy

![Check intune](images/12-denied-intune.png)

### 11. Retired the Device
Offboarded the Windows 11 device by disabling it in Entra ID first

![Entra disable](images/13-entra-disable.png)

Then deleted the device from Intune

![Delete intune](images/14-intune-delete.png)

Then confirmed it was not listed in Intune and therefore not managed by it

![Verify](images/15-intune-no-devices.png)

## Notes
- Usually would select `Retire` when offboarding a device however a pop up stated that Entra joined windows devices can not be retired 
- when syncing devices with new policies it can take a while to update and display as non-compliant (10-15 minutes)

## Outcome
Successfully gained hands-on experience with Intune device management. Connected a Windows 11 VM to the domain and managed it through Intune, applying a compliance policy that required a certain minimum OS version, and applying configuration settings that restricted users on the device from accessing the command prompt.

# Active Directory
## Objective
The purpose of this page is to showcase my skills in Active Directory. I will demonstrate various features, including setting up users, groups, and group policies, among other things. All the examples here will assume a company that has an AD environment setup (unless otherwise stated). 

<!-- As I learn new features, I will update this page to reflect on what I have learned. -->

## Table of Contents
<!-- - Installing Active Directory -->
- [Active Directory Users and Computers](https://github.com/HolyYewfelle/Active-Directory-Project/blob/main/Active%20Directory.md#active-directory-users-and-computers)
    - The toolbar 
- [OUs](https://github.com/HolyYewfelle/Active-Directory-Project/blob/main/Active%20Directory.md#ous)
    - What are they?
    - Common use cases
- [Users](https://github.com/HolyYewfelle/Active-Directory-Project/blob/main/Active%20Directory.md#users)
    - Creating, deleting, and disabling a user
    - Deleting vs. disabling
    - User permissions
- Groups
    - Creating a group
    - Adding members to a group
    - Setting group permissions
- Basic Scenarios + Tasks
    - "Hello? I forgot my password"
    - Temporary employees and vacation leaves
    - Promotion
    - Changing departments
- Advanced Scenarios + Tasks
    - "Our client wants to have an AD environment set up"
        - Set up a DC
        - Create any groups/users
        - Create a GPO
        - Create file shares

<!-- ## Installing Active Directory -->
## Active Directory Users and Computers
<!-- Mention toolbar location for future easy reference. -->
To access Active Directory, ensure that the 'Active Directory Domain Services' add-on is installed. This can be done in Server Manager under 'Manage' > 'Add Roles and Features.' You will then have the option to either connect to an existing domain or create a new one. I promoted my server to a domain controller and created a new domain (kotone.local). Once the setup is successful, you will have access to 'Active Directory Users and Computers,' located under the 'Tools' tab. This is where you can manage various aspects of the domain. For simplicity, I will refer to it as AD UC from now on.

![ADUC Window](https://github.com/user-attachments/assets/70a138c8-7afd-48e6-859c-b8f9f7c9e782)

### The toolbar
One thing I want to mention is the toolbar at the top of the screen. I will briefly go over the different icons, as they help you conveniently and efficiently complete tasks. From left to right:

![ADUC Toolbar](https://github.com/user-attachments/assets/ea5f9dab-9f50-48f8-9155-821cec29e121)

*Note: Not all are actual names of the options; I have simplified some names to keep them relevant to their tasks.*

1. Back – Navigates to the previous page visited.
2. Forward – Navigates to the next page visited (when applicable).
3. Up One Level – Moves up one level within the directory hierarchy.
4. Show/Hide Console Tree – Toggles the visibility of the left pane.
5. Cut – Copies the selected object to the clipboard and removes the original (only visible when an object is selected).
6. Paste – Pastes the object saved to the clipboard.
7. Delete – Deletes the selected object (only visible when an object is selected).
8. Properties – Displays the properties of the selected object.
9. Refresh – Refreshes the list of objects.
10. Export List – Exports the list of objects and basic information to a file.
11. Help – Opens the official Microsoft ADUC help guide.
12. Show/Hide Action Pane – Toggles the visibility of the right pane.
13. New User – Creates a new user within the selected OU.
14. New Group – Creates a new group within the selected OU.
15. New OU – Creates a new Organizational Unit (OU).
16. Filters – Narrows down the object list using filters.
17. Search – Uses the search function to quickly find objects.
18. Add to a Group – Adds the selected object (typically a user) to a specified group.


## OUs
### What are they?
OUs stand for Organizational Units, and as the name implies, they help organize the structure of the domain environment. A good way to think of OUs is like folders within a file directory system. You can add objects to an OU or create OUs within another, just as you would with files and folders. In fact, the icons for OUs are folders, which emphasizes their similarities. To add OUs, simply click 'New OU' from the toolbar within the desired location. In my case, I created four OUs named HR, IT, Marketing, and Sales. As you can see, you can also create OUs within an OU; for example, I created 'Managers' within the 'IT' OU.

![OUs](https://github.com/user-attachments/assets/e1d17991-be21-4633-9927-bc5cc6e9ebff)

### Common use cases
OUs primarily serve an organizational purpose. For example, instead of having every user in an enterprise listed under the 'Users' OU it is more feasible to create new OUs to sort the users, such as by departments (HR, Sales, etc.). There is also an option to have an OU's control delegated onto another user. Let's say that we want an administrator to only handle changes within the HR department. The OU created for users of the HR department could have it's control delegated onto that administrator, creating a separation of duties (no one user has the power to change everything).

## Users
Users are one of the biggest, if not the biggest, components of Active Directory. For example, onboarding and offboarding employees is a relatively common task. Another important aspect is that user accounts are not limited to humans; services can also have their own accounts. Let's dive into it.

### Creating, deleting, and disabling a user
**Scenario:** A new employee, Jim Lee, joins the company. Jim is a member of the sales department and will need an account to access anything, so let's create one for him.

First, select the Organizational Unit (OU) where Jim’s user account will reside; in my case, it is 'Sales.' Next, in the toolbar, select the option to add a new user. Enter the user’s first and last name, and assign a logon name. A note on the logon name: Many companies have a standardized convention for creating logon names; a common one is the 'first initial + last name' format. In this case, I'll enter 'Jim' as the first name, 'Lee' as the last name, and assign him the logon name 'jlee.'

![Creating Jim Lee's account](https://github.com/user-attachments/assets/603ae22b-b344-446e-a533-13f350ea1e12)


On the next page, set a password for Jim. Many companies have specific rules for creating passwords, but for now, I'll give Jim a password that meets minimum security standards (at least 8 characters with a mix of lowercase, uppercase, numbers, and symbols). Make sure to select the option "User must change password at next logon," as we want Jim to have a password only he knows.

![Setting up a password](https://github.com/user-attachments/assets/c52f4c7c-97b8-4605-a4be-8bbb0151be39)


The following page will allow you to review all the information. If everything looks correct, finish creating the account. Now, Jim has an account that he can use to log in to our domain environment.

![Reviewing user information](https://github.com/user-attachments/assets/34ed7efb-c32b-4a1f-a7a2-b4338dbd80cb) 

Using these steps, I have made new user accounts for the various departamental OUs that I have created. You will see some of them mentioned as I go on.

---
**Scenario:** Kara Sanders has recently left the company. She will no longer be working with us, so we need to ensure her account cannot be used to log in. Kara worked in the Human Resources department.

To find Kara Sanders' account, you can either manually navigate to the Organizational Unit (OU) where she is located or use the search function from the toolbar. You can search within a specific OU, the domain, or the entire directory.

![Utilizing the search function](https://github.com/user-attachments/assets/2c4257c7-7a20-41b4-990b-57fb0c34318b)

Once you have located the account, right-click on it and select the 'Delete' option. A warning dialogue will prompt you to confirm the deletion. After confirming that it is indeed Kara Sanders' account, accept the deletion. You will notice that her account is no longer visible.

Alternatively, you can disable the account. The steps are the same as deleting the account, but instead of choosing 'Delete,' select 'Disable Account.' Disabling the account keeps it stored in the system, which is the main difference between disabling and deleting. To enable the account again, follow the same steps, and you will notice that the option now reads 'Enable Account.'

![Deleting or Disabling](https://github.com/user-attachments/assets/392f8632-284d-494f-9d12-edad29fc23f3)


### Deleting vs. disabling
Why disable an account when we will delete it later anyway? When might enabling a previously disabled user account be useful?

Deleting an account is an irreversible action, and that alone should be a major consideration. Chances are your company has a policy regarding the deletion of user accounts, so always follow company policy first. Personally, I recommend disabling accounts first and only deleting them afterward if they are deemed unnecessary.

There are a few common use cases for disabling an account. The first, as mentioned earlier, may simply be company policy. Another example is disabling user accounts while their respective owners are on vacation. We shouldn’t delete those users, as they still work for the company but are temporarily away. A third, less common example could occur when an employee is under investigation and the company needs to keep their account stored but deactivated. The account might have access to important evidence, so it’s critical not to delete it.

<!-- ### User Permissions

## Groups

### Creating a Group

### Adding Members to a Group

### Setting Group Permissions

## Basic Scenarios + Tasks

## Advanced Scenarios + Task -->

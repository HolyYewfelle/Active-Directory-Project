# Active Directory
## Objective
The purpose of this page is to showcase my skills in Active Directory. I will demonstrate various features, including setting up users, groups, and group policies, among other things. All the examples here will assume a company that has an AD environment setup (unless otherwise stated). 

<!-- As I learn new features, I will update this page to reflect on what I have learned. -->

## Table of Contents
<!-- - Installing Active Directory -->
- Active Directory Users and Computers
- OUs
    - What are they?
    - Common use cases
- [Users](https://github.com/HolyYewfelle/Active-Directory-Project/edit/main/Active%20Directory.md#users)
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
<!-- ## Active Directory Users and Computers
Mention toolbar location for future easy reference.

## OUs

### OU Sub 1

### OU Sub 2 -->

## Users
Users are one of the biggest, if not the biggest, components of Active Directory. For example, onboarding and offboarding employees is a relatively common task. Another important aspect is that user accounts are not limited to humans; services can also have their own accounts. Let's dive into it.

### Creating/Deleting/Disabling a User
**Scenario:** A new employee, Jim Lee, joins the company. Jim will need an account to access anything, so let's create one for him.

First, select the Organizational Unit (OU) where Jim’s user account will reside. Next, in the toolbar, select the option to add a new user. Enter the user’s first and last name, and assign a logon name. A note on the logon name: Many companies have a standardized convention for creating logon names; a common one is the 'first initial + last name' format. In this case, I'll enter 'Jim' as the first name, 'Lee' as the last name, and assign him the logon name 'jlee.'

On the next page, set a password for Jim. Many companies have specific rules for creating passwords, but for now, I'll give Jim a password that meets minimum security standards (at least 8 characters with a mix of lowercase, uppercase, numbers, and symbols). Make sure to select the option "User must change password at next logon," as we want Jim to have a password only he knows.

The following page will allow you to review all the information. If everything looks correct, finish creating the account. Now, Jim has an account that he can use to log in to our domain environment.

---
**Scenario:** Kara Sanders has recently left the company. She will no longer be working with us, so we need to ensure her account cannot be used to log in.

To find Kara Sanders' account, you can either manually navigate to the Organizational Unit (OU) where she was placed, or use the search function located in the toolbar. <!-- input search tool instructions --> Once you have located the account, right-click on it and select the 'Delete' option. A warning dialogue will prompt you to confirm the deletion. After confirming that it is indeed Kara Sanders' account, accept the deletion. You will notice that her account is no longer visible.

Alternatively, you can disable the account. The steps are the same as deleting the account, but instead of choosing 'Delete,' select 'Disable Account.' Disabling the account keeps it stored in the system, which is the main difference between disabling and deleting. To enable the account again, follow the same steps, and you will notice that the option now reads 'Enable Account.'

### Deleting vs Disabling
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

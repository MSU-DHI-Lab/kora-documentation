---
title: Managing Users in a Kora Installation
---
# Managing Users in a Kora installation

Kora makes it easy for administrators to manage who is part of a Kora installation. This includes the ability to invite, edit and view users. Follow these steps to get to the *User Management* page.

1. Management of users can start from anywhere in kora by going to the main navigation menu at the top right of the page.  <p align="center"> <img src="../user-accounts-img/managing_users_in_a_kora_installation_1_annotated.png" width="100%" style="align:center" title="Step 1"> </p>

2. Select the **Management** option at the bottom of the page. <img style="display:block;margin:auto;max-width:100%" src="../user-accounts-img/managing_users_in_a_kora_installation_2_annotated.png" title="Step 2">

3. After opening up the **Management** sub-menu, select **User Management** to bring you to the page for user management. <img style="display:block;margin:auto;max-width:100%" src="../user-accounts-img/managing_users_in_a_kora_installation_3_annotated.png" title="Step 3">

4. You may search for users by using the **Find a User** search bar. <p align="center"> <img src="../user-accounts-img/managing_users_in_a_kora_installation_4_annotated.png" width="100%" style="align:center" title="Step 4"> </p>

5. You may also organize your users alphabetically or by the date they joined your Kora installation. <p align="center"> <img src="../user-accounts-img/managing_users_in_a_kora_installation_5_annotated.png" width="100%" style="align:center" title="Step 5"> </p>

## Inviting New Users to a Kora installation

Any number of new users can be added to the Kora installation. All that is required for new users is a valid email address to [sign up for a new user account](signing_up_for_a_user_account.md). Follow the steps below from the *User Management* page to add a new user to your Kora Installation:

1. Select the **Invite New User(s)** button at the top of the page. <p align="center"> <img src="../user-accounts-img/managing_users_in_a_kora_installation_6_annotated.png" width="100%" style="align:center" title="Step 6"> </p>

2. An *Invite User(s)* pop-up will appear. Enter any number of emails for your users into the **Enter Email(s) to Invite User(s)** field. Emails must be separated by either a space or a comma. <p align="center"> <img src="../user-accounts-img/managing_users_in_a_kora_installation_7_annotated.png" width="100%" style="align:center" title="Step 7"> </p>

3. You have the option to include a personal message with your invite. <p align="center"> <img src="../user-accounts-img/managing_users_in_a_kora_installation_8_annotated.png" width="100%" style="align:center" title="Step 8"> </p>

4. Click **Invite User(s)** at the bottom of the pop-up. <p align="center"> <img src="../user-accounts-img/managing_users_in_a_kora_installation_9_annotated.png" width="100%" style="align:center" title="Step 9"> </p>

New users will receive an email invitation to join Kora. For directions on how to sign up for a new user account, check out the [new user account](signing_up_for_a_user_account.md) documentation.

## Managing Permissions

You may give a user administrative access by checking the box next to **Admin**. Administrators are able to grant or remove admin access to other users within your Kora installation. Admins will have the ability to manage users, create projects, manage API tokens, and perform other high level actions. Care should be taken with who is given administrative action since they will have a lot of power to change the organization of data within a Kora installation. <p align="center"> <img src="../user-accounts-img/managing_users_in_a_kora_installation_10_annotated.png" width="100%" style="align:center" title="Step 10"> </p>

You are also able to mark users as active or inactive. Active users will be able to login and work on your Kora installation, while inactive users will no longer be able to sign into their Kora accounts. <p align="center"> <img src="../user-accounts-img/managing_users_in_a_kora_installation_11_annotated.png" width="100%" style="align:center" title="Step 11"> </p>


## Viewing User Profiles

Administrators are able to view the profiles of any user within a Kora installation by selecting **View User Profile**. Administrators are able to [view the same account information that users can view of themselves](viewing_your_user_account.md). This includes their profile information, permissions and record history. <p align="center"> <img src="../user-accounts-img/managing_users_in_a_kora_installation_12_annotated.png" width="100%" style="align:center" title="Step 12"> </p>

## Editing User Profiles

As an administrator, you have the ability to update any user's profile information by selecting **Edit User Profile** for a user. This allows you to [edit the same profile information as a user editing their own account](edit_user_account.md). This includes their name, username, email, profile image, organization, language, and password. <p align="center"> <img src="../user-accounts-img/managing_users_in_a_kora_installation_13_annotated.png" width="100%" style="align:center" title="Step 13"> </p>

## Manual User Confirmations/Activations and Password Resets

For installations of Kora without working email servers, it will be necessary to manually activate any new accounts, whether they were created by a user themselves, or via an invitation by an administrator. To activate a user account that has been created but not yet confirmed, simply check the **Active** box for that user. For invited accounts, notify the user of their new username.

If the user account was created via invitation, or if a user requires a password reset, you will additionally need to set a temporary password and then manually notify the user of it. To temporarily set a password, select **Edit User Profile** for the desired account, type in the temporary password, retype it to confirm, and hit **Update User Profile**. When relaying this temporary password to the owner of the account, warn them that their password is not safe and they should change it themselves immediately after logging in. They can do so by following the instructions in the article "[Edit User Account](edit_user_account.md#update-password)"

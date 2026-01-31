---
title: Understanding Kora User Types and Permissions
---
# Understanding Kora User Types and Permissions
Understanding Kora's user types and associated permissions is critical for managing a Kora installation or project (or for understanding what you, as a user, have permission to do within a Kora installation). Kora takes a somewhat unique approach to user types and permissions. Instead of having a variety of user types, each with their own fixed array of permissions, Kora (mostly) uses a group model. Basically, a permission group in Kora is a bucket to which a Kora admin assigns permissions (called group permissions). Any user can be placed in a permission group, thereby inheriting the permissions of the group. The point of this model is to provide maximum flexibility for user management. A Kora admin could create a permission group that only allows users to *view* records, while another permission group could allow users to *view and edit* records.

There are two types of permission groups: **Project Groups** and **Form Groups**. Each group type has slightly different options (more on that below), since what can be done in a Kora project is different from what can be done in a Kora form.

Beyond permission groups, there are three fixed user types: **Kora Admin**, **Project Admin**, and **Form Admin**.

### Kora Admin
A Kora admin sits on top of the user pyramid. They have access to all projects in a Kora install, and have unique management privileges such as: creating, editing, and deleting projects; importing and exporting projects; configuring a Kora install; managing all users in a Kora install; and managing Kora tokens and API requests. In addition, they have all of the privileges of all other user types and permission groups. Essentially, a Kora admin can do anything in a Kora install. While all new Kora installs require at least one admin, you (as an admin) can create any number of other admin accounts.

### Project Admin

Similar to the Kora Admin, the **Project Admin** sits at the top of the user pyramid *within a project*. While they can't create new projects, they pretty much can do anything within the project for which they are an admin. This includes creating forms, editing forms, deleting forms, creating field value presets, importing and exporting forms, and managing user permissions. They also have the permissions of all of the user and permission groups below them.

### Form Admin

Similar to Kora Admins and Project Admins, a **Form Admin** is a top-level user *within a form*. While they can't create new forms, they have pretty much all other permissions within the form for which they are an admin. This includes managing form permissions, managing associator permissions (by managing which forms are allowed to associate to others), importing and exporting records, deleting records, deleting all records, deleting old record files (including deleting files that belong to a record which no longer exists), managing record presets, managing revisions, creating and editing fields, creating and editing records, deleting records, and modifying form layouts.

### Project Groups

As its name suggests, a **Project Group** exists on the project level, and controls permissions of that group of users within a single project. Project groups have three options that can be turned on or off: Create Forms, Edit Forms, and Delete Forms.

By default, when a new project is created in Kora, there are two permission groups: **Admin Group** and **Default Group**. The Admin Group has all three options mentioned above enabled; the Default Group, on the other hand, has all three disabled. Project Admins (or Kora Admins) can enable or disable any of the options for the two default permission groups, or create any number of new groups as needed.

Need to learn how to add/remove users within a project? Visit the "[Adding Users to Projects](../projects/adding_users_to_projects.md)" guide.

### Form Groups

As its name suggests, a **Form Group** exists on the form level. It controls the permissions of that group of users within a single form. Form Groups have 6 options that can be enabled or disabled: Create Field, Edit Field, Delete Field, Create Record, Edit Record, and Delete Record.

When a new form is created, two default permission groups are created: Admin Group and Default Group. The Admin Group has all of the aforementioned options enabled, while the Default Group has all of them disabled. A Form Admin (or a Project Admin or Kora Admin, for that matter) can modify these as they see fit, or create any number of new Form Groups as needed.

Need to learn how to add/remove users in specific forms within a project? Visit the "[Adding Users to Forms](../forms/adding_users_to_forms.md)" guide.

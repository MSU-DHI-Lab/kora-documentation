---
title: Installing Kora on Domain of One's Own and Reclaim Hosting
---

# Installing Kora on Domain of One's Own and Reclaim Hosting

This is a basic guide for installing Kora in a [Reclaim Hosting](https://reclaimhosting.com)-based server environment, which includes any Domain of One's Own services offered by institutions. A few things about this guide. First, in many cases of naming something or writing Terminal commands, things will be case sensitive, so unless the specific instance requires uppercase for something, this guide will always use lowercase and its author strongly suggests you do the same. Keeping things all lowercase is a good thing to follow for best practices because it removes any doubt or confusion over whether some file, directory, or URL should have uppercase letters in it.

Second, a note about terminology. To keep things consistent, this guide will be using the word "directory" and its derivatives throughout this guide, rather than "folder" in order to better illuminate the link between URL and file structure throughout this process.

Finally, make sure to visit the [Kora GitHub repo](https://github.com/matrix-msu/kora) to download a zip file containing the most recent Kora iteration of the repo. To do this, visit that page and click on the "Code" button. In the menu that appears, the default tab ("Local") will have a "Download ZIP" option to click on. Save the downloaded ZIP

## Log In to cPanel

Begin all of this by logging into your account to reach your cPanel. Most cPanels look something like this:

<img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_1_annotated.png" title="cPanel Main View">

## Set up MySQL Database

1. After reaching the cPanel for your server environment, begin by setting up the necessary MySQL Database for your Kora installation. Start by finding the section called "Databases" and clicking on "MySQL Databases".

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_2_annotated.png" title="cPanel's MySQL Databases">

1. Under "Create new Database," enter "kora" or some other name in the text field and click "Create Database."

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_3_annotated.png" title="New MySQL Database">

1. Take note of the auto-generated prefix, which, when combined with whatever you just provided, will be the name of your MySQL database. In this example case it is called `geyerbri_kora`. Once you've noted this database name, click on the link to take you back to the previous page.

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_4_annotated.png" title="New MySQL Database">

1. Next, scroll down to "MySQL Users" and provide the username "kora" in the text box under "Add New User". This is a common practice — the database and the default user for that database having the same name — which will make it easier to update configurations elsewhere. After this, click on the button "Password Generator."

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_5_annotated.png" title="Database New User">

1. The Password Generator modal will open and generate a random string of characters (blocked out in the image below).

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_6_annotated.png" title="Database User Password Generator">

    <br>

    !!! tip "IMPORTANT"
        Copy this password to somewhere for safe-keeping. You will need it later for configuration of your Kora installation.

    After copying this password to somewhere, click "Use Password."

1. When the modal closes, the generated password will auto-fill into the "Add New User" section and it should rate the password as "Very Strong." Click on "Create User" to complete this process.

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_7_annotated.png" title="Completing New User">

    Just as you did with the database name, take note of this username, as you will need it for Kora configuration elsewhere. Because this guide follows the common practice of using the same name for the database and user, this example username is also `geyerbri_kora`.

    Click the back link to get back to the previous page.

1. The final step in setting up the required MySQL database is to assign the newly-created user to the newly-created database and give that user full permissions. Do this by first scrolling down to "Add User To Database", confirming that the names are correctly chosen, and clicking on "Add."

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_8_annotated.png" title="Add User to Database">

1. The page that opens will provide a list of permissions that can be assigned to the chosen user for the specified database. Click the checkbox for "ALL PRIVILEGES."

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_9_annotated.png" title="Provide All Permissions">

    Scroll down if needed to find the "Make Changes" box. Clicking on it will generate an in-page notification that it was successful. Click on the "Go Back" link to get back to the main "MySQL Databases" page.

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_10_annotated.png" title="Confirm Permissions and Return">

1. To confirm that you have successfully created the database, created the user, and added the user to the database, find the section "Current Databases" and check that there is an entry for your new database, with your new user listed as a privileged user.

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_11_annotated.png" title="Confirm Database and Privileged User">

## Return to cPanel Main

To return from nearly any part of cPanel to the Main interface (shown in the screenshot at the beginning of this guide), you can click on the grid icon in the upper-left.

<img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_12_annotated.png" title="Return to cPanel Main">

## Upload and Prepare Kora Application Files via cPanel File Manager

1. From cPanel Main, find the section "Files" and click on "File Manager."

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_13_annotated.png" title="cPanel's File Manager">

1. Take a note of which directory is your main URL directory (the one that provides all the files available via your main URL). In this screenshot you can see the globe icon being used for the URL directory "public_html", which is the common icon in this version of cPanel and used in MSU's Domain of One's Own. You may use this directory later, to confirm something in Step 3 of "Subdirectory URL Setup Via cPanel Terminal", if following that path for creating your Kora installation URL (this will make sense later).

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_14.1_annotated.png" title="URL Directory">

    You will also notice the same globe icon, but with a black chain-link icon over it, used for "www".

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_14.2_annotated.png" title="'Linked' Directory">

    This is something different, which will be explained in one of the sections about setting up the installation URL below. But for now just know that the directory with the globe and without the chain-link is the one you need to make note of.

1. In order to properly view all the relevant Kora installation files once they have been created, it is important for you to make all the hidden files visible. To do this, go to the File Manager's "Settings" by clicking on the gear icon in the upper-right.

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_24.2_annotated.png" title="Open File Manager Settings">

    Click the checkbox for "Show Hidden Files (dotfiles)" and then click "Save".

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_15_annotated.png" title="Enable Viewing Hidden Files">

1. Next, you'll upload the Kora installation .zip file you downloaded earlier from [Kora's GitHub repo](https://github.com/matrix-msu/kora) page. Kora is intended to be installed *outside* of the main URL directory you noted in Step 2 of this section, to keep it secure and reduce any chances of interference with any other website content you have in your server environment; the easiest is to install it into the same directory alongside your main URL directory. If you have never changed the default directory that loads when opening File Manager, you should be viewing the correct location, which in this example case is named after the user ("geyerbri").

    !!! note
        In the screenshots below, you may notice that the .zip file, and the initial kora directory, has a different name. Though these screenshots are from an old guide with different file names, the process is exactly the same.

    While at this location, click on "Upload" in the menu at the top.

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_16.1_annotated.png" title="Upload Files">

    In the page that opens, just drag-and-drop the .zip file to upload it. You may also click on "Select File" to find it via your computer's file management windows.

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_50_annotated.png" title="Upload a File">

    When the .zip file finishes uploading, click on the link leading back to File Manager.

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_17_annotated.png" title="Back to File Manager">

1. Locate the uploaded .zip file in this directory, right-click it to bring up the context menu, and select "Extract."

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_18_annotated.png" title="Selecting Extract in the Context Menu">

    In the Extract modal that opens, leave the default location alone (the text box is likely blank) and click "Extract File(s)."

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_19_annotated.png" title="Extract Files">

    In the follow-up modal called "Extraction Results," click "Close."

1. Extracting the .zip file will create a new directory, which is likely called "kora-master". Locate this directory, right-click on it, and select "Rename."

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_20.1_annotated.png" title="Selecting Rename in the Context Menu">

    In the Rename modal that opens, change the text in the box to "kora" (without quotations) and click "Rename File."

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_21_annotated.png" title="Rename Directory">

1. Next, it's time to initially set up the .env file that manages some of the configuration settings for your Kora install. Many of the settings in this file will be adjustable once the installation is complete, but a few are not and require configuration now.

    Enter/access your renamed "kora" directory by double clicking on it, then right-click on the ".env.example" file and select "Copy."

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_22_annotated.png" title="Selecting Copy in the Context Menu">
    In the Copy modal that opens, add "/.env" without quotations to whatever is already in the text box and click "Copy File(s)."

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_23_annotated.png" title="Create file copy with '.env' name">

1. Once the file has been renamed, select it and then click on "Edit" in the menu at the top.

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_24.1_annotated.png" title="Open File Editor">

    The Edit modal that opens provides a warning to back up the file you are about to edit before making any changes. This is always a good practice to follow, so that any mistakes can be quickly and easily rectified. Luckily, since the file you are about to edit is a direct copy of ".env.example," you already *have* a backed-up copy of its current state, so in this case making an additional backup is not necessary. So go ahead and click on "Edit."

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_25_annotated.png" title="Confirm opening File Editor">

    A new tab will open with the editor. Here, change lines 6, 7, and 8 to match the info you saved about your MySQL database. For example, given the info previously saved from the database setup before, this guide's example code would look like:

        DB_DATABASE=geyerbri_kora
        DB_USERNAME=geyerbri_kora
        DB_PASSWORD={saved database user password}

    Notice, this is where you will paste in the database password you saved in Step 5 of "[Set Up MySQL Database](#set-up-mysql-database)" above. Remove the curl brackets from the example code and make sure there are no spaces before or after the password.

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_26_annotated.png" title="Editing .env File">

    After finishing this, click "Save Changes". Once that's done you can either close the tab or click "Close" (which does the same thing) and go back to the File Manager tab.

1. Finally, there is one more example file to copy as a configuration file. Enter the directory "public" and also copy the file ".htaccess.example". Add "/.htaccess" after the defaulted location, the same way you did for ".env" in the previous step. The default settings in this file will work for basic installations of Kora, but should you want to adjust settings such as more complex URLs than what this guide presents (see "[Create Kora Installation URLs](#create-kora-installation-urls)" below), or to change the advanced settings such as acceptable file sizes, memory limits, timeout lengths, etc., they are controlled in this file.

    Once copied, follow the same steps to edit this file.

    Add a new first line in this file, with the following:

        Require all granted

    Just as before, click "Save Changes" to complete the editing process.

    You're finished with the initial file setup. Navigate back to cPanel Main.

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_16.2_annotated.png" title="Return to cPanel Main from File Manager">

## Kora Installation and Initial Configuration via cPanel Terminal

1. In cPanel Main, scroll down to the section called "Advanced" and open "Terminal."

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_27_annotated.png" title="cPanel's Terminal">

    Read and (hopefully) accept the terms to reach the in-cPanel Terminal interface. It will look like this:

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_28_annotated.png" title="Terminal Window">

1. In Terminal, you will be using some basic commands to move around and change a few things. The first one is `cd`, which just changes your location in the file system. Change your directory to whichever directory you just renamed the extracted zip file to. If you've been using the suggested names above, this will be "kora":

        cd kora

    For installation, Kora relies on a dependency management tool called [Composer](https://getcomposer.org) to locate and add a number of additional files required for Kora to work correctly. Reclaim Hosting environments include Composer already, but it is important that the installation use the most recent version, for stability.

    To ensure your server is up to date, run the following:

        composer update

    !!! note
        For current (January 2024) Reclaim Hosting servers, the default server-wide PHP version is 8.0, which is not sufficient to properly install and run Kora. Please follow [this guide for a temporary workaround](XXXXXXXX) for this limitation. The guide begins with an explanation of how to check your current default server-wide PHP version.

    Next, run the Kora installation process:

        php artisan kora:install

    After running, if it is successful, the window will look like this, with the successful installation message (in green):

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_30_annotated.png" title="Successful Installation Message">

    !!! note
        If the installation fails and provides a message that says (in part) "Failed to connect to database! Check your database credentials or review the logs for more error information," this may be due to some common problems and there are a few things to check before trying to run the installation command again. First, return to the MySQL section of cPanel to confirm you have written down the full database name and username correctly. Second, re-open the .env file where you earlier put that database information, to double-check that these names are correct. If they are, there may be an issue with the generated password for your MySQL user. You can go generate a new password, save it again, and enter it into the .env file, before once again trying to run the installation command. If the installation again fails, the issue may be something else. You can check for any similar issues and potential solutions in [Kora's GitHub Issues](https://github.com/matrix-msu/kora/issues), or open your own Issue with a detailed description of the problem.

1. **INCREDIBLY IMPORTANT**: You *must* copy the last line generated here in the successful installation message (outlined above), which has your password for the generated username of "admin". To copy things in cPanel's Terminal, first use your mouse to select the line, then right-click and select "Copy." Paste this somewhere safe, where you will not lose it!

    !!! warning
        It cannot be stressed enough how important this step is, because losing this password means losing access to your installation and will require a full reinstallation.

1. Notice that, in the successful installation message, you are directed to "give READ access to the web user," as well as "WRITE access" for specific directories, to ensure that Kora continues functioning properly after users start contributing. What these directions require could be different for different Domain of One's Own environments, because different system administrators may have set up the default permissions for the environment differently. For now, to ensure that things are set up for the most likely scenario for most Domain of One's Own or Reclaim Hosting environments, you will be setting file permissions for the entire "kora" directory and its contents.

    Because these commands have to be applied to all the files and directories within, you will have to do this here, via Terminal, using the `chmod` command and the `-R` flag.

    `chmod` stands for "change mode," which is how the server's operating system refers to changing permissions. The `-R` flag tells the command to run recursively, i.e. change them for this directory and everything it contains. Finally, the `.` is the short-hand for "my current location."

    This first command is to make sure that any new files and directories created in Kora are assigned the correct permissions in the future. It may not be needed for most cases, but in the few cases where it is, it will be useful. So run the following code:

        chmod -R g+s .

    When successful, Terminal will just re-display the command prompt without a message:

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_31_annotated.png" title="Successful g+s Command">

1. Next, it is important to confirm that the directories and files in this installation are all set to the `755` permissions level. In the operating system your server is running, this number represents the permissions levels for three different attributes related to a file or directory's ownership in the system. The first number represents the level set for "Owner," the second for "Group," and the third for "Other/World." Setting `7` is full access — aka read, write, and execute — whereas setting `5` is read and execute access only. For the purposes of this basic installation, the level for "Owner" should always be set to `7` so that you will always be able to make changes to things if needed. However the amount of access given to "Group" and "Other/World" attributes will affect the security of your server environment, so it is important to set these to `5` or some other non-write setting whenever possible.

    So, to confirm that the installation's permissions are set at the appropriate levels for the appropriate attributes, run this command to set all of this directory and its contents to "READ" (and execute, which is missing from the successful installation message). Again, in many cases it isn't strictly needed, but in the few where it is this will ensure the settings are set correctly (do not forget the period):

        chmod -R 755 .

    And just as before, when successful, it will just re-display the command prompt without a message.

1. Next it is important to check if your "Write" permissions are set properly. Run the `ls` command with the `-l` flag. `ls` is the list command; the `-l` flag is for listing contents in long-form. The full command is:

        ls -l

    The resulting list will look like this:

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_51_annotated.png" title="Long-form Directory List">

    In the long-form list, Terminal will display two account names: first the username of "Owner," then (the one highlighted in the image above) the username of "Group." In the example here, both are set to the same username, which means the "Owner" permissions level is applied to "Group" as well. In this such case — where the "Owner" and "Group" have the same username — no further permissions changes need to be made to ensure Kora is working properly and you may skip down to "[Create Kora Installation URLs](#create-kora-installation-urls)."  

    However, if these two are different, then you will need to additionally adjust the "Write" permissions for "Group," so please continue to the next section.

    If you intend to set the "Write" permissions because you are sure your specific server environment's defaults will prevent Kora from working properly, then you can prepare for the commands in the next section

## Set "Write" and "Execute" Permissions On Certain Directories if Needed via cPanel Terminal

As stated in the previous section, the previous commands will have been enough for some users to complete the required permissions setup for their installation. However for others, it will be necessary to specifically change the permissions on the three directory trees noted in the successful installation message.

If you are unsure of whether or not your file permissions are properly configured, you can quickly test this by completing the rest of the Kora setup process, then creating a record in your Kora installation that has a file attached to it and uploading that file. If the file upload process works, then your current installation does not need any further permissions adjustments. If it does not work, you will need to re-enter cPanel and re-enter Terminal, which should default to the correct location (the root directory) for this section's instructions.

You will need to wait until your Kora installation is completed and properly configured before you can conduct this test, so its instructions are provided in the final section of this page, "[Testing the Installation](#testing-the-installation)."

To set the "Write" and "Execute" permissions for the relevant directories:

1. Begin by ensuring your current Terminal location is the root directory, represented by a "~" in the Terminal prompt to the left of the cursor. If your prompt does not have a "~" — it may instead still display "kora" — change your location relocate to the root. As before, use `cd`, but this time use `~`, which will go straight to the root location:

        cd ~

    When located correctly, your terminal prompt will look similar to the outlined line in this screenshot:

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_32_annotated.png" title="Moving Up One Directory">


1. Run the following three commands, using the exact locations described in the successful installation message (reproduced here in case you are coming back to Terminal after learning that your installation requires these settings to work). These will set the "Write" (and "Execute") permissions for "Group" correctly. Hit "Enter" after each command (i.e. run each on its own).

        chmod -R 775 kora/bootstrap/cache/
    <span></span>

        chmod -R 775 kora/storage/
    <span></span>

        chmod -R 775 kora/public/assets/javascripts/production/

    Just as before, when successful, each of these will just re-display the command prompt without a message. After you've run all three, your Terminal will look something like this:

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_33_annotated.png" title="Setting Write/Execute for 'Group' and 'Others'">

## Create Kora Installation URLs

Next, it is important to have your Kora installation accessible via a web browser and URL. There are two options for doing this: a **subdomain** or a **subdirectory**. A subdirectory URL looks like: https://example.org/subdirectory, whereas a subdomain looks like: https://subdomain.example.org. You only need to choose **one** of these two options for you to do.

Find the directions for each below.

### Subdirectory URL Setup Via cPanel Terminal

1. To set up a subdirectory URL for your Kora installation, you will just have to do a couple more things in Terminal. First you will change your location to be inside of the directory that your main URL is accessible from: in this example case in MSU's Domain of One's Own environment, this is a directory called `public_html`. But another common name for it is `www`. Use the following, with whatever name pertains to your version:

        cd public_html

    !!! note
        If you receive an error that "public_html" (or "www") does not exist, more than likely this is because you skipped over a few previous steps that did not pertain to you and so you are currently still inside of the "kora" directory. If this is the case, use `cd ..` to move your terminal prompt upward one directory, and then again try `cd public_html`.

    (There is no screenshot for this specifically, but you will know you have successfully changed your directory to `public_html` — or the one relevant to your case — when you see it written to the left of the dollar sign character, inside the brackets.)

1. Setting up the subdirectory for your URL requires using the command `ln` with the `-s` flag. `ln` stands for "link" and the `-s` flag tells the system that the link being created is "symbolic". The next part of the command is the location of the Kora installation public directory, relative to your current location. And then the final part is the location of the desired subdirectory that will appear at the end of your site's URL. So in the case of a `public_html` example, the public directory of the installation files is located one directory up, and then inside of `kora`. So the command is:

        ln -s ../kora/public kora

    After both of these steps, your Terminal window will look something like this:

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_34_annotated.png" title="Set up Subdirectory Symbolic Link">

    This was the last bit of Terminal required for setup, so you may now close Terminal and return to cPanel Main. It isn't necessary, but if you wish, you can run the command `exit` to terminate your Terminal connection before navigating back to cPanel Main.

1. To confirm that the symbolic link process worked, you may go back into File Manager and navigate into your publicly-accessible directory, which you were to take note of in Step 2 of "[Upload and Prepare Kora Application Files via cPanel File Manager](#upload-and-prepare-kora-application-files-via-cpanel-file-manager)." There, you should find the directory "kora" with the black chain-link icon over the folder icon.

1. After completing this step, you will need to additionally configure Kora to enable functionality for a module called `mod_rewrite`. This is explained in the "[Using *mod_rewrite* in Kora](../advanced_configuration/#using-mod_rewrite-in-kora)" section of the "Advanced Configuration of Kora" page.

### Subdomain URLs

If going this route for your URL, you can now close Terminal and return to cPanel Main.

1. Setting up the subdomain option for your URL requires using the "Subdomains" tool in cPanel, under the "Domains" section.

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_35.1_annotated.png" title="cPanel's Subdomains">

1. In the Subdomain text box, type what you would like for your URL to begin with, before your site's main URL (remember the example above: https://subdomain.example.org). The selected "Domain" will likely default to your main URL, which is correct (in the case where you have multiple URLs available, choose the appropriate one). And the tool will autogenerate content in the "Document Root" box after you enter something in the "Subdomain" box; delete this autogenerated content and instead enter the directory tree for the public folder of your Kora installation. If you have been using all the same directory names and locations as this guide, then you will enter "kora/public" into this box. Then hit create. You can see all of this in this screenshot:

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_36_annotated.png" title="Create New Subdomain">

### Enable Force HTTPS for URL

Once you have implemented one of the two methods above, your Kora installation is now reachable via a web browser! But there is one last task you should complete before doing so.

!!! note
    If you previously had to implement the PHP version workaround to deal with an insufficient default server-wide PHP version, please return to [step XXXX of that guide](XXXXXXXX) to finish the HTTPS configuration process.

1. Kora is designed to use HTTPS protocol for its URLs. So it is important to set up a Force HTTPS Redirect for your domain, and for the subdomain as well if you have gone that route for your URL. To do this, go to "Domains" under the "Domains" section in cPanel.

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_35.2_annotated.png" title="cPanel's Domains">

1. For your main domain entry and subdomain entry on the list, click the toggle to turn it on (or ensure it is already toggled on for each).

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_37_annotated.png" title="Force HTTPS Toggled On for Domain and Subdomain (if applicable)">

    Toggling this setting may not immediately work, with an error displaying that might say, "You cannot activate HTTPS Redirect because AutoSSL is not currently active for this domain or the SSL certificate is not valid." If this happens, wait one or two minutes, refresh the page, then try toggling the setting on again.

Once completed, return to cPanel Main.

## Further Configure Kora Once Installed

In a new tab, navigate to your Kora application's URL. If everything has been done correctly, you should land on the login page for your Kora installation. But keep the cPanel open in another tab because you will need to switch back to it to set up your email at some point.

If you successfully reached the Kora login page, **Congratulations!** Your install is at least partially working!

1. From here you will log into the admin account in order to configure your installation properly, but also to test that your directory permissions settings are working properly.

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_38_annotated.png" title="Kora Login Page">

    The username is "admin" and the password is the one that you copied from Terminal, from the successful installation message. Put in that password to log in and you will land on a page that looks like this:

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_39_annotated.png" title="Successful Login to Kora">

1. It is highly recommended that you at some point click through the introduction to get a quick tutorial on the basics of using Kora. Once done, click on the menu icon in the top-right to bring out the side-bar menu.

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_40.1_annotated.png" title="Open Kora Menu">

    Then click on "Management" at the bottom and select "Kora Configuration File" from the options that appear.

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_41_annotated.png" title="Kora Configuration File Menu Item">

    This page provides text fields to update much of the information saved in that .env file you briefly edited back in Step 8 of "[Upload and Prepare Kora Application Files via cPanel File Manager](#upload-and-prepare-kora-application-files-via-cpanel-file-manager)."

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_42_annotated.png" title="Configuration File Page">

### Configure reCAPTCHA

!!! note
    Because this subsection regards setting up an external service, there are no screenshots provided.

**Kora currently uses reCAPTCHA v2 Checkbox**

1. Kora uses Google's reCAPTCHA service for anti-robot protections. As you can see on the screenshot above, the configuration file is asking for a "Recaptcha Private Key" and "Recaptcha Public Key", which you will get from that service. The reCAPTCHA documentation can be found at <https://developers.google.com/recaptcha>, but to create the keys needed for your site, you will go to <https://www.google.com/u/0/recaptcha/admin/>. Google will ask you to log in with a Gmail account. Many academic institutions have contracts with Google for using their tools via an educational arrangement; in the case of MSU, it is possible to give Google's login page an MSU email address, which then redirects to an MSU-related login page. Successfully logging in redirects back to reCAPTCHA under the MSU account. If this option is not available to you, unfortunately you will need a Gmail account to gain access to reCAPTCHA, which is required for completing Kora's installation setup.

1. Once logged in, if this is your first time using reCAPTCHA, it will automatically go to the registration page. However, if you have used reCAPTCHA before, it will take you to a page displaying the information for the first reCAPTCHA key set you created. To create a new set of keys, click on the plus icon in the upper-right to register a new site.

    Give your new set any label you prefer (a suggestion would be to use your Kora installation URL). As noted above, Kora currently uses reCAPTCHA v2 "I'm not a robot" Checkbox version, so pick those options. Under "Domains", write your main domain (do not include "http://", "https://", or the subdirectory) and either hit Enter or click the plus sign to add it to the list of approved domains for the set of keys that are about to be generated. As an aside: this functionality means you could conceivably have multiple Kora installations, or even multiple sites that use reCAPTCHA v2 Checkbox, all using the same keys.

1. The "Owners" section should auto-add your account email, but you can add another if you wish. Be sure to (review and) accept the Terms of Service. The final option is the checkbox for "Send alerts to owners", which you may wish to leave enabled so that you receive emailed updates when security issues with your site arise.

1. Finally, click "Submit". Once redirected back to the main page, the lighter-blue bar at the top will display the number of sites registered and have a dropdown list for you to select whichever. Obviously if this is the first time setting one up, you will only have one. Ensure the one you intend to use is selected in the dropdown and then click on the gear icon in the upper right to go to the reCAPTCHA "Settings" page. Click on the "reCAPTCHA keys" dropdown list to display your site and secret keys.

1. Copy the "site key" and paste it into your Kora Configuration File page text box titled "Recaptcha Public Key"; copy the "secret key" and paste it into the text box titled "Recaptcha Private Key". If you want to ensure this information is saved before setting up your email, scroll to the bottom of the page and click "Update Configuration File".

### GitLab Integration

If desired, your Kora installation can use GitLab's authentication system to manage account creation and user login. For more information about this, including integration instruction, please see the section of "Advanced Configuration" called, "[GitLab Integration](../advanced_configuration/#gitlab-integration)."

### Set Up Server Email and Link It to Kora

!!! warning "Email No Longer Supported"
    Kora 3 no longer supports email integration. A previous iteration of Kora 3 would generate emails for a number of tasks, such as account creation or password resets, and so email integration was encouraged. All the account management tasks that appeared to require email integration were possible without it, as explained in the guide for [managing Kora user accounts](../../user-accounts/managing_users_in_a_kora_installation/#manual-user-confirmationsactivations-and-password-resets). Though email integration is no longer supported, the setup process is preserved here for completeness of past documentation.

    This guide describes entering server information into a Kora Configuration File page and clicking "Update Configuration File", which would then save the information as values for variables found in the installation's .env file. "Mail Host" populated `MAIL_HOST`, "Mail From Address" populated `MAIL_FROM_ADDRESS`, "Mail From Name" populated `MAIL_FROM_NAME`, "Mail User" populated `MAIL_USER`, and "Mail Password" populated `MAIL_PASSWORD`. If something provided on the Kora Configuration File page contained spaces (e.g. if "Mail From Name" was set on this page to "Kora Admin"), the value in the .env file would be saved as a string surrounded by quotations.

!!! tip "Deprecated Guide"
    To set up mail for your Kora install, this guide will explain how to use the email client available through cPanel for your Domain of One's Own account. It is possible to set this up with other email clients, however this basic option is easiest for keeping the installation and email all under the one environment.

    1. Return to your tab with cPanel Main. Find "Email Accounts" under the "Email" section.

        <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_43_annotated.png" title="cPane's Email Account">

        To set up a Kora-specific email address, click on "Create".

        <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_44_annotated.png" title="Create a New Email">

        (You could also use the default email address that has already been generated if you like; if using the default email, skip to Step 4 below.)

    1. In the "Create an Email Account" box, look at the options available in the "Domain" dropdown menu. This will be the portion of the email address *after* the @ symbol. If using a subdomain URL, you can specify this subdomain here, otherwise your option will be limited to your main URL. After choosing the domain, enter a "Username", such as "admin" if you use the subdomain option, or "kora" if you use the main URL option. Finally, click on Generate in the "Password" section to receive a randomly generated password (as you did when setting up your MySQL database).

        <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_45_annotated.png" title="Add Information for Setting Up New Email Account">

        <br>

        !!! note "IMPORTANT"
            Just as before, ensure you copy this password and save it someplace safe, because it will be needed for email configuration in Kora.

    1. The remaining settings should be set according to your preferences. I will not outline how to link this email account to a mail client because the option to generate an email with just such a guide is provided by cPanel. Once everything is set as you like, click "Create", which, as long as you leave the "Stay on this page..." option unchecked, will create the address and redirect you back to the list of email addresses.

        <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_46_annotated.png" title="Complete the New Email Account Setup with Default Settings">

    1. To confirm that your address is working properly, click on "Check Mail" next to your new address in the list.

        <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_47_annotated.png" title="Check Mail for the New Address">

        Then click "Open" on the resulting page. As long as these pages load correctly, your server's email client is working correctly. If they do not — for instance, MSU's Domains of One's Own accounts currently are not working — you must contact the administrators of your server to rectify this.

    1. Return to your Kora Configuration File page tab. Scrolling down, you will find the text boxes for your email information. Leave "Mail Host" with "localhost". For "Mail From Address", it is best to enter the email address you just created so that the emails that users receive appear to come from that account; in this example, "admin@kora.geyerbri.msu.domains". Set the "Mail From Name" to your own preference, such as "Kora Admin". The "Mail User" setting is how Kora connects with your server's mail client, to actually send the email. So this one must be set to an appropriately-configured email, such as the one just created; in this example, "admin@kora.geyerbri.msu.domains" again. Finally, paste in the save email password into the last box, "Mail Password".

        Save all of these configurations by clicking "Update Configuration File". See all of these settings in this screenshot:

        <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_48_annotated.png" title="Add Email Information to Kora Configuration">

    !!! note
        If your server email is disabled by account administrators — as is the case for MSU Domains of One's Own accounts — and you cannot get another server email to successfully work with Kora, it is still possible to do the tasks that may appear to require the email server working, such as confirming new users, inviting users, or setting passwords. Find instructions for these tasks in the guide for [managing Kora user accounts](../../user-accounts/managing_users_in_a_kora_installation/#manual-user-confirmationsactivations-and- password-resets).

### Admin User Profile Settings

The final portion of configuration is for the admin account's profile settings. This section is specific to what is a part of the initial configuration for Kora, but this documentation website also has a more complete [guide for user profile settings](../../user-accounts/edit_user_preferences/).

1. To get there to the profile settings page, select the user icon in the upper-right.

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_40.2_annotated.png" title="Open User Menu">

    Then choose "Edit My Profile."

    <img style="display:block;margin:auto;max-width:100%" src="../getting-started-img/installing_kora_domains_49_annotated.png" title="User Profile Settings Menu Item">

1. On this page, you can change the username and password that were auto-generated when installing Kora in Terminal, however it is probably best to leave these alone. However, it *is* important to change the default admin email here because it is shown to users at various locations throughout Kora. Change it to either your own professional email address, or if you plan to check the server email account set up before (either through the interface you loaded before, or by forwarding it to an email client), set it to that address. You can also change the displayed admin name, if you wish, as it is also displayed to users in various locations. Finally, should you wish to change the admin account password from what was auto-generated to one you prefer, you can do that here.

1. Once all these have been set, click "Update Profile" to complete your setup.

## Testing the Installation

To check whether or not your installation works properly:

1. [Create a Project](../../projects/creating_a_project/).

1. [Create a Form](../../forms/creating_a_form/) in that project.

1. [Create a Field](../../forms/creating_fields/) in that project *with the field type set to one of the File types* (setting it to "Documents" will give the greatest flexibility for uploading any file to test).

1. And finally, [create a Record](../../records/creating_a_record/) where you upload an example file.

If the creation of that Record with an uploaded file succeeds, such that the uploaded file is viewable or downloadable when clicked upon, then your permissions are correct. If this fails, please go to "[Set 'Write' and 'Execute' Privileges On Certain Directories if Needed via cPanel Terminal](#set-write-and-execute-permissions-on-certain-directories-if-needed-via-cpanel-terminal)" above. Follow the instructions there for using cPanel Terminal to adjust your Kora installation's permissions on the correct directories.

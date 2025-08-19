## User Authentication in Infiniworkflow

Following the switch from Infiniworkflow being run on Flash to Django, we now have a number of new possibilities that were not as easily accessible before, including adding user authentication to the application. This provides a layer of security by requiring users to sign in before being able to access Infiniworkflow.

This is not enabled by default, but can be enabled easily by your administrator by running the following python script to create a INFINIWORKFLOW superuser:

     cd /path/to/INFINIWORKFLOW/app
     python3 create_superuser_script.py

With a superuser created, User Authentication is enabled. Now, when starting INFINIWORKFLOW, users will reach the login page and have to enter their login information to continue to INFINIWORKFLOW. Making pages such as the login page has taught me a lot about and built up my confidence in using HTML and CSS to create the frontend of applications.

![Login Page](/assets/ui_user_login_page.jpg)

When a user is finished using Infiniworkflow, they may click "Yes" or "Save and Exit" to exit the application, or they may click "Logout", which saves the current workflow and logs out of the session, returning back to the login screen.

As an Admin, you will have extended permissions that regular users won't, which includes making and removing users and groups. To access these controls, click on the Admin link and enter your admin username and password to continue. You will then reach a page like this, with all of the Admin controls available.

![Admin Page](/assets/ui_user_admin_page.jpg)







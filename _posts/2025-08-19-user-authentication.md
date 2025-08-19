## User Authentication in Infiniworkflow

Following the switch from Infiniworkflow being run on Flash to Django, we now have a number of new possibilities that were not as easily accessible before, including adding user authentication to the application. This provides a layer of security by requiring users to sign in before being able to access Infiniworkflow.

This is not enabled by default, but can be enabled easily by your administrator by running a Python script to create a INFINIWORKFLOW superuser. A portion of the Python script can be found below:

```
    def create_superuser_programmatically(username, email, password):
	    if User.objects.filter(username=username).exists():
	        print(f"Superuser '{username}' already exists.")
	    else:
	        User.objects.create_superuser(username=username, email=email, password=password)
	        print(f"Superuser '{username}' created successfully.")

	if __name__ == '__main__':
	    superuser_username = input("Enter your username: ")
	    superuser_email = input("Enter your email: ")
	    superuser_password = getpass.getpass("Enter your password: ")

    valid_email = re.match(r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$', superuser_email)
    valid_password_length = len(superuser_password) >= 8
    valid_password_type = not superuser_password.isnumeric()

    if not valid_email:
        print("Invalid email address")
    elif not valid_password_length:
        print("Password must contain at least 8 characters")
    elif not valid_password_type:
        print("Password cannot be entirely numeric")
    else:
        create_superuser_programmatically(superuser_username, superuser_email, superuser_password)
```
With a superuser created, User Authentication is enabled. Now, when starting INFINIWORKFLOW, users will reach the login page and have to enter their login information to continue to INFINIWORKFLOW. Making pages such as the login page has taught me a lot about and built up my confidence in using HTML and CSS to create the frontend of applications.

![Login Page](/assets/ui_user_login_page.jpg)

When a user is finished using Infiniworkflow, they may click "Yes" or "Save and Exit" to exit the application, or they may click "Logout", which saves the current workflow and logs out of the session, returning back to the login screen.

As an Admin, you will have extended permissions that regular users won't, which includes making and removing users and groups. To access these controls, click on the Admin link and enter your admin username and password to continue. You will then reach a page like this, with all of the Admin controls available.

![Admin Page](/assets/ui_user_admin_page.jpg)







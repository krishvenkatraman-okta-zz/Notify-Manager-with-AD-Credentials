# AD-Credential-Delivery

### <span style="text-decoration:underline;">Overview</span>

To Onboard users in an organization, Some big organizations provisions users to Microsoft active directory. Users do not get the system until day 1. Companies needs to provision these accounts ahead of time and send an email to users manager with one time password.

This flow adds the look for events when the user is pushed to activedirectory. This is set by Okta event added to application. On this event Okta goes to generate a one time password using Expire password API with tempPassword=true flag.

https://developer.okta.com/docs/reference/api/users/?_ga=2.144064246.2110324271.1598044957-208344352.1593389880#expire-password

    
    
### <span style="text-decoration:underline;">Before you get Started / Prerequisites</span>
Before you get started, you will need:

Access to an Okta tenant with Okta Workflows enabled for your org
Integrated with Active directory and enabled Active directory provisioning.
Setup user profile in Okta with proper manager username or manager email address. So that workflow can send to right manager.
Your organization should use Office 365 or Google email. 
If your organization uses O365 or google for email, Create a service mailbox that can be linked in Okta workflows to send email.


### <span style="text-decoration:underline;">Setup Steps</span>

1.Import the flopack in your workflow environment.
2.Setup a connection to Okta tenant.
3.Setup a Mail connection to O365 or google.
4.Open the AD activation flow and point the first card to the right AD APP in Okta.

![image](https://user-images.githubusercontent.com/14205843/90942085-12b4ec80-e3c9-11ea-83dc-89ae71eff88e.png)

5. Flow reads the existing user managerID from the user's profile and read the manager profile in Okta to grab the Manager emailAddress.

![image](https://user-images.githubusercontent.com/14205843/90942290-07ae8c00-e3ca-11ea-831e-87f783211322.png)

**If you have manager email address directory in the user profile. You can directly read that using the first read card and map the fields for email address in subsequient cards.**

6.In the end of the flow change the subject and body based on your company requirement. You can also construct the Body in html inside the compose card.
7.If you use O365 change the connection in the final O365 card. If you use Google remove the O365 card and add Google mail.
8.Activate the workflow


### <span style="text-decoration:underline;">Testing this Flow</span>

1) Create a new user and add the user to AD provisioning group.  
2) Successful provision to AD triggers an event call to Workflow and manager email is sent.


### <span style="text-decoration:underline;">Limitations & Known Issues</span>
1) Okta workflows does not have any on-premise connector at this time for writing. Provisioning will be through Okta.

# Introduction

In this tutorial, you will learn how to integrate Salesforce with Azure Active Directory (Azure AD). The scenario outlined in this tutorial consists of:

1.	Creating a Salesforce developer account
2.	Adding the Salesforce app to your tenant from the Azure AD gallery
3.	Assigning users to the Salesforce application in Azure AD
4.	Configuring and testing user account provisioning
5.	Configuring Azure AD single sign-on
6.	Configure Salesforce for single sign-on
7.	Testing single sign-on

## Assumptions

•	An Azure AD tenant with an admin account enabled

•	Valid email account


# Integrate Salesforce with Azure Active Directory for Single sign-on

## Task 1: Create a Salesforce developers account

1.	[Sign up](https://developer.salesforce.com/signup) for a Salesforce developer instance using a valid email address (you can use the same email address for your username).
2.	Go to your email inbox to verify the account. After signing in for the first time, Salesforce may send an extra verification code to your email.
3.	Open a new tab and sign into the same Salesforce admin account. On the top right corner of the page, click the view profile icon, and then click **Settings**
4.	On the left navigation pane, click **My Personal Information** to expand the related section, and then click **Reset My Security Token**.
5.	On the Reset Security Token page, click **Reset Security Token button**.
6.	Check the email inbox associated with this admin account. Look for an email from Salesforce.com that contains the new security token. Save the security token. You will need it later.
7.	Go back to the homepage by clicking on **home** at the top. On the left navigation pane, click **Company settings** to expand the related section, and then click **My Domain**.
8.	On My Domain, enter a domain name and check whether it’s available.
9.	Click on Register Domain. It can take few minutes to update its naming. You will receive an email when it’s done. The domain follows the pattern: *https://<subdomain>-dev-ed.my.salesforce.com*


## Task 2: Add Salesforce from the gallery

10.	Using the Office 365 credentials provided in the Resource tab, access the [Azure portal](https://portal.azure.com/). Then, on the left navigation panel, click **Azure Active Directory** icon.
11.	Click **Enterprise applications** from the menu to go to the Enterprise Applications - All Applications page. 
12.	Click the **New application** button at the top of the page.
13.	In the search box, type Salesforce and select it from the result panel (do not select the Sandbox version). Then click the **Add** button to add the application. It may take a few seconds to create your application. 

## Task 3: Assign a test user to the application

14.	In the menu on the left, click **Users and groups.**
15.	Click the **Add user** button. Then select **Users** on Add Assignment dialog.
16.	On Users dialog, select the test user from the Users list. Click the **Select** button. 
17.	On the **Select Role** dialog, select Chatter Free User. Click the **Select** button. 
18.	Click the **Assign** button on **Add Assignment** dialog.

## Task 4: Enable automatic user account provisioning

19.	In the menu on the left, click **Provisioning**.
20.	Set the Provisioning Mode to Automatic.
21.	Under the Admin Credentials section, provide the following configuration settings:	
	- In the **Admin Username**, type a Salesforce account name that has the System Administrator profile in Salesforce.com assigned.
	- In the **Admin Password**, type the password for this account.
	- In the **Secret Token**, paste the security token value you have saved previously. 
22. In the Azure portal, click Test Connection to ensure Azure AD can connect to your Salesforce app.
23.	Click Save. 
24.	Under the Mappings section, select **Synchronize Azure Active Directory Users to Salesforce**.
25.	In the Attribute Mappings section at the bottom of the dialog, click on Add New Mapping.
26.	On Edit Attribute dialog, perform the following actions
	- In the **Mapping type**, select Direct
	- In the **Source attribute**, select userPrincipalName
	- In the **Target attribute**, select FederationIdentifier
27.	Click Ok.
28.	Click Save at the top of the Attribute Mapping section
29.	Close the attribute mapping dalog to go back to the Provisioning configuration page. 
30.     Set the provisioning status toggle to on, to enable the Azure AD provisioning for Salesforce. 


## Task 5: Configure single sign-on for Azure AD

30.	In the Azure portal, on the Salesforce application integration page, click Single sign-on.
31.	On the Select a single sign-on method, select SAML to enable single sign-on.
32.	In step 1 (Basic SAML configuration), click the pen to edot the Sign on URL and Identifier:
	- In the **Sign-on URL** textbox, type the value using the following pattern:
	*https://<subdomain>-dev-ed.my.salesforce.com.*	
	- In the **Identifier** textbox, type the value using the following pattern:
	*https://<subdomain>-dev-ed.my.salesforce.com*

33.	In step 3 (SAML Signing Cerficiate), click on download certificate. You will import this certificate later in Salesforce.


## Task 6: Set up Salesforce for single sign-on

35.	Open a new tab in your browser and log in to your Salesforce administrator account.
36.	Click on the Setup under settings icon on the top right corner of the page.
37.	Scroll down to the **SETTINGS** in the navigation pane, click Identity to expand the related section. Then click Single Sign-On Settings.
38.	On the Single Sign-On Settings page, click the Edit button.
39.	Select SAML Enabled, and then click Save.
40.	Click New to configure SAML single sign-on settings.
41.	On the SAML Single Sign-On Setting Edit page, make the following configurations:
	- For the **Name**, type SSO Ignite demo.
	- In the **Issuer**, paste the value of SAML Entity ID (you can find this by clicking **view step-by-step" instructions** in the Azure Portal SSO configuration page and copying the entity id from step 5).
	- In the **Entity Id**, type your Salesforce domain name using the following pattern: *https://<subdomain>-dev-ed.my.salesforce.com*
	- To upload the Identity Provider Certificate, click **Choose File** to browse and select the certificate file, which you have downloaded from Azure portal.
	- As **SAML Identity Type**, choose: Assertion contains the Federation ID from the User object
	- For **SAML Identity Location**, select Identity is in the NameIdentifier element of the Subject statement.
	- For **Service Provider Initiated Request Binding**, select HTTP Redirect.
	- In **Identity Provider Login URL**, paste the value of Single Sign-On Service URL, which you have copied from Azure portal (step 1 of the SSO configuration page) 
	
42.	Finally, click Save to apply your SAML single sign-on settings.
43.	On the left navigation pane in Salesforce, click Company Settings to expand the related section, and then click My Domain.
44.	Scroll down to the Authentication Configuration section, and click the Edit button.
45.	In the Authentication Configuration section, Check the SSO Ignite demo as Authentication Service of your SAML SSO configuration, and then click Save.

## Task 7: Testing single sign-on

46.	In the Azure portal, on the Salesforce application integration page, click Single sign-on (step 5).
47.	On the Test single sign-on with Salesforce section, click Test.
48.	Click on Sign in as current user. 
49.	You will be redirected to the Salesforce sign-in page. Click on Log in using SSO Ignite demo. If you don’t see it, it can be located at the bottom of the page.

## Optional tasks

### Create a conditional access policies for blocking all users to access Salesforce

50. In the Azure portal, on the Salesforce application integration page, click **Conditional Access.**
51. At the top of the blade, click on **New Policy**.
52. In the Name field enter: *Blocking all users to access Salesforce*
53. Under Assignments, select **Users and Groups**. Then, select **Include - All Users**.
54. Click **done**.
55. Under Access Control, select **Grant**. Then, select **Block access**.
56. Click **Select**.
57. Under Enable policy, select **On**.
58. Click on **Create**, to create the policy.

### Test conditional access policy

59. In the Azure portal, on the Salesforce application integration page, click Single sign-on.
47.	On the Test single sign-on with Salesforce section, click Test.
48.	Click on Sign in as current user. 
49.	You will be redirected to the Salesforce sign-in page. Click on Log in using SSO Ignite demo. If you don’t see it, it can be located at the bottom of the page.

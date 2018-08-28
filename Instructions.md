# Introduction

In this tutorial, you learn how to integrate Salesforce with Azure Active Directory (Azure AD). The scenario outlined in this tutorial consists of:

1.	Creating a Salesforce developers account
2.	Adding Salesforce app from the Azure AD gallery
3.	Assign users to the Salesforce application in Azure AD
4.	Configuring and testing user provisioning
5.	Configuring Azure AD single sign-on
6.	Configure Salesforce for single sign-on
7.	Testing single sign-on

## Assumptions

•	An Azure AD tenant with an admin account enabled

•	Valid email account


# Integrate Salesforce with Azure Active Directory for Single sign-on

## Task 1: Create a Salesforce developers account

1.	Sign up for a Salesforce developer instance using a valid email address.
2.	Go to your email inbox to verify the account. After login for the first time, Salesforce may send an extra verification code to your email.
3.	For future steps, you need to get your Salesforce security token, Open a new tab and sign into the same Salesforce admin account. On the top right corner of the page, click the view profile icon, and then click **Settings**
4.	On the left navigation pane, click **My Personal Information** to expand the related section, and then click **Reset My Security Token**.
5.	On the Reset Security Token page, click **Reset Security Token button**.
6.	Check the email inbox associated with this admin account. Look for an email from Salesforce.com that contains the new security token. Save the security token. You will need it later.
7.	On the left navigation pane, click **Company settings** to expand the related section, and then click **My Domain**.
8.	On My Domain, enter a domain name and check whether it’s available.
9.	Click on Register Domain. It can take few minutes to update its naming. You will receive an email when it’s done. The domain follows the pattern: *https://<subdomain>-dev-ed.my.salesforce.com*


## Task 2: Add Salesforce from the gallery

10.	In the [Azure portal](https://portal.azure.com/), on the left navigation panel, click **Azure Active Directory** icon.
11.	Navigate to **Enterprise applications**. Then go to **All applications**.
12.	To add new application, click **New application** button on the top of dialog.
13.	In the search box, type Salesforce, select Salesforce from result panel then click **Add** button to add the application.

## Task 3: Assign a test user to the application

14.	In the menu on the left, click **Users and groups.**
15.	Click **Add user** button. Then select **Users** on Add Assignment dialog.
16.	On Users dialog, select the test user from the Users list. Click **Select** button. 
17.	On **Select Role** dialog, select Chatter External User. Click **Select** button. 
18.	Click **Assign** button on **Add Assignment** dialog.

## Task 4: Enable automated user provisioning

19.	In the menu on the left, click **Provisioning**.
20.	Set the Provisioning Mode to Automatic.
21.	Under the Admin Credentials section, provide the following configuration settings:	
	- In the **Admin Username** textbox, type a Salesforce account name that has the System Administrator profile in Salesforce.com assigned.
	- In the **Admin Password** textbox, type the password for this account.
22. In the Azure portal, click Test Connection to ensure Azure AD can connect to your Salesforce app.
23.	Click Save. 
24.	Under the Mappings section, select **Synchronize Azure Active Directory Users to Salesforce**.
25.	In the Attribute Mappings section, click on Add New Mapping.
26.	On Edit Attribute dialog, perform the following actions
	- In the **Mapping type**, select Direct
	- In the **Source attribute**, select userPrincipalName
	- In the **Target attribute**, select FederationIDentifier
27.	Click Ok.
28.	Click Save at the top of the Attribute Mapping section
29.	To enable the Azure AD provisioning service for Salesforce, change the Provisioning Status to On in the Settings section. Click Save.


## Task 5: Configure single sign-on for Azure AD

30.	In the Azure portal, on the Salesforce application integration page, click Single sign-on.
31.	On the Select a single sign-on method, select SAML to enable single sign-on.
32.	On the Basic SAML configuration, click on the pen to perform the following steps:
	- In the **Sign-on URL** textbox, type the value using the following pattern:
	*https://<subdomain>-dev-ed.my.salesforce.com.*	
	- In the **Identifier** textbox, type the value using the following pattern:
	*https://<subdomain>-dev-ed.my.salesforce.com*

33.	On the SAML Signing Certificate, click on download certificate.
34.	On the Set up Salesforce section, click Configure Salesforce, copy the SAML Entity ID and SAML Single Sign-On Service URL.

## Task 6: Set up Salesforce for single sign-on

35.	Open a new tab in your browser and log in to your Salesforce administrator account.
36.	Click on the Setup under settings icon on the top right corner of the page.
37.	Scroll down to the **SETTINGS** in the navigation pane, click Identity to expand the related section. Then click Single Sign-On Settings.
38.	On the Single Sign-On Settings page, click the Edit button.
39.	Select SAML Enabled, and then click Save.
40.	To configure your SAML single sign-on settings, click New.
41.	On the SAML Single Sign-On Setting Edit page, make the following configurations:
	- For the **Name** field, type SSO Ignite demo.
	- In the **Issuer** field, paste the value of SAML Entity ID, which you have copied from Azure portal.
	- In the **Entity Id** textbox, type your Salesforce domain name using the following pattern: *https://<subdomain>-dev-ed.my.salesforce.com*
	- To upload the Identity Provider Certificate, click **Choose File** to browse and select the certificate file, which you have downloaded from Azure portal.
	- As **SAML Identity Type**, choose one of the following options:		- Select Assertion contains the Federation ID from the User object, if Federation ID from the User object is being passed in SAML assertion
	- For **SAML Identity Location**, select Identity is in the NameIdentifier element of the Subject statement.
	- For **Service Provider Initiated Request Binding**, select HTTP Redirect.
	- In **Identity Provider Login URL** textbox, paste the value of Single Sign-On Service URL, which you have copied from Azure portal
	
42.	Finally, click Save to apply your SAML single sign-on settings.
43.	On the left navigation pane in Salesforce, click Company Settings to expand the related section, and then click My Domain.
44.	Scroll down to the Authentication Configuration section, and click the Edit button.
45.	In the Authentication Configuration section, Check the SSO Ignite demo as Authentication Service of your SAML SSO configuration, and then click Save.

## Task 7: Testing single sign-on

46.	In the Azure portal, on the Salesforce application integration page, click Single sign-on.
47.	On the Test single sign-on with Salesforce section, click Test.
48.	Click on Sign in as current user. 
49.	You will be redirected to the Salesforce sign-in page. Click on Log in using SSO Ignite demo. If you don’t see it, it can be located at the bottom of the page.

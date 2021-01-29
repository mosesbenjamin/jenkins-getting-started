# Jenkins-getting-start

__Installation__
- Head to jenkins.io, select either LTS/ Weekly release, download jenkins.war 
- Head to https://adoptopenjdk.net
- Select your prefered OS and run the installer
- Verify java installation using: java --version
- (Inside folder where the jenkins.war file is located) java -jar jenkins.war
- Take note of this section:
*************************************************************
*************************************************************
*************************************************************

Jenkins initial setup is required. An admin user has been created and a password generated.
Please use the following password to proceed to installation:

xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

This may also be found at: C:\Users\SOMEUSER\.jenkins\secrets\initialAdminPassword

*************************************************************
*************************************************************

- Visit localhost:8080 and fill the admin password field with the password above 
- Install suggested plugins or select plugins to select.
- Fill user information form
- Skip jenkins instance URL setup
- Start using jenkins
- ====================================================
- To wipe out jenkins state/ storage on disc: Delete C:\Users\SOMEUSER\.jenkins
- Re-run: java -jar jenkins.war 

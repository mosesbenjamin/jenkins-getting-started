# Jenkins-getting-started

__Manual Installation__
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
- To wipe out jenkins state/ storage on disc: Delete C:\Users\SOMEUSER\.jenkins
- Re-run: java -jar jenkins.war

__Installation with dockerhub__
- Spin up a jenkins container from a jenkins image on dockerhub
- Head to: https://hub.docker.com/r/jenkins/jenkins and select an image or use- docker run -p 8080:8080 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts

__Installation with docker-compose__
- docker compose up
- (Additional mail service included)
- docker compose ps
- docker compose down (To clean up)

__Building applications with freestyle jobs__
 - Create a freestyle job
__To clone source code__
- Head to "Configure", under SCM, provide repo URL with appropriate branch name
- Save configuration
- Build the job with "Build now"
- Use "Console output" to see build process and/status (failure or success build message)
__To compile and test source code__
- Head to "Configure"
- Under "Build", choose the "execute (windows)shell" option and add build steps
- To keep build outputs: Go to "Post-build Actions" under configure
- Select "Archive the artifacts"

__Configuring our job to trigger by pulling changes__
- Head to "Configure"
- Under "Build triggers", select "Poll SCM"

__Automating jobs configured with code__
- Jenkins + docker-compose makes it incredibly easy to run instances side by side on the same host by defining separate ports for your services
- Select pipeline option on jenkins when asked to create a new item
- Under pipeline, select "Pipeline script"
- ===========================================
- To clone a github repo
- Under Stage('Build") -> steps: provide github URL link.
- (Use the format:   git url: 'https://github.com/some-project-link.git',  branch: 'main')
- Save and hit "Build Now"
- ===========================================
- To compile source code
-  Use shell script or windows natch screen option depending on your operating system. E.g.,
// sh "mvn -Dmaven.test.failure.ignore=true clean package"

// To run Maven on a Windows agent, use
// bat "mvn -Dmaven.test.failure.ignore=true clean package"
- ==============================================
- Setting up post-build actions
- Divide project into logical steps with different stages... checkout, build, deploy to staging etc..
- Install "convert to pipeline plugin"

__Colocating jobs and source code with jenkinsfile__
- ===============================================
- Jenkins runner approach
- Configure .vscode folder with "jenkins runner installed" and hooked to a job
- Over on jenkins, create job with the same name as appears on pipeline.groovy script
- Hold CMD/CTRL + shift + p and run : Jenkins Runner: Run Pipeline Script On Default Job
- Configure email server:
- Configuring an email server
- Under "Configure", look for "Extended E-mail Notification"
- Set "SMTP Server" to the service name in docker-compose
- Set "SMTP Port" accordingly and save.
- =============================================
- Jenkinsfile approach
- Create a jenkinsfile
- Write pipeline script
- Under "configure" select "Pipeline script from  SCM" as pipeline definition and fill necessary build information.

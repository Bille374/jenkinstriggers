## jenkinstriggers


### Popular triggers
  - Git WEbhook
  - poll scm
  - scheduled jobs
  - remote triggers
  - build after other projects are built


### Steps:

  - Create git repository on github
  - Ssh auth
  - Create a Jenkins in git repo & Commit
  - Create Jenkins job to access Jenkinsfile from git repo
  - Test triggers

### Build Triggers Remotely
#### Generate JOB URL
1. Job Configure => Build Triggers 
2. Check mark on “Trigger builds remotely”
3. Give a token name
4. Generate URL & save in a file
#### Generate Token for User
1. Click your username drop down button (Top right corner of the page)
2. configure => API Token => Generate
3. Copy token name and save username:tokenname in a file
#### Generate CRUMB
1. wget command is required for this, so download wget binary for git bash
2. Extract content in c:/program files/Git/mingw64/bin
3. Run below command in Git Bash, (replace username,password,Jenkins URL)
wget -q --auth-no-challenge --user username --password password --output-document - 
'http://JENNKINS_IP:8080/crumbIssuer/api/xml?xpath=concat(//crumbRequestField,":",//crumb)'
4. Save the token in a file
#### Build Job from URL
By now we should have below details
1. JENKINS Job URL with token
E:g http://52.15.216.180:8080/job/vprofile-Code-Analysis/build?token=testtoken
2. API Token
USERNAME:API_TOKEN
E:g admin:116ce8f1ae914b477d0c74a68ffcc9777c
3. Crumb
E:g Jenkins-Crumb:8cb80f4f56d6d35c2121a1cf35b7b501
Fill all the above details in below URL and Execute
curl -I -X POST http://username:APItoken @Jenkins_IP:8080/job/JOB_NAME/build?token=TOKENNAME 
-H "Jenkins-Crumb:CRUMB"
e:g curl -I -X POST http://admin:110305ffb46e298491ae082236301bde8e@52.15.216.180:8080/job/
vprofile-Code-Analysis/build?token=testtoken -H "Jenkins-Crumb:8cb80f4f56d6d35c2121a1cf35b7b501

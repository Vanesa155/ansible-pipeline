# Ansible Pipeline 

## Ansible Setup

### 1. Configure Ansible
- Added `ansible.cfg` to handle passwords.
- Created `inventory.ini` to define the machines where services will be installed.
- Added `plugins.txt`, as it is required in `playbook.yml`.

### 2. Additional Installations
- Added **OpenJDK 17** to the **nginx** machine so that the Jenkins agent can run.
- Updated **Jenkins** and **SonarQube** to the latest versions.

### 3. Run the Playbook
Run the playbook using:

```bash
ansible-playbook -i inventory.ini playbook.yml
```

![Description](img/1.png)

## Jenkins Configuration

   
   ![Description](img/2.png)

### Requirements
Before setting up Jenkins, install the following plugins:
- **SSH Build Agents**: To add the agent in Jenkins.
- **GitHub Plugin**: To clone and use the project repository.
   
   ![Description](img/3.png)
   
   ![Description](img/4.png)
   
   ![Description](img/5.png)
   
   ![Description](img/11.png)
### Add Credentials to Jenkins
1. In Jenkins, go to **Manage Jenkins > Manage Credentials**.
2. Add new credentials using **username and password** (instead of RSA keys, which can be problematic).
3. It should look like this:
   
   ![Description](img/6.png)


### Configure the Jenkins Agent
1. In Jenkins, go to **Manage Nodes and Clouds > New Node**.
2. Fill in the agent configuration, **making sure to add a label** to use later.
   
   ![Description](img/7.png)
   
   ![Description](img/8.png)   
    
   
3. In the SSH connection section, add the **IP address** of the machine where the agent will run.
   
   ![Description](img/9.png)
   
4. Save the configuration and **launch the agent**.
5. Ensure that Java is installed on the agent machine, as Jenkins requires it to run.
6. Verify that the agent is running correctly by checking the logs:
   
   ![Description](img/10.png)

If you encounter issues, check the logs and make sure the SSH connection is working properly.

## Creating the Task (Job) in Jenkins

1. In Jenkins, create a new task and give it a name.
2. **Restrict task execution** to the node where the agent is located, using the same label assigned earlier.
   
   ![Description](img/12.png)

3. **Add the Git repository URL**, ensuring you are using the correct branch (`main` or `master`).

   
   ![Description](img/13.png)
   
   
4. **Set up a Shell script** to move the files to the default nginx directory:
   
   ![Description](img/16.png)
   

5. **Run the task and check the console output** to ensure everything is working correctly.
   
   ![Description](img/18.png)
## Deployment Verification

1. Open a browser and go to `http://<SERVER_IP>:8080`.
2. If everything was set up correctly, you should see the app running:
   
   ![Description](img/19.png)


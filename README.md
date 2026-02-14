<h1 align="center">Automated React Deployment on AWS</h1>

<p align="center">
Terraform provisions infrastructure • Ansible configures server • Nginx serves app
</p>
<p align="center">
  <img src="https://img.shields.io/badge/Terraform-IaC-purple?style=for-the-badge&logo=terraform"/>
  <img src="https://img.shields.io/badge/Ansible-Configuration-red?style=for-the-badge&logo=ansible"/>
  <img src="https://img.shields.io/badge/AWS-EC2-orange?style=for-the-badge&logo=amazonaws"/>
  <img src="https://img.shields.io/badge/Nginx-WebServer-green?style=for-the-badge&logo=nginx"/>
</p>

<p align="center">
<img src="screenshots/fINAL DEPLOYMENT.png" width="800"/>
</p>

<p align="center">
<i>Infrastructure becomes reproducible, server becomes replaceable.</i>
</p>

## Terraform Provisioning
<img src="screenshots/init.png" width="700"/>

## SSH Key Automation
<img src="screenshots/createkeyterrafrom.png" width="700"/>

## Configuration with Ansible
<img src="screenshots/finally.png" width="700"/>


## Documentation
 <h3>Problem</h3> <p> Deploying a website traditionally involves manual steps: </p> <ul> <li>Create a server</li> <li>Configure networking</li> <li>SSH into the machine</li> <li>Install dependencies</li> <li>Copy files</li> <li>Start services</li> </ul> <p> This process is slow, error-prone and not reproducible. If the server is lost, the setup must be remembered and repeated manually. </p>
<h3>Solution</h3> <p> This project converts deployment into code by separating responsibilities: </p> <ul> <li><b>Terraform</b> creates infrastructure and access</li> <li><b>Ansible</b> prepares the machine and deploys the application</li> </ul> <p> The same commands recreate the working system at any time. </p>
<h3>How the System Works</h3> <ol> <li>Terraform provisions an EC2 instance and networking rules</li> <li>Terraform generates an SSH key locally using TLS</li> <li>The public key is injected into the instance</li> <li>The React app is built into static production files</li> <li>Ansible connects using the generated key</li> <li>Nginx is installed and configured</li> <li>The website is deployed and served</li> </ol> <p><b>Result:</b> A working website available on the public IP.</p>
<h3>Key Design Decision — Automated SSH Access</h3> <p> Normally AWS requires manually downloading a keypair before login, which breaks automation. </p> <ul> <li>SSH key generated locally by Terraform</li> <li>Public key uploaded automatically</li> <li>Ansible uses the same key</li> </ul> <p> Access becomes part of infrastructure rather than a manual prerequisite. </p>
<h3>Why React Build is Required</h3> <p> The server does not run React. </p> <p><code>npm run build</code> converts the application into static files:</p> <ul> <li>HTML</li> <li>CSS</li> <li>JavaScript</li> </ul> <p> Nginx serves these files directly to the browser, removing the need for Node.js on the production server. </p>
<h3>Deployment</h3> <pre> terraform apply ansible-playbook -i inventory.ini deploy-playbook.yml </pre> <p>Destroy and recreate:</p> <pre> terraform destroy terraform apply ansible-playbook -i inventory.ini deploy-playbook.yml </pre>
<h3>Outcome</h3> <ul> <li>No manual server configuration</li> <li>Identical deployments every time</li> <li>Infrastructure becomes disposable</li> <li>Access and setup fully automated</li> </ul>
<h3>What This Demonstrates</h3> <ul> <li>Infrastructure as Code</li> <li>Configuration Management</li> <li>Automated credential handling</li> <li>Separation of provisioning and configuration</li> <li>Reproducible deployments</li> </ul>

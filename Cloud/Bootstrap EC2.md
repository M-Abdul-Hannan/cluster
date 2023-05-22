
### Bootstrap EC2

Click on Advanced detail <br>
Copy and paste the below code in User Data  
```
#!/bin/bash
sudo su
apt-get update -y
apt install apache2 -y
service apache2 start
```

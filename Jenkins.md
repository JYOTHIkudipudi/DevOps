# Jenkins & Tomcat 9 Setup on Ubuntu 24.04

## Prerequisites
Ensure you have access to an Ubuntu 24.04 server, EC2 instance, or virtual machine.

---

## 1️⃣ Connect to the Server
```bash
ssh user@your-server-ip
sudo su
apt update && apt upgrade -y
clear
```

---

## 2️⃣ Install Java (OpenJDK 17)
```bash
apt install openjdk-17-jdk -y
java -version
```

---

## 3️⃣ Install Maven
```bash
apt install maven -y
mvn -version
```

---

## 4️⃣ Install Git
```bash
apt install git -y
git --version
```

---

## 5️⃣ Install Jenkins
### 🔗 Official Jenkins Documentation: [Jenkins Installation Guide](https://www.jenkins.io/doc/book/installing/)
```bash
wget -O /usr/share/keyrings/jenkins-keyring.asc \
https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

apt-get update
apt-get install jenkins -y
systemctl enable jenkins
systemctl start jenkins
systemctl status jenkins
```

---

## 6️⃣ Install Docker
### 🔗 Official Docker Documentation: [Docker Installation Guide](https://docs.docker.com/engine/install/ubuntu/)
```bash
apt install docker.io -y
usermod -aG docker jenkins
systemctl start docker
systemctl enable docker
systemctl status docker

apt update
apt install apt-transport-https ca-certificates curl software-properties-common -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
apt-get update
apt install docker-ce -y
systemctl status docker

docker run hello-world
```

---

## 7️⃣ Install & Configure Tomcat 9
### 🔗 Official Tomcat Website: [Apache Tomcat 9](https://tomcat.apache.org/)

```bash
mkdir -p /opt/tomcat9
cd /opt/tomcat9

wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.98/bin/apache-tomcat-9.0.98.tar.gz
tar -xvzf apache-tomcat-9.0.98.tar.gz
mv apache-tomcat-9.0.98/* /opt/tomcat9/

cd /opt/tomcat9/bin
sh startup.sh

ps aux | grep tomcat
netstat -tulnp | grep 8080
```

---

## 8️⃣ Change Tomcat Port (Optional)
```bash
vim /opt/tomcat9/conf/server.xml
# Change port from 8080 to 9090 (or any custom port)

ss -tulnp | grep 9090
```

---

## 9️⃣ Create Tomcat Service
```bash
groupadd tomcat
useradd -s /bin/false -g tomcat -d /opt/tomcat9 tomcat
chown -R tomcat:tomcat /opt/tomcat9
chmod -R 755 /opt/tomcat9
```

Create a new service file:
```bash
vi /etc/systemd/system/tomcat.service
```
Paste the following:
```ini
[Service]
Type=forking
User=tomcat
Group=tomcat
Environment="JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64"
Environment="CATALINA_HOME=/opt/tomcat9"
ExecStart=/opt/tomcat9/bin/startup.sh
ExecStop=/opt/tomcat9/bin/shutdown.sh
Restart=always
```
```bash
systemctl daemon-reload
systemctl restart tomcat.service
systemctl status tomcat9
```

---

## 🔟 Deploy a WAR File in Tomcat
1. Copy your `app.war` file to Tomcat’s `webapps/` directory:
```bash
cp /path/to/your-app.war /opt/tomcat9/webapps/
```
2. Restart Tomcat:
```bash
systemctl restart tomcat.service
```
3. Access the application:
```
http://your-server-ip:9090/your-app
```

---

## ✅ Conclusion
This guide covers the complete **Jenkins & Tomcat 9 setup** on Ubuntu 24.04 along with **Docker installation** and **WAR file deployment**. 🚀

---

### 🔥 Need More Help?
🔗 [Jenkins Documentation](https://www.jenkins.io/doc/)  
🔗 [Tomcat Documentation](https://tomcat.apache.org/tomcat-9.0-doc/)  
🔗 [Docker Docs](https://docs.docker.com/)  

💡 **Now you are ready to automate builds and deploy applications efficiently!** 🚀

## Setup-Edge-Server-GCS

# Log to root user
sudo su

# Update package
sudo apt-get update

# Installer java
sudo apt-get install openjdk-7-jdk

# Vérifier si java est bien installé
java -version

# Setting env variables
## Create .bash_profile file
sudo nano ~/.bash_profile
## Copy the code bellow in .bash_profile file
export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
export PATH=$PATH:/usr/lib/jvm/java-7-openjdk-amd64
## Launch .bash_profile file
source ~/.bash_profile
## Check java home
echo $JAVA_HOME


# Install ssh et sshd
sudo apt-get install ssh
sudo apt-get install openssh-client
sudo apt-get install openssh-server
sudo /etc/init.d/ssh restart

# Create user
sudo adduser test1 # password test1
sudo adduser test2 # password test2
sudo adduser test3 # password test3
sudo adduser test4 # password test4

# Grant suddoers privilege acces to user test1
sudo adduser test1 sudo 
sudo adduser test2 sudo 
su - test1
exit

# Create analytics group 
sudo groupadd analytics

# Add users test1, test3 and test4 in analytics group
sudo adduser test1 analytics
sudo adduser test3 analytics
sudo adduser test4 analytics

# Cretating analytics folder in home repository
sudo mkdir /home/analytics

# Jailled each user in him home repository
sudo chmod a-srwx /home/test1
sudo chmod u+srwx /home/test1

sudo chmod a-srwx /home/test2
sudo chmod u+srwx /home/test2

sudo chmod a-srwx /home/test3
sudo chmod u+srwx /home/test3

sudo chmod a-srwx /home/test4
sudo chmod u+srwx /home/test4

# Make other folder inavalable for nonsudoers user
sudo chmod a-srw /dev
sudo chmod a-srw /etc
sudo chmod a-srw /lib
sudo chmod a-srw /usr
sudo chmod a-srw /bin

# Make analytics folder available for group user
sudo chmod a-srwx /home/analytics
sudo chmod g+srwx /home/analytics
sudo chgrp -R analytics /home/analytics

# Add new user 
sudo adduser test5 # password test4
sudo chmod a-srwx /home/test5
sudo chmod u+srwx /home/test5
sudo adduser test4 analytics
sudo adduser test1 sudo


# Install pip and virtualenv
sudo apt-get install python-pip python-dev build-essential 
sudo pip install --upgrade pip 
sudo pip install --upgrade virtualenv

# Create a virtualenv
virtual env venv

# Activate virtual env
source venv/bin/activate
pip install requests
pip freeze | grep requests

deactivate
pip freeze | grep requests

# 
# Générer une clé ssh pour pouvoir ouvrir une session sur le noued sans fournir le mot de passe
ssh-keygen -t rsa -P ""

# Ajouter la clé publique à la liste des clés acceptées
#chmod 755 /home/hadoop/.ssh/id_rsa.pub
#chmod 700 /home/hadoop/.ssh/id_rsa
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

# Tester la connexion au local host
ssh localhost
exit

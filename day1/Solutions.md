ASSIGNMENT 1

TASK 1 :- Install and configure Apache2.
 STEPS  :- 
```
                           # apt-get insatll apache2 -y (as a root user)
                           # systemctl status apache2.service (should be active)
                           # cd /var/www/html
                           # vim index.html (hi! I am devops ninja)
```

TASK 2 :- Install and configure nginx – configure it to run a                  proxy to apache.
STEPS   :- 
```
                           # apt-get install nginx (It will not run either stop apache or change the port)
                           # cd /etc/apache2
                           # vim ports.conf (changed the port to 81)
                           # vim /etc/nginx/sites-available/defaults
                           # mv defaults proxytest (changed the file defaults to proxytest)
                           # vim proxytest 
```

( server {

listen 80;

server_name proxy_test.com;

location / {

proxy_pass http://192.168.33.10:81;}} )
```
                              # ln -s /etc/nginx/sites-available/proxytest proxytest
                              # vim /etc/host ( add – 192.168.33.10 proxytest.com )
```
Now, nginx is working as a proxy server of apache2.

TASK 3 :- Install & Configure ntp with singapore timezone.
Steps    :-  
```
                          # apt-get install ntp
                          # vim /etc/ntp.conf ( edit the singapore pool.ntp.org configuration)
                          # systemctl restart ntp
                          # apt-get install ntpdate -y
                          # ntpdate 
```

TASK 4 :- Install tomcat version 8.
Steps    :-  
```
                          # wget http://www-eu.apache.org/dist/tomcat/tomcat-8/v8.5.31/bin/apche-tomcat-8.5.31.tar.gz
                          # cd /opt/tomcat
                          # tar xzvf apache-tomcat-8.5.31.tar.gz -C /opt/tomcat
```                          
                                                             configured tomcat – Install Java with home environment
                                                             Installed apache tomcat version 8
                                                             Created tomcat group and user
                                                             Test apache tomcat on 8080 by config. ~/bashrc
                                                             Setup Apache tomcat.service
                                                             Config. Apache tomcat user in /opt/tomcat/conf/
                                                             Edited users.xml & context.xml
                                                             Testing tomcat



TASK 5 :- Install java8.
Steps    :-               
```
                          # add-apt-repository ppa:webupd8team/java
                          # apt-get update
                          # apt-get install oracle-java8-installer  -y
                          # update-alternatives  --config java
                          # vim /etc/environment ( JAVA_HOME=”/usr/lib/jvm/java-8-oracle/jre”) 
                             # vim ~./bashrc ( export java home and path)
                             # source ~/.bashrc
                             # echo $JAVA_HOME
```

TASK 6 :- Install build-essential.
Steps    :-  # apt-get install build-essential
Theory  :-  
Why we need build-essentials?
1. This package is recquired for building debian-packages.
2. If you have this package installed, you only need to install whatever a package specifies as its build-time dependencies to build the package. Conversely, if you are determining what your package needs to build-depend on, you can always leave out the packages this package depends on.
3. This package consist of various tools :- dpkg-dev, g++, gcc, libc-dev, etc.
4. This package provides the c, c++ environment.


TASK 7 :- Install logrotate & rotate tomcats catalina.out logs.
Steps    :- 
```
                        # apt-get install logrotate -y
                        # cd /etc/logrotate.d
                        # touch tomcat
                        # vim tomcat 
```
( /opt/tomcat/apache-tomcat-8.5.31/logs/catalina.out
{
rotate 5
create
size 500K
compress
delay compress
}
```   
                     # logrotate -f /etc/logrotate.conf
```



TASK 8 :- Install git.
Steps    :- 
```
# apt-get install git
```
Theory  :-
What is git?
1. By far, the most widely used modern version control system in the world today is Git.
2. Git is a mature, actively maintained open source project originally developed in 2005 by Linus Torvalds, the famous creator of the Linux operating system kernel.
3. Linus Torvald make it because Bitbucket started charging him for space. (abhishek told me :) ).
4. A staggering number of software projects rely on Git for version control, including commercial projects as well as open source.
5. Having a distributed architecture, Git is an example of a DVCS (hence Distributed Version Control System).
6. Rather than have only one single place for the full version history of the software as is common in once-popular version control systems like CVS or Subversion (also known as SVN), in Git, every developer's working copy of the code is also a repository that can contain the full history of all changes.
7. Using github developers can share their code.
8. In jenkins, code is picked up from github.
9. Our assignments are also shared by github. Its amazing.


TASK 9 :- Mention the log files.
Theory  :- 
1. Apache - /var/log/apache2
2. Nginx - /var/log/nginx
3. Ntp - /var/log/ntpstats
4. Tomcat - /opt/tomcat/apache-tomcat-8/logs/catalina.out
5. Java - /var/log

TASK 10 :- Mention the files created after installation.
Theory  :-
1. Apache – apache2
2. Nginx – nginx
3. Tomcat – apache-tomcat-8.5.31

                           
                           
 

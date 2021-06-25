Assignment 3

Task1:- Make a script and pass 5 command line arguments (arguments value should be interger)
Script:- 
```
              #!/bin/bash
              echo $1, $5
              if [ $2 -eq 10 ]
              then
              echo "INDIA"
              else
              echo "india"
              fi
              for i do
              sum=$(expr $sum + $i)
              done
              echo $sum
```
Output1:-
```
# ./task1.sh 1 4 6 10 8
```
1, 8
INDIA
29
Output2:-
```
# ./task1.sh 1 2 3 4 5
```
1, 5
india
15






Task2 :- Make a script and pass one command line arguments(use loop)
print the table of command line argument if value is less 10
print 5 times "INDIA" if value is greater than or equal to 10
Script:-      
```
              #!/bin/bash
              if [ $1 -le 9 ]
              then
              for i in 1 2 3 4 5 6 7 8 9 10
              do
              a=$( expr $1 '*' $i)
              echo $a
              done
              elif [ $1 > 10 ]
              then
              for i in 1 2 3 4 5
              do
              echo "OPSTREE"
              done 
              fi
```



Output1 :- 
```
# ./task2.sh 5
```
5
10
15
20
25
30
35
40
45
50
Output 2:- 
```
#  ./task2.sh 10
```
OPSTREE
OPSTREE
OPSTREE
OPSTREE
OPSTREE




Task3 :- Make a script and print your name 10 times(use fuction to print your name)
Script:- 
```
              #!/bin/bash
              printname ()
              {
              for i in {1..10}
              do 
              echo $1
              done
               }
               printname $1 
```
Output:-# ./task3.sh love
love
love
love
love
love
love
love
love
love
love
Task4:- Make a excel sheet manually with 5 column, and print the 1st,3rd and 5th column
```
# sed 's/,/ /g' testsed.csv | awk '{print $1,$3,$5}'
```

Task5:- Install the zabbix-agent using shell script
Script:- 
```
              #!/bin/bash
              sudo apt-get update
              sudo apt-get install zabbix-agent -y
              sudo systemctl start zabbix-agent
              sudo sed -i 's/Server=127.0.0.1/Server=zabbix.opstree.com/'   /etc/zabbix/zabbix_agentd.conf
               sudo sed -i          's/Hostname=Zabbix/Hostname=192.168.0.20- zabbixagent/' /etc/zabbix/zabbix_agentd.conf
                sudo service zabbix-agent restart
```
  
Task 6:- Make a script in which you will pass a git repo path and it will generate a html report of last 5 days commits.                                                               1. Html report should contain
Commit Message
Commit ID
Author Name
Commit Date
Script:- 
```
#!/bin/bash
mkdir gittest
cd gittest
sudo git clone https://github.com/apache/hadoop.git -y
sudo chmod 777 hadoop
cd  hadoop
sudo git log –since=”5 days” --pretty=format:’%cd,                                  %an,%B,%cm’ > log.csv
cat log.csv
```


Task7:-  
```
              #!/bin/bash
              printf "Enter any charcter you want to print: "
              read character
              echo "Enter number of times you want to                      print $character"
              read number
              echo $number
              for i in  $(seq "$number")
              do
              echo $character
              done
```
Output:- 
```
# ./rajattask.sh
```
Enter any charcter you want to print: opstree
Enter number of times you want to print opstree
5
5
opstree
opstree
opstree
opstree
opstree 

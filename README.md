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
  
Sudo NetDiscover

Found the IP 192.168.0.131 

![Screenshot from 2023-01-19 01-55-20](https://user-images.githubusercontent.com/108471951/213287257-c109721a-ccfa-4bd8-aea1-f42411a9f400.png)



Firstly we have to identify the machine IP address using tool like NetDiscover 

###Nmap

nmap -sC -sV -p- 192.168.0.131


![Screenshot from 2023-01-19 01-57-13](https://user-images.githubusercontent.com/108471951/213287521-1a995297-b7d5-4679-a74d-2eb7047c0463.png)

so we can see it its a worpress site in nmap result.


 By searching the ip in browser ,we can see in website footer its mentioned it is a wordpress website.

![Screenshot from 2023-01-16 17-00-08](https://user-images.githubusercontent.com/108471951/213288183-7462e484-ff1c-4f78-b14a-70669e3c415b.png)


In website We found a Flag1


![Screenshot from 2023-01-16 17-01-22](https://user-images.githubusercontent.com/108471951/213289621-ccb28013-29c2-4dbf-a771-0626321c8454.png)


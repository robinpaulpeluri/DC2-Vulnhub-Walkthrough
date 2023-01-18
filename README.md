# DC2 Vulnhub Walkthrough

####Description

Much like DC-1, DC-2 is another purposely built vulnerable lab for the purpose of gaining experience in the world of penetration testing.

As with the original DC-1, it's designed with beginners in mind.

Linux skills and familiarity with the Linux command line are a must, as is some experience with basic penetration testing tools.

Just like with DC-1, there are five flags including the final flag.

And again, just like with DC-1, the flags are important for beginners, but not so important for those who have experience.

#####In short, the only flag that really counts, is the final flag.


 # Scaning
  
  ### Reconnaissance 
  
Sudo NetDiscover

Found the IP 192.168.0.106 {Note - your IP may Different}

![Screenshot from 2023-01-19 01-40-20](https://user-images.githubusercontent.com/108471951/213284288-44af1562-2f39-4818-b57e-393e212bf80d.png)

Firstly we have to identify the machine IP address using tool like NetDiscover 

###Nmap

nmap -sV -p- 192.168.0.106

![Screenshot from 2023-01-19 01-50-24](https://user-images.githubusercontent.com/108471951/213286156-9f01da43-332e-4fd7-8883-2c2e58175759.png)





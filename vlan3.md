Vlans(part3)
- to configure  Vlan on a router;
	- encapsulation dot1q vlan-id native
		<img width="860" height="129" alt="image" src="https://github.com/user-attachments/assets/c981d4e6-46b9-4dc0-ab34-5fcaef486f45" />

	- or
	- configure native vlan on the router physical interface
		- <img width="913" height="157" alt="image" src="https://github.com/user-attachments/assets/8ef91640-d028-4ec5-a89b-aaceea369aaf" />

		- here we removed the subinterfaces 
		- and inter to the g0/0 interface => put the ip address on that interface then show the interfaces on the router will show that;
			- <img width="565" height="403" alt="image" src="https://github.com/user-attachments/assets/34cd9ee2-a989-46bb-b256-ff1f01ce54e9" />

				- you have interface on G0/0 with an ip address for the native vlan 
				- you have other interfaces with dot1q encapsulation for other vlans
				- 
- now let's analyse the traffic that going from sw2 to R1 on wireshark;
	- <img width="947" height="497" alt="image" src="https://github.com/user-attachments/assets/35c92333-63e1-4bb6-8c88-4601464ddfb6" />

		- <img width="890" height="283" alt="image" src="https://github.com/user-attachments/assets/f1d8f83e-c482-4e71-b4cf-ebbd18e0e7dc" />

		- you need to know ;
			- that type of the vlan is 802.1Q and it's hexadeciaml value 0x8100 -
			- note; the type field is after source field of the analysis
			- and the type filed is part of TPID as we discuss before (0x8100) is the value that stored inside TPID.
			-<img width="399" height="135" alt="image" src="https://github.com/user-attachments/assets/7c7902f0-73c3-4aa1-90f7-7011849aa809" />

		- after the TPID you have TCI;
			- PCP -> periority code point -> default here is 0 (3bits)
			- DEI -> drop eligible indicator (1 bit )  it's value is 0
			- VID ->vlan identifier -> (12 bits) type of vlan is 20
		- so all of these called: ICMP
	- also you have the source ip,destination ip
- ---
- now the message will return from R-> Sw2
	- this is the output ;
		- <img width="944" height="169" alt="image" src="https://github.com/user-attachments/assets/d1e067de-d187-4f35-92c3-726f240637f5" />

		- you have the src ip, destination ip 
---
What is the Multilayer 3 switches?
- <img width="843" height="416" alt="image" src="https://github.com/user-attachments/assets/af6a4715-3f94-4b36-85dd-26c369ff7902" />

- it's a multilayer switch used for both -> switching,routing
- you can configure ip address on it's interfaces like router
- you can use virtual vlan on it's interfaces +assign ip addresses to it.
- you can uses it for vlan routing
- 
----
Multilayer 3 switch?
- can be used as 
	- switch virtual interfaces(SVI) =>is to assign a virtual addresses to it's interfaces.
	- then you can configure each pc to use SVI as their gateway address.
	- so; to send the traffic to different pcs -> pc send traffic to the switch(Multilayer switch)=> then it will forward it to the the subnets you need to send to.
- ex;
	- <img width="957" height="475" alt="image" src="https://github.com/user-attachments/assets/507a4dd1-6aa3-48bb-9597-b5285671bef8" />

	- here if we need to send the traffic from pc in vlan20 through multilayer switch -> multilayer switch will tagged it to the vlan of destination address 
	- then sw2(layer2 switch) will receive that traffic and forward it to the destination pc .1 in vlan 10 at the above floor .
	- ex;
		- what if we need to send traffic to the cloud or internet so we will configure the stick between sw2,R1 by assigning an IP address on it
		- then and give an ip address for the sw2,and one for R1
		- now we will use default routing to send the traffic from sw2 to the internet
		- here are the commands to configure it on the router , switch;
			-<img width="906" height="344" alt="image" src="https://github.com/user-attachments/assets/aa5a041a-012b-41b2-b5cb-30815c671285" />

			- he removed subinterfaces on g0/0.10,g0/0.20,g0/0.30
			- then return the g0/0 to it's default way .
			- then he showed the ip of the interfaces on  the router
			- <img width="931" height="293" alt="image" src="https://github.com/user-attachments/assets/3e3b2069-484d-4dc9-b8f7-6e2bc43d921a" />

			- then he assign an ip address for that interface 
				- interface name
				- then ; ip address  network+host portion then subnet mask of it .
				- then ; do show ip interfaces brief.
			- <img width="852" height="464" alt="image" src="https://github.com/user-attachments/assets/27c24049-239f-4c81-a9b7-68b57ee1ec2f" />

				- then do the same on the switch;
					- make the default interface to be g0/1
					- then activate the ip routing on the switch
						- then go to interface g0/1
						- then; no switchport -> make that interface as router port (note that)
						- then assign to it an ip address with a subnet mask
						- then do show ip interface brief
					- then you will see the ip is on the switch .
			- <img width="815" height="459" alt="image" src="https://github.com/user-attachments/assets/48680475-70a2-4e15-a113-3128baa3a71a" />

			- now we need to allow for sw2 to forward the traffic to the internet(cloud)
				- exit 
				- then assign default route 0.0.0.0 0.0.0.0 next hub(R2 to be accessed by the sw2)
				- then do show ip route 
					- will show that you routed to the next hub(R2) with the ip address 0.0.0.0 and his ip addreess
			- or you can make this ;
				- <img width="788" height="424" alt="image" src="https://github.com/user-attachments/assets/2e2d4734-cfb5-431d-ab25-883ba2d3e440" />

			- this shows you that g0/1 has been routed.
		- Now how to make an SVI routing on the switch;
			- switch virtual interface;
				- <img width="792" height="274" alt="image" src="https://github.com/user-attachments/assets/ec003328-0202-4f6e-89ac-2a8ca6d9c271" />

				- interface vlan10 -> this get you into vlan10
				- ip address address subnet -> assign ip address to that interface 
				- no shutdown as the SVI  => by default they are shutdown so you need to make them noshutdown.
				- <img width="771" height="282" alt="image" src="https://github.com/user-attachments/assets/3990eeac-5e3b-485e-b0e3-52a783eb1879" />

				- here we entered into an interface that doesn't exist -> then assign to it an address
				- when we write do show ip interface brief
					- we will see the vlan is on the switch but it's status are down-> down.
				- 3 rules to be taken when build an SVI;
					- vlan must be on the switch
					- vlan must have in access port if it was in the vlan that connected to the switch or has a trunk port at case the vlan isn't connected to the switch. like vlan 30 on the network topology that we took before.
					- vlan ->not shutdown 
					- svI -> not shutdown.
				- now after we created the svi on the vlans  hit do show ip route;
				-<img width="713" height="481" alt="image" src="https://github.com/user-attachments/assets/49e43697-4c7e-44b7-8d9b-e64343a035a2" />

			- after doing svi 
				- you can send traffic to the internet;
					-<img width="928" height="470" alt="image" src="https://github.com/user-attachments/assets/8f5d05c5-6f38-4866-8f00-5754f395b72f" />

				- or you can send traffic to any vlan ;
					- ![[Pasted image 20260428194633.png]]
- ---
- Questions;
	- Q1;<img width="966" height="463" alt="image" src="https://github.com/user-attachments/assets/7e60f3af-bdde-4c2b-b3e4-4efba4382fd7" />

	- answer ; b,c
		- b -> to configure the native on a subinterface
		- c -> configure native vlan on a physical interface so you don't need encapsulation.
	-  
	-  Q2;
		- <img width="962" height="499" alt="image" src="https://github.com/user-attachments/assets/400fd6f7-ea8f-4848-a0f1-f422751036ac" />

		- a,c -> as the the rules was![[Pasted image 20260428201638.png]]
		- so the svi mayby shutdown
	- Q3
		- <img width="940" height="170" alt="image" src="https://github.com/user-attachments/assets/6bdcb874-d216-4c36-beeb-5e97864e3ee1" />

		- a -> as it configure the switch interface as routed port
	- Q4;
		- <img width="531" height="196" alt="image" src="https://github.com/user-attachments/assets/40ebd0d9-b084-4e52-977a-a6bba1b833c7" />

		- answer; b
		

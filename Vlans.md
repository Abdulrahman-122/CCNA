# Vlans
  -Virtual local area network.
  - Lan -> a broadcast domain contain all devices
  - broadcast domain => group of devices that receives a broadcast frame(Mac ffff.ffff.ffff)
  - <img width="778" height="418" alt="image" src="https://github.com/user-attachments/assets/fb9314bd-e953-4956-b303-ef516f1b5edf" />
      from this image you have 4 LANs as the upper left Lan is achieved as if we sent the frame from pc1 to sw1 ->sw1 will flood the frame out of it to any device connected to it except that one that was sent to him the frame
        so this  is a local Area netword untill R1
      the same with Lan2,Lan3,Lan4 between two routes why -> as the first routes sends the routes from him to the second router .
    so this achieve a Lan .
    ----
    <img width="819" height="382" alt="image" src="https://github.com/user-attachments/assets/ca3e45c3-3731-4e3c-bccc-77919b1bb4a1" />

    from here you see ; we have 3 areas of Lans now if we sent the frame from any pc in Engineering department out of it to the switch
    the switch will flood it to all departments which is not good;
      - we want to prevent get access to the message by other departments
      - we need to put some firwalls in order to make some security stuff.
    --------
<img width="877" height="484" alt="image" src="https://github.com/user-attachments/assets/44914537-390d-4df8-8227-542532455acc" />
we need to achieve this =>send the traffic from pc1 in Eng department to sales pc2 across the switch+router.

-------
<img width="901" height="507" alt="image" src="https://github.com/user-attachments/assets/3503aea0-dd45-40bd-8ece-85556fd165f8" />
however we here ; message is flooded out of switch to all departs
however we just want to flood the message inside HR departments but this didn't worked
as switch just understand layer 2 mac address  but didn't understand layer 3,4 so it will flood it to all.

untill now -> all the pcs are in the same  broadcast domain (same mac add) as we see above
even if we divide it into subnets

---------------
<img width="962" height="520" alt="image" src="https://github.com/user-attachments/assets/922d7021-6590-43b0-809b-67ff5d48010d" />

here ; we edit the broadcast domain => we divide the departments into vlans 
each vlan is isolated than the others throw a mac address for each one.
as you see -> we just need to send the traffic from one depart to another without access the data using other departs.
note;
the switch doesn't perform an inter-vlan routing instead router need to access the data first before send it.

==========
note;
  - vlans can configured on a swithches
    - vlans => separate end hosts at layer2.
----------------     
<img width="904" height="469" alt="image" src="https://github.com/user-attachments/assets/13348cab-ac24-42d7-8bca-88b6e60a712d" />
let's make some vlans config;

  - to see the list of vlans;
    - vlan brief.
      - you will see; default vlan that collect all the devices of  one broadcast domain.
  - some old vlans  it's status is act/unsup (ignore it)+they can't be deleted.
  - now to config some vlans on your switch;
    - interface range g1/0-3          this open the range for you
    - switchport mode access       this allow for vlan on the swith
    - switchport access vlan10     give this vlan name=vlan10
    - interface range g2/0-2          open the range
    - switchport mode access          allow for  vlan
    - switchport access vlan20       give new name for this
  - ....... you can make any vlans like this
  - as you see switchport is carry multiple vlans  at the same time (trunk ports

    - do show vlan brief
      - this shows all the vlans you made.
      - now to change any vlan name
        - vlan 10       this get you into vlan 10
        - name Engineering         change the name from vlan10 to Engineering
---------------
   <img width="877" height="459" alt="image" src="https://github.com/user-attachments/assets/e4bf1749-d97a-4e1c-8869-27229057c5b9" />
       -now if ping the pc1 on sales depart -> it will send the traffic to all pcs connected to that vlan
some-questions;
<img width="882" height="462" alt="image" src="https://github.com/user-attachments/assets/8435c20e-07bd-4769-a743-1b443aae6642" />
there are ; 6 vlans
<img width="866" height="410" alt="image" src="https://github.com/user-attachments/assets/816663db-80c8-418f-b206-fc514708a3ce" />

<img width="937" height="471" alt="image" src="https://github.com/user-attachments/assets/b398ee6b-643a-4182-b81c-e42145fb41f2" />
there are 5 broadcast domains
<img width="872" height="307" alt="image" src="https://github.com/user-attachments/assets/59d02901-68d1-488b-9645-332cac084b39" />
the switch wii create the vlan
<img width="856" height="460" alt="image" src="https://github.com/user-attachments/assets/eb0475cb-2eb9-4052-806f-f92d16d3b242" />
broadcast message -> is to send a message to all the devices across the whole network
so here; switch,Router,second pc in HR
<img width="909" height="293" alt="image" src="https://github.com/user-attachments/assets/7bd6c65f-7f19-4add-a801-1b141ca89db0" />
8 -> default vlans,oldones(4 vlans from 1002;1005),3 newones

now; you need to solve this lab ; https://youtu.be/-tq7f3xtyLQ?si=lDnldkFqB4T7WYvl

------------

# to sum up
  - the purpose of vlan is to prevent access data through all the network just 2 ends


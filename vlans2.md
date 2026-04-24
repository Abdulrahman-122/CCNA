<img width="1765" height="885" alt="image" src="https://github.com/user-attachments/assets/adc8e585-68b4-4aa4-b524-f8fecb769e12" />

  -as you see Router act a inter vlan routing to make connection between vlan20,vlan10 

  - In big area network -> if you used separate interfaces for each Vlan on the switch -> this will  be wasted + router will not  get enough interfaces to work -> so we used trunk port to solve this issue (to carry multiple vlans over single interface)
  - like this ;
    - <img width="987" height="498" alt="image" src="https://github.com/user-attachments/assets/36664301-3198-48b9-b484-9c59d112fd0f" />
  - so when sending a frame from a vlan to another vlan
    - switch will tag the frames so that the second switch will know that that frame is coming from that specific vlan.
    - note;Trunk ports -> tagged ports
-----
types of Trunk protocols;
  - ISL(inter-switch link) ->old protocol -> you will not use it
  - IEEE 802.1Q->standard protocol -> used in Cisco equipments.

------
  - this is the Ethernet Frame structure;
    - <img width="820" height="433" alt="image" src="https://github.com/user-attachments/assets/f99a5e9d-6eba-4b8c-b4e3-e96dafd0a449" />
  -this is where tag protocol is found;
    -<img width="745" height="63" alt="image" src="https://github.com/user-attachments/assets/a4eecdf9-1b80-4961-b40e-5986791631a0" />
    - it's inserted between source,type
    - tag  is 4 bytes
    - tag contain;
      - Tag protocol identifier(TPID)
      - Tag control information(TCI)
        - contain 3 fields.
       
      - structure of 802.1Q protocol;
        - <img width="942" height="300" alt="image" src="https://github.com/user-attachments/assets/fd324f95-a8f1-474c-9374-ab5f8355d88a" />
        - it contains ->
          - TPID -> length of it is 16 bits(2bytes)
            - it's value 0x800 -> indicate that the tag is 802.1Q
          - TCI(tag control information)
            - contain ->
            -  PCP(periority code point)
                - 3bit length
                - used(COS)->class of service -> to perioritzes traffic in congested networks.
            -DEI (Drop Eligible indicator)
              -1bit
              - indicate whether frames can be  dropped or not if the   network has been congested or  not.
            -  VID(vlanID)
              -  12 bits length
              -  identify the vlan ->frame belongs to
              -  so it's range from 0;2^12 ->0-4096
                -  0,4095 is reserved
                 actual range from 1;4094 (this is 802.1Q also ISL has the same range)
                 -notes;
                      -range of vlan 1-4094 divided into
                       -Normal vlan(1-1005) supported
                       - Extended vlan(1006-4094) supported also
-----
now if we want to send a frame from vlan10(Engineering)to vlan10(engineering) into another floor 

  -switch2 will tag the frame in order to be distinguished then send it to it's  distination area.
  <img width="945" height="492" alt="image" src="https://github.com/user-attachments/assets/fe6e0533-263c-4327-9e75-06f3eec1d4bc" />

note; 
    -Native vlan->feature on 802.1Q protocol 
        native vlan->it's vlan1(on trunk port0
        so switch doesn't add any tagging to any frames on this native vlan 
        - once untagged frame is received on a switch -> switch will assume that this is a native vlan frame
        -you configured native vlan on the switch +must be matched on the switches 
        ex;
        here sw1,sw2 has matching in native vlan -> so they will detect the frame and route it to it's destination correctly;
        <img width="982" height="502" alt="image" src="https://github.com/user-attachments/assets/bd077e78-63be-46ac-900b-bb77f5e3be52" />
      ex; here as you didn't configure both switches correctly so they will not send the frame correctly as you see
      <img width="998" height="491" alt="image" src="https://github.com/user-attachments/assets/c7cdee03-102b-40d4-8f70-70c471d94814" />

-----
Trunk configuration;

  -This example we will apply on the config of trunk port;
  <img width="998" height="506" alt="image" src="https://github.com/user-attachments/assets/09c1f0f7-c249-43d1-93c0-80312f3224c8" />

  1.first define the interface+define the encapsulation type(802.1Q or ISL) once switch support 2 protocols if no no need to define the encapsulation
  but here it's support the both so we define which one
  + define the interface as trunk port mode .
 <img width="988" height="255" alt="image" src="https://github.com/user-attachments/assets/9fdc1b78-6605-4bf0-a4a6-0fd7e8555b09" />
2.<img width="589" height="486" alt="image" src="https://github.com/user-attachments/assets/db4d8a63-b1de-4c89-b958-36c297c8b53e" />
  - here we got the mode that we created 802.1Q + it's on
  - you have also  ranges of vlans ;1-1094 that are allowed
  - while the active vlans are 1(native vlan),10,30(these two are created)
  - then below;
    - 1 is the default vlan
    - 10,30 are created on the switch
    - 1002->1005 -> these are the default that came with the switch
  3.<img width="934" height="320" alt="image" src="https://github.com/user-attachments/assets/d8473c37-82f6-4546-9ffd-c258f6eafd8b" />
      - then here ; go into the interface to start add or do operation on the trunk port.
      - he want to choose specific operation to made over the vlan.
      - here he allowed vlan 10,30 on the trunk mode -> below you will see the allowed vlans on trunk are 10,30.
      - <img width="898" height="441" alt="image" src="https://github.com/user-attachments/assets/91993d31-aaa3-4106-af52-ee78b94f0fb6" />
          -then here he added vlan 20 to the trunk port.
          - but you will see 20 not in management domain as it's not created yet as vlan on the switch .
          - <img width="909" height="449" alt="image" src="https://github.com/user-attachments/assets/4a45d23f-beda-4d45-8d0e-088ce80f936a" />
              -while here we removed vlan 20 as its not vlan yet.

        -<img width="925" height="449" alt="image" src="https://github.com/user-attachments/assets/928f86ee-4903-4bed-832b-0ed62309788b" />
            -then here we allowed all the vlans on the system to be act as trunk ports.
        - then here we except from the trunk mode some of the  vlan numbers like;1-5,10
          - <img width="908" height="428" alt="image" src="https://github.com/user-attachments/assets/69199b2c-48b0-41fc-900d-e0171608b725" />
        -then here we removed all the vlans from trunk port
          <img width="907" height="446" alt="image" src="https://github.com/user-attachments/assets/12fc3bca-a136-4c5f-bf8f-6aec143d78d4" />

--- 
now let's do some  operations;
      - you need to move native vlan frm vlan1 to any other vlan for security purposes.
      like this example;
                                   <img width="887" height="434" alt="image" src="https://github.com/user-attachments/assets/1b026b0b-6d8b-44d0-be62-aa5230056a03" />

  - here you will see the vlans but if you want to see the vlans that on trunk port do show interfaces trunk.
  - <img width="985" height="360" alt="image" src="https://github.com/user-attachments/assets/6b7b5537-f120-4fff-97b8-0fc579f129dc" />


-now we got here;
  <img width="665" height="486" alt="image" src="https://github.com/user-attachments/assets/aad8214d-c67b-459b-ace7-778257f17b2f" />

  -he made interface
  then he made the encapsulation
  then switch to the trunk port
  then allow ports 10,20,30
  then change native vlan to 1001
  then do show interfaces  trunk
  
-----
Roas(router on a stick)
  - it's a way used to put just one interface between router,switch=>then divide that interfaces into sub interfaces like  the in  the image (after creating the vlan trunk,create vlans for the process of transformation )
  - <img width="967" height="495" alt="image" src="https://github.com/user-attachments/assets/8a8170dc-af7b-4033-8799-5c8b461433d4" />

  -now if we want to move on and create sub interfaces and create on one of them the trunk then assign an ip address for each one after determine the encapsulation on it  like this ;
<img width="957" height="237" alt="image" src="https://github.com/user-attachments/assets/1662767a-327b-44ff-ba1a-ce46148cf43b" />

then make sure the  ip interfaces;
<img width="988" height="395" alt="image" src="https://github.com/user-attachments/assets/808c37ef-315a-4e7d-9db7-1d480fd8198a" />

then ip routes;
<img width="842" height="493" alt="image" src="https://github.com/user-attachments/assets/d9eab26e-12da-44b0-8f24-86d30ae78782" />
then 
to sum up
  -Roas -> use single interface between router,switch 
  - switch configured as regular trunk
  - router configured as subinterfaces(configure vlan,ip address on each interface)
  - once the frame recieved to the router -> router will tag that frame with vlan tag .
  - <img width="978" height="491" alt="image" src="https://github.com/user-attachments/assets/b61cc2f0-67e4-4992-8d3e-8dee1d40b522" />


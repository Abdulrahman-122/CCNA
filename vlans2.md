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
  - explain this image ....
        
        
        

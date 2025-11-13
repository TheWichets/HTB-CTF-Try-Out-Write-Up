# **Silicon Data Sleuthing**
>In the dust and sand surrounding the vault, you unearth a rusty PCB... You try to read the etched print, it says Open..W...RT, a router! You hand it over to the hardware gurus and to their surprise the ROM Chip is intact! They manage to read the data off the tarnished silicon and they give you back a firmware image. It's now your job to examine the firmware and maybe recover some useful information that will be important for unlocking and bypassing some of the vault's countermeasures!

Từ nội dung của challenge, ta có thể biết được đây là một OpenWRT firmware image.
Sử dụng _binwalk -e_ trong terminal để giải nén file chal_router_dump.bin (yêu cầu cần tool **sasquatch** và **jefferson** được cài từ trước)

>What version of OpenWRT runs on the router

Vào **/squashfs-root/etc** mở file banner lên sẽ thấy phiên bản của OpenWRT
<img width="439" height="167" alt="image" src="https://github.com/user-attachments/assets/806ab9ec-7fa3-4124-a680-e2e9a3dbbade" />

>What is the Linux kernel version

Chạy _binwalk_ với file .bin ban đầu là nó sẽ nói cho mình phiên bản của Linux luôn. Ở đây là 5.15.134
<img width="1899" height="34" alt="image" src="https://github.com/user-attachments/assets/7647c6ae-e223-417a-a7b5-118c513c396f" />

>What's the hash of the root account's password, enter the whole line

Để tìm password hash thì phải vào phân vùng **overlay** định dạng JFFS2 vì đây là phân vùng chứa config của router này
Ở đấy hash password sẽ tìm được trong **/work/work/#32**
<img width="480" height="184" alt="image" src="https://github.com/user-attachments/assets/f5033f74-7070-4c61-aefc-377df107e4ba" />

>What is the PPPoE username
>
>What is the PPPoE password

2 Cái này ở trong **/work/work/#4** file **network**

<img width="459" height="115" alt="image" src="https://github.com/user-attachments/assets/8b27593c-56ab-4701-b21d-08f01d66bc06" />

>What is the WiFi SSID
>
>What is the WiFi Password

Cùng folder file **wireless** có thông tin này

<img width="428" height="181" alt="image" src="https://github.com/user-attachments/assets/b8830cff-a4c8-4b7d-b578-92ecd8e9561b" />

>What are the 3 WAN ports that redirect traffic from WAN -> LAN

Mình tìm thấy cái này ở **/work/work/#b**

<img width="303" height="457" alt="image" src="https://github.com/user-attachments/assets/268457bc-4230-4cbc-9191-8d0a5e99835a" />

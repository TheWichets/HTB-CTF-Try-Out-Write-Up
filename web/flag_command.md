# ** Flag Command **
> Embark on the "Dimensional Escape Quest" where you wake up in a mysterious forest maze that's not quite of this world. Navigate singing squirrels, mischievous nymphs, and grumpy wizards in a whimsical labyrinth that may lead to otherworldly surprises. Will you conquer the enchanted maze or find yourself lost in a different dimension of magical challenges? The journey unfolds in this mystical escape!

Chạy và truy cập Docker bằng trình duyệt và chơi thử trò chơi

<img width="2560" height="1600" alt="Image" src="https://github.com/user-attachments/assets/217f1147-90a6-47a7-902e-345bfcbf2de3" />

Gõ **start** để bắt đầu chơi
Sau khi chơi vài lần chọn ngẫu nhiên các đáp án thì chúng ta khả năng cao vẫn thua nên ta cần xem cách hoạt động của web để tìm ra các lựa chọn đúng

Bấm **F12** mở **Inspect**, vào tab **Source**. Ở đây ta thấy có 3 file js nhưng chỉ cần tập trung vào file **main.js**

<img width="2560" height="1600" alt="Image" src="https://github.com/user-attachments/assets/4a741183-d9e5-4668-a023-09fdd7f658e8" />

Mở file **main.js**, ta thấy ở hàm này có các câu lệnh điều kiện, để ý thấy ở đây có điều kiện **currentCommand == 'HEAD NORTH'** giống với các lựa chọn trong trò chơi. Khả năng cao là lựa chọn đúng sẽ là **HEAD NORTH -> FOLLOW MYSTERIOUS PATH ->  SETUP CAMP**

<img width="1185" height="1317" alt="Image" src="https://github.com/user-attachments/assets/3e62bbd2-1d26-4f78-9c2a-ef690b8ba95f" />

Đúng như ta dự đoán thì sau khi lựa chọn theo những gì được ghi trong file **main.js** thì ta đã tiến được tiếp trong trò chơi nhưng lại có tiếp 4 lựa chọn

<img width="2560" height="1600" alt="Image" src="https://github.com/user-attachments/assets/3d6d3bd8-071c-4161-a39e-7615d5815281" />

Và cả 4 lựa chọn này đều khiến ta thua game :v

Mở lại **Inspect**, vào tab **Network** sau khi đã refresh lại web để xem hoạt động của web

<img width="2560" height="1600" alt="Image" src="https://github.com/user-attachments/assets/0b8e0cf2-91e7-48be-be94-c19708770320" />

Ở đây ta để ý thấy mục **option** - đây là **api/option** được **main.js** gọi mỗi khi đưa chúng ta các lựa chọn

<img width="2560" height="1600" alt="Image" src="https://github.com/user-attachments/assets/f4b44cad-edf7-4615-b4b5-dcc2908a80ef" />

Ta thấy có 1 lựa chọn secret: **Blip-blop, in a pickle with a hiccup! Shmiggity-shmack**
Đây là lựa chọn cho câu cuối sau khi đã lựa chọn đúng 3 câu trên

<img width="2554" height="718" alt="Image" src="https://github.com/user-attachments/assets/7df32c2e-0817-4236-8c29-9c53efbfb28b" />

Flag: **HTB{D3v3l0p3r_t00l5_4r3_b35t_wh4t_y0u_Th1nk??!_cfe55f71e8e47c2a2529a899e503e9d6}**





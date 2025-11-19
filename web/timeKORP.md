# ** TimeKORP **
> Are you ready to unravel the mysteries and expose the truth hidden within KROP's digital domain? Join the challenge and prove your prowess in the world of cybersecurity. Remember, time is money, but in this case, the rewards may be far greater than you imagine.

Chạy và truy cập docker bằng **trình duyệt**

<img width="2559" height="1371" alt="Image" src="https://github.com/user-attachments/assets/e4d3c973-39a8-4ea3-8389-7abf52ae9c67" />

Tải file bài cho cề máy và giải nén

<img width="1099" height="364" alt="Image" src="https://github.com/user-attachments/assets/bab45630-a589-4592-abf0-8e5d2053eb37" />

Ở đây ta có 2 thư mục **challenge và config**, **file docker**, file bash, và flag (tất nhiên là fake flag để thử)
Vậy nên tại đây ta không quan tâm tới file flag và file build_docker.sh mà thử xem qua file docker

<img width="1338" height="1016" alt="Image" src="https://github.com/user-attachments/assets/caab6119-bda2-4171-a2bf-7add7541a6ed" />

Sau khi đọc xong file docker thì không có gì đặc sắc lắm ngoại trừ dòng **COPY flag /flag**
Chứng tỏ là flag được copy vào từ đường dẫn /flag (Cái này sẽ hữu ích về sau)

Ta không cần quan tâm đến folder **config** vì ở đây chứa các config của docker không ảnh hưởng đến bài (thực ra là đọc không hiểu gì :v)
Ta vào luôn folder **challenge**, đây là folder sẽ cung cấp cho ta manh mối giải bài này

<img width="1115" height="415" alt="Image" src="https://github.com/user-attachments/assets/b0daa74a-8273-493d-b2c2-c044b83325d8" />

Folder **challenge** khá nhiều thứ và mình khá lười xem hết
Vậy nên loại bớt những folder như **assets** (thường chứa ảnh, icon, link ...), **static** và **views** (2 folder thường chứa giao diện web)
2 file **index.php** và **router.php** cũng không có gì đáng lưu tâm nên ta sẽ vào luôn 2 folder còn lại

Folder **controllers** chứa file **TimeController.php**

<img width="840" height="315" alt="Image" src="https://github.com/user-attachments/assets/ba1157a1-464f-4855-827f-3d71db1cee6e" />

Ta thấy file này định dạng giờ cho trang web nhưng có vấn đề khá nghiêm trọng

<img width="753" height="42" alt="Image" src="https://github.com/user-attachments/assets/5bb597ca-a4f0-4f06-a851-bdd12a7c65a2" />

Ở đây ta thấy dòng này đang định nghĩa format giờ nhưng lại dùng method **? $_GET['format']**, tức là sẽ nhận query từ client(người dùng) ở browser
Ta hãy thử kiểm chứng điều này

<img width="2560" height="1600" alt="Image" src="https://github.com/user-attachments/assets/73fe6f11-ab28-4a1e-8815-343458c6211c" />

Ở đây ta thấy rằng ở đường dẫn được ghi là **?format=%H:%M:%S**, chính là thứ đã nói ở trên 
Nếu giả thuyết là đúng thì ra có thể thay đổi format để trình duyệt in ra cái ta muốn
Nhập thử **?format=hello world** và bấm enter xem chuyện gì xảy ra

<img width="2560" height="1600" alt="Image" src="https://github.com/user-attachments/assets/56d71d31-5028-4506-bc1e-32c0dbf6adc5" />

Ta thấy rằng trên màn hình đã hiện hello world
Ta có thể nghĩ đến việc tiêm câu lệnh vào đường dẫn để xem flag
Nhưng ở đây ta thấy rằng "hello world" là 1 string nên khi nhập vào bất kì cái gì vào sau **?format=** thì sẽ in ra cái đó
Nên không thể tiêm lệnh vào đây được nhưng đây là hint của bài

Ta xem tiếp folder **models**. Folder này chứa file **TimeModel.php**

<img width="738" height="466" alt="Image" src="https://github.com/user-attachments/assets/a2821f6d-c5f4-4817-b89d-4a3a10034206" />

Vấn đề nằm ở hàm dưới này

<img width="621" height="136" alt="Image" src="https://github.com/user-attachments/assets/d683f5bb-d415-48fc-8278-36ee462e60b7" />

Ta thấy tham số truyền vào là **$format** chính là cái mà ta có ở file **TimeController.php**

Ở đây tham só được truyền vào câu lệnh **$this->command = "date '+" . $format . "' 2>&1";**
Điều này tức là sẽ tạo nên 1 biến **command** được **exec** ở ngay hàm bên dưới
Ý tưởng là tạo payload theo cấu trúc của **command** để khi execute thì chạy được câu lệnh trên terminal

Ta để ý **date** ở đây tức là format giờ có dạng **%H:%M:%S**, **$format** chính là được xử lý ở trên nên ta có thể thay bằng câu lệnh ta cần
Ở đây biến **command** được tạo bằng cách ghép các chuỗi với nhau
Sau **%H:%M:%S** có dấu **'** nên ta thêm 1 dấu **'** để đóng sau đó thêm dấu **;** để ngăn cách
**" . $format . "** ta có thể thay bằng câu lệnh ta cần ví dụ **ls**
Còn lại 1 dấu **'** thì thêm 1 cái nữa để đóng

Vậy payload mẫu sẽ là: **?format=%H:%M:%S';ls'**
Ta thử luôn với trình duyệt

<img width="2560" height="1600" alt="Image" src="https://github.com/user-attachments/assets/dd7239df-16f6-4d86-bf12-303e5dca89e9" />

Yeah có vẻ là ta đã thành công !!!
Vậy là chỉ cần tìm flag nữa là xong

Nếu bạn còn nhớ ở trên mình đã nói là flag được copy từ **/flag**. Đây là mấu chốt để tìm ra flag
Mình đã thử dùng **cd** để tìm flag nhưng không được và mất nhiều thời gian mãi không tìm được flag
Tình cờ đọc lại file **docker** thì có dòng **COPY flag /flag**

Vậy là chỉ cần đổi **ls** ở payload trên thành **cat /flag** là sẽ có được flag

<img width="2560" height="1600" alt="Image" src="https://github.com/user-attachments/assets/1556a553-ccbb-4f36-a0cb-a29bd74cdd34" />
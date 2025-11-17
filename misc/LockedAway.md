Mở đầu ta sẽ tải file về và giải nén như bình thường

Sau khi kiểm tra các file ở đầu thì thấy được không có gì quá quan trọng

Vào folder challenge sẽ thấy 1 file tên là flag.txt và rõ ràng là 1 fake flag

Tiếp theo ta check file main.py thì thấy có thể biết được nhiệm vụ là chạy hàm open\_chest

Nhưng khó ở chỗ nó lại ban 1 loạt các từ vào trong blacklist nên k thể gọi trực tiếp open\_chest ra

Nhưng ta lại có 1 trick lỏ là dung hàm globals

Hàm này có thể cho phép ta gọi hàm open\_chest ra vì cơ chế của nó có thể cho gọi tên hàm dưới dạng chuỗi

Ta nhập hàm sau sau khi chạy chương trình

globals().get(chr(111)+chr(112)+chr(101)+chr(110)+chr(95)+chr(99)+chr(104)+chr(101)+chr(115)+chr(116))()  

Và thành công nhân được flag!


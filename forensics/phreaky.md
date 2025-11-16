# Phreaky
>In the shadowed realm where the Phreaks hold sway,
A mole lurks within, leading them astray.
Sending keys to the Talents, so sly and so slick,
A network packet capture must reveal the trick.
Through data and bytes, the sleuth seeks the sign,
Decrypting messages, crossing the line.
The traitor unveiled, with nowhere to hide,
Betrayal confirmed, they'd no longer abide.

Giải nén scenario files ra mình được một file .pcap
Mở trong wireshark, điều đầu tiên mình nhìn là nhìn tới Protocol Hierarchy của file.
<img width="1165" height="349" alt="image" src="https://github.com/user-attachments/assets/2e310729-2603-4b73-b5f3-2d2660b64116" />

Ở đây thấy dùng 2 protocol chính: HTTP và SMTP

-HTTP: thấy HTTP traffic là dùng để update ubuntu -> Không cần để ý tới trong challenge này
<img width="1918" height="263" alt="image" src="https://github.com/user-attachments/assets/2d093b5b-f861-4d91-ac37-7883c97be118" />

-SMTP: ở đây thấy SMTP traffic là các email đính kèm các file zip được gửi nhiều lần
Mình lọc theo filter smtp.data.fragment rồi follow TCP stream của từng cái để lấy dữ liệu và mật khẩu của các file zip

<img width="1919" height="271" alt="image" src="https://github.com/user-attachments/assets/6d64b597-1109-422d-ad44-44e197bcac8e" />

Do mình lười viết script lên mình cop hết dữ liệu và mật khẩu vào rồi chạy một vòng lặp đơn giản để giải nén file :)))))

~~~
data=("UEsDBBQACQAIAGZ3Zlgub1pG0gAAAN0AAA..................",.........) // phần data cop vào đây

pass=("j2SRRDraIvUZ",...............) // phần pass cop vào đây

name=("5dc7a18136ec2d085dd747e7869859b00418d2073fc2c6946c1cff84ab56b6ef.zip",...........) // phần tên zip cop vào đây

for i in {0..9}; do
	echo "${data[$i]}" |base64 -d > "${name[$i]}"
	unzip -P "${pass[$i]}" "${name[$i]}"
done
~~~

Xong ta sẽ được như sau:

<img width="603" height="330" alt="image" src="https://github.com/user-attachments/assets/2971ebad-69f0-4244-80ef-99aeb3f5d7fe" />

Dùng cat để kết hợp các part lại thành pdf hoàn chỉnh
~~~
cat $(ls -1 phreaks_plan.pdf.part?) $(ls -1 phreaks_plan.pdf.part1?) > phreaks_plan.pdf
~~~

Cuối cùng vào file pdf hoàn thiện ta có được flag của bài này

<img width="238" height="205" alt="image" src="https://github.com/user-attachments/assets/56bc467f-e23b-48a6-9321-12ac6cc0ad95" />

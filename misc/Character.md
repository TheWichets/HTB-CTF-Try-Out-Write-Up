Mở đầu bài thì ta chỉ cần dùng nc với ip và port mà bài đã cấp sẵn
Khởi đầu ta sẽ có 1 giao diện cho phép ta nhập vào 1 số bất kỳ, khi ta nhập nó sẽ cung cấp cho ta 1 giá trị trong flag ta cần tìm tương ứng với số ta nhập.
Sau khi thử nhập khoảng 10 ký tự đầu thì có thể thấy được đây là 1 flag có tên khá là dài nên ta sẽ không nhập thủ công mà sẽ dùng 1 script để nó tự động nhập và in ra flag.
Dưới đây là script để nhập và in:
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
#!/bin/bash

ip="94.237.52.164"
port="39104"

head="0"
tail="103"

Flag=""

for i in $(seq $head $tail); do
a=$(echo "$i" | nc -w 1 $ip $port | awk '/Character at Index/ { print $NF }')
Flag+=$a
if [[ "$a" == *"}"* ]]; then
break
fi
done

echo "$Flag"
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
sau khi chạy script ta nhận được flag cần tìm

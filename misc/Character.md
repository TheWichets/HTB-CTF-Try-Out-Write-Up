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

### Bổ sung script python cho bài này

```
#!/usr/bin/python3

from pwn import *

context.log_level = 'debug'

flag = ""

r = remote('IP', PORT) // Thay bằng IP và PORT được cấp

for i in range(0, 150):
        r.recvuntil(b'Which character (index) of the flag do you want? Enter an index:' )
        r.sendline(str(i).encode())
        line = r.recvline().decode().strip()
        print(line)

        if ":" in line:
                char = line.split(":", 1)[1].strip() // Lấy chuỗi sau dấu ":"

                if char != "":
                        flag += char
        if "}" in flag:
                break

print(flag)

```


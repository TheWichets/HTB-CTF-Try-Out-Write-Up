# ** Stop Drop and Roll **
> The Fray: The Video Game is one of the greatest hits of the last... well, we don't remember quite how long. Our "computers" these days can't run much more than that, and it has a tendency to get repetitive...

Chạy và truy cập Docker bằng **terminal**

<img width="932" height="800" alt="Image" src="https://github.com/user-attachments/assets/1f81230f-c907-4ff1-b364-46ee6b23a851" />

Ở đây ta phải chơi 1 trò chơi
Trò chơi này sẽ có 3 tình huống là: **GORGE, PHREAK or FIRE** và 3 câu trả lời là: **STOP, DROP, ROLL**

Nếu là **GORGE** thì phải **STOP**
Nếu là **PHREAK** thì phải **DROP**
Nếu là **FIRE** thì phải **ROLL**

Và để bắt đầu trò chơi ta sẽ trả lời **Y**

Thay vì nhập tay câu trả lời thì ta có thể viết 1 đoạn script để tự động chạy

Mình dùng thư viện **pwn** của **Python**. Có thể tải xuống bằng bằng cách: **sudo apt install python3-pwntools**

### Dưới đây là đoạn script để giải bài này
```
!/usr/bin/python3

from pwn import *

context.log_level = 'debug' // Chế độ in ra console các thông báo tiện cho việc debug

r = remote('IP', PORT) // Thay bằng IP và PORT của bạn

// Đọc và gửi 'y' để bắt đầu chơi
r.recvuntil(b'Are you ready? (y/n) ')
r.sendline(b'y')

def action(scenario):
        if scenario == b'GORGE':
                return b'STOP'
        if scenario == b'PHREAK':
                return b'DROP'
        if scenario == b'FIRE':
                return b'ROLL'

while True:
        scenarios = r.recvline_contains(('GORGE','PHREAK','FIRE'))
        log.debug(f"scenarios: {scenarios}")

        r.recvuntil(b'What do you do? ')

        items = scenarios.split(b', ')
        instructions = map(action, items)

        response = b'-'.join(instructions)

        r.sendline(response)
 ```
 ### Cách dùng: python3 {filename}.py

 Sau khi code chạy xong ta sẽ có flag



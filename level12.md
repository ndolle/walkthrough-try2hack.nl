#### Level 12

This solution is for GNU/Linux.

Download this Python decompiler and place it on your desktop https://github.com/wibiti/uncompyle2

Open a terminal and cd into the folder and run:
`sudo python setup.py install`

Then run the binary on the .pyc file: `uncompyle2 level12.pyc`

The result is this:
```python
# 2011.11.06 20:27:44 CET
from md5 import new

print "Enter username:"
username = raw_input()
print "Enter password:"
password = raw_input()

try:
    x  = chr((int(password[0:3])/3)-100)
    x += chr(((int(password[0:3])/12)+3)*2)
    x += chr(int(password[0:3])-700+173)
    x += chr(((int(password[0:3])-148)/4)-21)
    x += chr(((int(password[0:3])-327)/3)-10)
    x += chr(int(password[0:3])-534)
    x += chr(((int(password[0:3])+52)/70)*10)
    x += chr((int(password[0:3])**2)-(640*int(password[0:3]))-5083)
    x += chr(int(password[0:3])*5-3126)
except ValueError: pass

try:
    if new(username).hexdigest() == '3e3a378c63aa1'+x[7:8]+'55e3e9'+x[4:5]+'e9d2bdcd6a1' and password[3:12] == x:
        print "Well done. Enter the valid username and password on the form online."
    else:
        print "Wrong username and/or password"
except NameError: 
    print "Wrong username and/or password"
+++ okay decompyling level12.pyc 
# decompiled 1 files: 1 okay, 0 failed, 0 verify failed
```

What the code does is that you actually create your own password based on what you start to type in.
There are many valid passwords, but they need to comply with the algorithm.

This Javascript gets all the passwords. You can run it from the Javascript console in your web browser.

```Javascript
var i = 0;
while(i <= 999) {
    document.write(i);
    document.write(
    String.fromCharCode((i/3)-100) +
    String.fromCharCode(((i/12)+3)*2) +
    String.fromCharCode(i-700+173) +
    String.fromCharCode(((i-148)/4)-21) +
    String.fromCharCode(((i-327)/3)-10) +
    String.fromCharCode(i-534) +
    String.fromCharCode(((i+52)/70)*10) +
    String.fromCharCode(Math.pow(i,2)-(640*i)-5083) +
    String.fromCharCode(i*5-3126));
    document.write("<br>\n");
    i++;
}
```

The first three digits of the password creates the rest of the password, which basically means that you create your own password.
You will see a whole bunch of valid passwords, but it's just one password that makes any sense, which is "648tryharder".

Now for the username, which is based on the password:
```Javascript
var pw = "tryharder";
document.write("3e3a378c63aa1"+pw.substring(7,8)+"55e3e9"+pw.substring(4,5)+"e9d2bdcd6a1");
```

Let's try Google on that hash...
First hit gave me the answer: 3e3a378c63aa1e55e3e9ae9d2bdcd6a1 => lamer

Success!

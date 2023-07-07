# Nikto and Burp-Suite


# Scan a Web Server

Scan the root directory of the web server and identify any significant vulnerabilities.

![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/6f04d67f-1e39-49ec-8c8e-d953fc6b8c0a)


![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/108b3145-d7e5-463d-8b32-27bf705202c8)



ni![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/b9f6d41a-8306-46d5-90d2-9a9f463c7765)


![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/19b1fe52-8f14-4529-9967-98e9cd56ce7f)

firefox /root/Downloads/dvwa.htm
![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/16fd0b67-6f21-43db-b17a-bd3eae4f7ba3)

# Configure an Interception Proxy

Configure the browser to use Burpsuite as an interception proxy.

![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/8a5d1490-0019-45f4-a5ad-2e825222b820)


![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/15f0fe69-3dd9-41d9-8b2b-e3237b20bd14)

![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/0599c22b-8825-4883-b713-6bcc16205f8b)


# Inspect Session and Header Data

An interception proxy like Burpsuite can be used to monitor and record web sessions. You can inspect (and modify) the data that the server and browser exchange as headers, cookies, and form field submissions.

![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/cd6a2551-3ffb-4894-9f10-c9d7d80bdd19)

![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/6cf60464-5f6d-4de5-b33b-186cdd2cc18d)
![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/862573f0-a72e-45d6-a8c6-1f2781ccad9a)

![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/bf46bfbe-2583-4dda-b0e9-d8892180c6b6)


You can also see the information you submitted via the browser.


Credentials and session information must be protected by encryption when they are transmitted over the network. The server should be configured with HTTPS and insist on a secure connection for the login page.
![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/f737ebf1-378d-4d28-aaed-02df5d6151e0)


# Test Command Injection

Command injection means passing shell commands to the underlying OS via an unsecure form or API. Test a form for command execution vulnerabilities.

![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/930055f5-1c54-4a63-8919-d7941fbf652c)


The developer of this web app has decided to allow users to access a command in the native OS. Has the developer limited users to the ping command only though?

Submit each of the following command sequences and note which work:

ls

10.1.0.1 && ls

1 && ps -e

10.1.0.1 && ps -e

10.1.0.1 && netstat -tlnp

10.1.0.1 && cat /etc/passwd

10.1.0.1 && cat /etc/shadow

![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/78b63cb8-676e-4258-9433-cc28877719ad)


![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/a355ecb2-31f7-44f7-b572-ee83703928f7)


![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/b321d1ac-85cd-4d9e-8c9b-a3034f67d818)

You should be able to deduce that the developer is checking for the presence of a well-formed IP address but has not prevented additional command strings being appended.


Note from the output of the netstat command and the inability to read "/etc/shadow" that you are not root but we can confirm with this final sequence of commands.

10.1.0.1 && whoami

10.1.0.1 && getent passwd 0

10.1.0.1 && getent group root

![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/1fcd003f-795e-421f-abcd-b994fd24acc9)


![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/9fc76fc6-7a53-4743-b63e-3122fcc31e79)


# Submit Fuzzed Input

![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/96503022-0ea3-4d31-b277-95238fe501a6)


![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/ad10f6ab-2234-4265-9df0-59d147386f9f)

![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/2c919474-cc2d-470f-a4a1-08b8bd5ba3ca)

Click the Payloads tab. Click the Load button then browse to select /usr/share/wordlists/wfuzz/injections/SQL.txt

![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/e79971ae-746e-4d6c-a5ff-63f329fffccc)

Click the Start Attack button. Click OK to confirm the prompt.

![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/dd909bed-f986-463b-b5d6-3dbd7a8b8356)

Sort the output by the Length column and look for a response larger than 4868 bytes.

You should find some using the OR keyword have returned a number of rows. As with the command injection, this response tells us that the SQL statement being executed by the web app code can be modified by what we enter into the input box.

![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/529cb93b-d522-4358-a638-8d71ec3bb231)

![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/aab5c1c7-6265-433f-b6b7-cad00946e671)

![image](https://github.com/itzyezz/Burp-Suite/assets/105263523/0e436e02-bc36-4acc-b9a9-97a2c3b3d482)

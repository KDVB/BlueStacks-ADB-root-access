# BlueStacks ADB Vulnerability (Bluestacks root access with adb)
### Disclaimer
For informational purposes only. The author does not call for further actions. Created to warn users who use this product

### Background
ADB (Android Debug Brigde) - is a versatile command-line tool that lets you communicate with a device. The `adb` command facilitates a variety of device actions, such as installing and debugging apps. `adb` provides access to a Unix shell that you can use to run a variety of commands on a device.

### Research Walkthrough
For default, in Bluestacks, ADB port is open, but we can't to use shell command (output "error: closed")
![image](https://user-images.githubusercontent.com/34673122/228203203-adce4994-de46-4e50-9125-30112f61f85d.png)
Searching for information in the emulator files found the following file ".adbcmd" in Root.vnhd image. Path to file "dataFS\\downloads". In this file we can see adb commands that we can run without connection to shell
![image](https://user-images.githubusercontent.com/34673122/228203309-6aadaea7-16f3-4153-9199-1cad47d2b9e4.png)
For example, "getprop" command, that gives us information about android propetries
![image](https://user-images.githubusercontent.com/34673122/228203402-61ba611e-a2dc-407a-a3f0-c4a710abca84.png)
As we can see, interaction with android shell is working. So, I think "if I can interact with unix shell, maybe tryed to use pipe operators" and pwn i can interact with file system, but with shell-user privilage.
![image](https://user-images.githubusercontent.com/34673122/228203484-8357e1f8-bf73-463d-a9de-159fa1d07d7a.png)
![image](https://user-images.githubusercontent.com/34673122/228203542-9552ce13-d9a3-4b0d-b3b9-7abf7cfd2ea8.png)
As a result i continue my search to find su command to get root access. SU file is in "/boot/android/android/system/xbin/bstk/su". I tryed pipe operator to get root access, but get error and shell didn't open( 
![image](https://user-images.githubusercontent.com/34673122/228203692-3ab74b42-de43-4096-9826-72640991bab4.png)
After that i tryed list terminator ";" and it works. I get root shell
![image](https://user-images.githubusercontent.com/34673122/228203780-fd5c35f1-64f9-4130-9803-e054b5a8d4dc.png)

### Result
Bluestacks have this vulnerability and people involved in its development know about it and are engaged in its elimination.

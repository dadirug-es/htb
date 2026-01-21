# Introduction to Windows Command Line

1. The flag will print in the banner upon successful login on the host via SSH.
```sh
$ ssh user0@10.129.204.9 -p"Start!"
D0wn_the_rabbit_H0!3
```
2. Access the host as user1 and read the contents of the file "flag.txt" located in the users Desktop.
```sh
$ ssh user1@10.129.204.9 -p"D0wn_the_rabbit_H0!3"
> dir && cd Desktop && dir && type flag.txt
Nice and Easy!
```
3. If you search and find the name of this host, you will find the flag for user2
```sh
$ ssh user2@10.129.204.9 -p"D0wn_the_rabbit_H0!3"
> ipconfig /all
Windows IP Configuration
  Host Name............: ACADEMY-ICL11
```
4. How many hidden files exist on user3's Desktop?
```sh
$ ssh user3@10.129.204.9 -p"ACADEMY-ICL11"
> dir Desktop /A:H
...
07/18/2022  06:53 AM                 0 file-1.txt
...
07/18/2022  07:30 AM                 0 file19.txt
07/18/2022  07:30 AM                 0 file2.txt
...
07/18/2022  07:30 AM                 0 file99.txt
06/29/2022  01:41 PM             2,354 Microsoft Edge.lnk
             101 File(s)          2,636 bytes
```
5. User4 has a lot of files and folders in their Documents folder. The flag can be found within one of them.
```sh
```
6. How many users exist on this host? (Excluding the DefaultAccount and WDAGUtility)
```sh
```
7. For this level, you need to find the Registered Owner of the host. The Owner name is the flag.
```sh
```
8. For this level, you must successfully authenticate to the Domain Controller host at 172.16.5.155 via SSH after first authenticating to the target host. This host seems to have several PowerShell modules loaded, and this user's flag is hidden in one of them.
```sh
```
9. This flag is the GivenName of a domain user with the Surname "Flag".
```sh
```
10. Use the tasklist command to print running processes and then sort them in reverse order by name. The name of the process that begins with "vm" is the flag for this user.
```sh
```
11. What user account on the Domain Controller has many Event ID (4625) logon failures generated in rapid succession, which is indicative of a password brute forcing attack? The flag is the name of the user account.
```sh
```

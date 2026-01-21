# Introduction to Windows Command Line

1. The flag will print in the banner upon successful login on the host via SSH.
```sh
$ sshpass -p"Start!" ssh user0@10.129.204.9
D0wn_the_rabbit_H0!3
```
2. Access the host as user1 and read the contents of the file "flag.txt" located in the users Desktop.
```sh
$ sshpass -p"D0wn_the_rabbit_H0!3" ssh user1@10.129.204.9
> dir && cd Desktop && dir && type flag.txt
Nice and Easy!
```
3. If you search and find the name of this host, you will find the flag for user2
```sh
$ sshpass -p"D0wn_the_rabbit_H0!3" ssh user2@10.129.204.9
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
$ sshpass -p"101" ssh user4@10.129.204.9
> findstr /S "." flag.txt
Documents\3\4\flag.txt: Digging in The nest
```
6. How many users exist on this host? (Excluding the DefaultAccount and WDAGUtility)
```sh
$ sshpass -p"Digging in The nest" ssh user5@10.129.204.9
> powershell
PS> Get-LocalUser
Name               Enabled Description
----               ------- -----------
Administrator      True    Built-in account for administering the computer/d...
DefaultAccount     False   A user account managed by the system.
Guest              False   Built-in account for guest access to the computer... 
htb-student        True
user0              True
user1              True
user100            True
user2              True
user3              True
user4              True
user5              True
user66             False
user77             False
user88             False
user99             False
WDAGUtilityAccount False   A user account managed and used by the system for... 
```
7. For this level, you need to find the Registered Owner of the host. The Owner name is the flag.
```sh
$ sshpass -p"14" ssh user6@10.129.204.9
> systeminfo
..
Registered Owner:          htb-student
..
```
8. For this level, you must successfully authenticate to the Domain Controller host at 172.16.5.155 via SSH after first authenticating to the target host. This host seems to have several PowerShell modules loaded, and this user's flag is hidden in one of them.
```sh
$ sshpass -p"htb-student" ssh user7@10.129.204.9 ssh user7@172.16.5.155
> powershell
PS> Get-Module | Format-Table Name 

Name
----
Flag-Finder
Microsoft.PowerShell.Utility 
PSReadline
PS> Import-Module Flag-Finder
PS> Get-Flag
The Flag you are looking for is {Modules_make_pwsh_run!}
```
9. This flag is the GivenName of a domain user with the Surname "Flag".
```sh
$ sshpass -p"Modules_make_pwsh_run!" ssh user8@10.129.204.9
PS> Get-ADUser | Select-Object GivenName,Surname

cmdlet Get-ADUser at command pipeline position 1
Supply values for the following parameters:
(Type !? for Help.)
Filter: Surname -like "flag" 

GivenName Surname
--------- -------
Rick      Flag
```
10. Use the tasklist command to print running processes and then sort them in reverse order by name. The name of the process that begins with "vm" is the flag for this user.
```sh
$ sshpass -p"rick" ssh user9@10.129.204.9
> tasklist|sort /R
WmiPrvSE.exe                  4324 Services                   0     21,332 K
winlogon.exe                   664 Console                    1     16,420 K    
wininit.exe                    592 Services                   0      7,032 K    
vmtoolsd.exe                  3136 Services                   0     22,052 K    

```
11. What user account on the Domain Controller has many Event ID (4625) logon failures generated in rapid succession, which is indicative of a password brute forcing attack? The flag is the name of the user account.
```sh
$ sshpass -p"vmtoolsd.exe" ssh user10@10.129.204.9 ssh user10@172.16.5.155
PS> Get-WinEvent -FilterHashTable @{LogName='Security'; ID=4625} |
  Group-Object -Property @{Expression = {$_.Properties[5].Value}} |
  Sort-Object Count -Descending |
  Select-Object -First 1
```

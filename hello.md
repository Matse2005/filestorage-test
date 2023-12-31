# Basics

var1 = 'Variable' // Set a variable
echo 'Text" // Print text in terminal
echo var1 // Print var1 (Variable) in terminal

touch text.txt // Create file
mkdir test // Create folder
rm -rf test // Remove folder

cp /root/file /var/file // Copy folder or file from '/root/file' to '/var/file'
mv /root/file /var/file // Move folder or file from '/root/file' to '/var/file'
mv /root/file /var/folder // Move folder or file and rename from '/root/file' to '/var/folder'
nano NewFile.txt // Edit and create file if not exist
ls // List items in folder
ls -l // List items in folder and exta info
ls -la // List all items in folder also hidden folders and files and exta info

## Cheatsheet

| Command                             | Usage                                                                                            |
| ----------------------------------- | ------------------------------------------------------------------------------------------------ |
| touch [FILE PATH]                   | Maakt een nieuw bestand aan                                                                      |
| cd [PATH]                           | Verandert de huidige working directory                                                           |
| mkdir [DIRECTORY PATH]              | Maakt een nieuwe directory aan                                                                   |
| cat [FILE PATH]                     | Toont de inhoud van een bestand                                                                  |
| rm [PATH]                           | Verwijdert een bestand of map (met opties -rf)                                                   |
| pwd                                 | Toont de huidige working directory                                                               |
| ls [PATH]                           | Toont de inhoud van een map (of de huidige working directory als geen argument meegegeven wordt. |
| cp [SOURCE PATH] [DESTINATION PATH] | Een bestand of map kopiëren naar een andere locatie                                              |
| mv [SOURCE PATH] [DESTINATION PATH] | Een bestand of map verplaatsen naar een andere locatie                                           |
| nano [FILE PATH]                    | Edit and create file if not exist                                                                |
| ls                                  | List item in folder                                                                              |
| ls -l                               | List all items in folder and exta info                                                           |
| ls -la                              | List all items in folder also hidden folders and files and exta info                             |

# Apt

apt install [PACKAGE] // Install package
apt upgrade // Upgrade all
apt remove [PACKAGE] // Remove package

# Permissions

- User (owner) // Part 1
- Group // Part 2
- Others // Part 3
- R -> Read
- W -> Write
- X -> Execute

**Order**
RWXRWXRWX

**Examples**  
No one:
(---------)

User Can Do Everything The Rest Nothing
RWX------

User Can Do Everything rest Read and Execute:
RWXR-XR-X

# Explained

```sh
$ ls -l

drwxr-xr-x. 4 root root    68 Jun 13 20:25 tuned
-rw-r--r--. 1 root root  4017 Feb 24  2022 vimrc
```

In this example, you see two different listings. The first field of the ls -l output is a group of metadata that includes the permissions on each file. Here are the components of the vimrc listing:

- File type: -
- Permission settings: rw-r--r--
- Extended attributes: dot (.)
- User owner: root
- Group owner: root

# Calculate

- r (read) = 4
- w (write) = 2
- x (execute) = 1

**Examples**
Owner: rwx = 4+2+1 = 7
Group: r-- = 4+0+0 = 4
Others: r-- = 4+0+0 = 4

No one:
(---------) -> 000

User Can Do Everything The Rest Nothing
RWX------ -> (4 + 2 + 1)00 = 700

User Can Do Everything rest Read and Execute:
RWXR-XR-X -> (4 + 2 + 1)(4 + 1)(4 + 1) = 755

## Modify

You can modify file and directory permissions with the chmod command, which stands for "change mode." To change file permissions in numeric mode, you enter chmod and the octal value you desire, such as 744, alongside the file name. To change file permissions in symbolic mode, you enter a user class and the permissions you want to grant them next to the file name. For example:

```sh
$ chmod ug+rwx example.txt -> User and group
$ chmod o+r example2.txt -> Other
$ chmod a+rx example3.txt -> All
$ chmod 744 example4.txt
```

This grants read, write, and execute for the user and group, and only read for others. In symbolic mode, chmod u represents permissions for the user owner, chmod g represents other users in the file's group, chmod o represents other users not in the file's group. For all users, use chmod a.

Maybe you want to change the user owner itself. You can do that with the chown command. Similarly, the chgrp command can be used to change the group ownership of a file.

# Grep - To Do

grep <SEARCH_STRING> <FILE>

```sh
$ grep student /etc/passwd
```

Show all the lines in the file /etc/ssh/ssh_config that end in 'no'

```sh
$ cat /etc/ssh/ssh_config | grep "no$"
```

Show all the lines in the file /etc/passwd that start with 'root

```sh
$ cat /etc/passwd | grep "^root"
```

From the file /etc/resolv.conf, show onlythe lines that are not commented out Lines that are commented out canbe identified by the '#' with whichthey start

```sh
$ cat /etc/resolv.conf | grep -v "^#"
```

(-v will invert the result so show all the results that not start with #)

You can also use grep on command outputs

```sh
$ ls -l /etc | grep group
```

And combine multiple grep results

```sh
cat /usr/share/dict/american-english | grep '^f' | grep 's$'
```

Write a command that lists all files in /etc that are readable, writableand executable by the owner (user)

```sh
$ ls -l | grep '^-'
```

# Cut

cut -d <WHERE TO SPLIT (String)> -f <WHAT TO KEEP (Number)> [FILENAME]

```sh
$ cut -d "=" -f 2 /etc/os-release
```

# Tr

cat /etc/passwd | tr '<WHAT TO REPLACE>' '<WHAT TO REPLACE IT WITH>'

```sh
$ cat /etc/passwd | tr ':' ','
```

In the file /usr/share/dict/american-english, replace all the vowels ineach word by '\*'

```sh
$ cat /usr/share/dict/american-english | tr 'aeuio' '*'
```

From the directory /var/log, show us all the files, and return only thepermissions, file size and file name.

```sh
$ ls /var/log -la | grep '^-' | tr -s " " | cut -d " " -f 1,5,9
```

# Tail

Laatste 10 van ls output

```sh
$ ls -l | tail
```

Laatste N van ls output

```sh
$ ls -l | tail -n <N>
```

# Head

Eerste 10 van ls output

```sh
$ ls -la | head
```

Eerste N van ls output

````sh
$ ls -la | head -n <N>

# Processes

Show all the processes from the current user

```sh
$ ps
````

Options:

```sh
$ ps a -> All processes from all users
$ ps u -> All the info over the processes like the user who started it, cpu usage and memory usage
$ ps x -> All the background processes, not binded by a terminal by example in NetworkManager
```

Can be used together

```sh
$ ps au
$ ps ux
$ ps ax
$ ps aux
```

Kill a process

```sh
$ kill [PID] -> Pid => Process id
```

Search for calculator process

```sh
$ ps aux | grep calculator
```

**Exercises**

Wat is het PID van de je NetworkManager?

```sh
$ ps a | grep NetworkManager -> 3348
```

Tel hoeveel processen er actief zijn in de output van ps aux

```sh
$ ps aux | wc -l -> 216
```

Welk proces gebruikt het meeste CPU%?

```sh
$ ps aux --sort pcpu -> 3348
```

Welk proces gebruikt het meeste MEM%?

```sh
$ ps aux --sort -pmem -> 1184
```

`+` bij sort sorteerd van klein naar groot -> `Is de standaard`
`-` bij sort veranderd van groot naar klein

# Services

Service files must be placed in `/etc/systemd/system/`

Service file:

```
[Unit]
Description=Simple Python Service
After=network.target
StartLimitIntervalSec=0

[Service]
Type=simple
Restart=always
RestartSec=1
User=tiebevn
ExecStart=/usr/bin/python3 /opt/simple-service/main.py

[Install]
WantedBy=multi-user.target
```

Results in a file named:

/etc/systemd/system/simple-service.service

Enable service

```sh
$ systemctl enable simple-service
```

Disable service

```sh
$ systemctl disable simple-service
```

Status service

```sh
$ systemctl status simple-service
```

Start service

```sh
$ systemctl start simple-service
```

Stop service

```sh
$ systemctl stop simple-service
```

Create service user

```sh
$ sudo useradd -r -s /bin/nologin simple-service-user
```

Vervolgens kan je in het .services-bestand de ‘User=…’-lijn aanpassen om een andere user te gebruiken.

# Partities

Verkrijg een lijst van al je schijven

```sh
$ lsblk
```

Schrijf de output van de Primary GPT Header

```sh
$ sudo dd if=/dev/sda1 of=header bs=512 skip=1 count=1
```

skip -> Skip block sizes
count -> Number of blocks

View outpu with hexyl

```sh
$ hexyl header
```

Show ony wanted bits start bit 40 and lenght 8

```sh
$ hexyl header -s 40 -n 8
```

-s -> Start offset
-n -> Lenght

# Exercises

Schrijf een commando dat alle bestanden die eindigen op .sh in de huidige map uitvoorbaar worden voor alle gebruikers

```sh
$ chmod a+x *.sh
```

Tel hoeveel files er staan in de map /var/log

```sh
$ ls -l /var/log | wc -l
```

Schrijf een oneliner die de map ‘/etc’ kopieert naar ‘/opt/backup/etc_backup’

```sh
$ mkdir /opt/backup/etc_backup/ | cp /etc /opt/backup/etc_backup/
```

Wat is het commando om het volgende te realiseren. Hoeveel ASCII-karakters zijn er terug te vinden in het bestand /var/files/random_file.txt? (Tip wc)

```sh
$ wc -m /var/files/random_file.txt
```

```sh
$ wc -l /var/files/random_file.txt -> Lines
$ wc -w /var/files/random_file.txt -> Words
$ wc -c /var/files/random_file.txt -> Bytes
$ wc -m /var/files/random_file.txt -> Chars
```

Wat is het commando om het volgende te realiseren. Wat is de datum van de laaste HTTP request, terug te vinden in de log file van de HTTP-server in '/var/files/http.log'? Een GET en een POST zijn beide HTTP requests. Je commando moet enkel 02/Oct/2008 teruggeven.

```sh
$ cat /var/files/http.log | tail -n 1 | cut -d [ -f 2 | cut -d : -f 1
```

Wat is het commando om het volgende te realiseren. Maak in /var/files 1 bestand aan dat volgende naamgeving heeft file-1-Wednesday, als het vandaag woensdag is.

```sh
$ touch file-1-$(date +%A).txt
```

Wat is het commando om het volgende te realiseren. Welke woorden in /usr/share/dict/nederlands beginnen met _hog_ en eindigen met _ken_?

```sh
$ cat /usr/share/dict/nederlands | grep "^hog" | grep "ken$"
```

Wat is het commando om het volgende te realiseren.
Typ in je CLI "echo $RANDOM".
Gebruik voorgaand commando om een file 'getallen' aan te maken waar 15 random getallen onder elkaar in weggeschreven worden m.b.v. een for lus.
Hieronder is een voorbeeld van het bestand getallen

```sh
$ for i in `seq 15`; do echo $RANDOM; done > getallen
```

Eén getal als antwoord is voldoende.
Wat is de driewaardige getalwaarde van volgende permissie: rw--wxr-x.

```
635
```

Welk commando heb je nodig om alle lijnen in de file /etc/passwd die het woord root bevatten, en weg te schrijven in een bestand /tmp/vraag_passwd_root.

```sh
$ grep root /etc/passwd >> /tmp/vraag_passwd_root
```

Wat is het commando om de map /home/user/folder_oepsie te hernoemen naar de folder /home/user/beter_zo.

```sh
$ mv /home/user/folder_oepsie /home/user/beter_zo
```

Wat is het commando om het volgende te realiseren. Geef van alle bestanden in de directory /var/files de permissions, bestandgrootte en bestandnaam weer.

Volgend resultaat moet je bereiken:

- rw-r--r-- 69 array
- rw-r--r-- 2048 disk_header.bin
- rw-r--r-- 10535262 http.log
- rw-r--r-- 1723 passwd
- rw-r--r-- 51200 random_file.bin
- rw-r--r-- 82998 random_file.txt

```sh
$ ls /var/log -la | grep '^-' | tr -s " " | cut -d " " -f 1,5,9
```

Welk commando heb je nodig om alle lijnen in de file /etc/passwd die het woord root bevatten, en weg te schrijven in een bestand /tmp/vraag_passwd_root.

```sh
$ grep root /etc/passwd > output.txt
```

Maak een bestand ‘me.txt’ met als inhoud jouw naam, zonder gebruik te maken van een teksteditor

```sh
$ echo "Matse" > me.txt
```

Kopieer het bestand naar ‘we.txt’ en voeg wat extra namen (Pieter, Gerben, Tiebe) toe door gebruik te maken van >>

```sh
$ cp me.txt we.txt && echo -e "Pieter\nJos\nJan" >> we.txt
```

Maak een subdirectory test in je home-folder. Creëer hier in met het volgende commando wat files:

`for i in $(seq 1 9); do touch "file $RANDOM"; done && touch 'filekeep me'`

Hoe kan je alle bestanden verwijderen die net zijn aangemaakt behalve het bestand ‘filekeep me’? (Met 1 oneliner uiteraard)

```sh
$ rm -v !("filekeep me")
```

Hoeveel ruimte gebruikt de folder /var op de schijf?

```sh
$ sudo du /var -h -d 0
```

Gebruik het commando cal om de weekdag waarop je verjaart in 2050 weg te schrijven naar een nieuw gemaakt bestand

```sh
$ cal -d 2050-03 | cut -d ' ' -f 6 | head -3 | tail -2 > Date.txt
```

Voeg een lijn met de tekst ‘THE END’ toe aan het bestand dat je net hebt aangemaakt, zonder gebruik te maken van een teksteditor

```sh
$ echo 'THE END' >> Date.txt
```

Maak een nieuw bestand met een zelfgekozen naam, maar gebruik als prefix de huidige datum. Gebruik het formaat [JAAR].[MAAND].[DAG].[FILENAME] (bijvoorbeeld 2022.11.10.blabla.txt).

```sh
$ touch $(date +%Y.+%m.+%d).test.txt
```

Maak een bestand unsorted.txt aan met het volgende commando: `echo -e "1\n2\n5\n3\n4" > unsorted.txt`. Gebruik een onliner om het bestand te lezen, te sorteren en weg te schrijven naar het bestand sorted.txt.

```sh
$ sort unsorted.txt > sorted.txt
```

Gebruik het commando du om de grootte van de map /opt te tonen, 1 niveau onder de huidige directory

```sh
$ sudo du /opt/ -h -d 1
```

Gebruik het commando tee om in de map /tmp 3 bestanden (1.txt, 2.txt & 3.txt) aan te maken met als inhoud de uitvoer van de vorige oefening.

```sh
sudo du /opt/ -h -d 1 | tee /tmp/1.txt /tmp/2.txt /tmp/3.txt
```

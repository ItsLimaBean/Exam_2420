# Exam_2420

## Part 1 - Update Software

1. `sudo apt update`
2. `sudo apt upgrade`

## Part 2 - Replace
1. Replace V with C `:%s/V/C/g`
2. Replace numbs with :digit: `:%s/numbs/:digit:/g`
3. Replace echo with echo: `:%s/ech/echo/g`
4. Replace the first 1 with 0: `:s/1/0`
![Part 2](Images/part_2.png)

## Part 3 - journalctl

* I searched using /priority and shift+n to find the priority.
![priority](Images/part_3_prio.png)

* I searched for json to find the `--output` option.
![json](Images/part_3_json.png)

* I searched the man page using /boot
![boot](Images/part_3_boot.png)

* Working Command
![Working cmd](Images/part_3_work.png)

## Part 4 - Find Users

```bash
#!/bin/bash
#: Title       : find_users
#: Date        : Dec 8, 2022
#: Author      : Liam Brooke
#: Version     : 1.0
#: Description : Displays regular users and logged in users. Also outputs to /etc/motd.
#: Options     : None

function display(){
        echo Regular users on the system are:
        grep ':[1-5][0-9][0-9][0-9]:' /etc/passwd | awk -F ":" '{print $1,$3,$6}'

        echo ""
        echo "Users currently logged in are:"
        who | awk '{print $1}'
}

display

display > /etc/motd
```

## Part 5 - Service File

![Status](Images/part_5_status.png)

* Service file is located in `/etc/systemd/system`

```
[Unit]
Description=Tool to list users and output them to /etc/motd file

[Service]
Type=simple
ExecStart=/opt/find_users/find_users

[Install]
WantedBy=mutli-user.target
```

# Part 6 - Timer File

![Status](Images/part_6_status.png)

```
[Unit]
Description=Timer to start the find_users script 1 minute after boot once a day.

[Timer]
OnBootSec=1 m
Unit=find_users.service
Persistent=true

[Install]
WantedBy=timers.target
```
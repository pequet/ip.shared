#ip.shared

**ip.shared** is ip.blacklist mutualised across multiple servers.

```
git clone ssh://git@github.com/pequet/ip.shared.git
cd ip.shared
chmod +x install
./install
```

This script installs a copy of the ip.blacklist repository and sets a cron that will: 

- keep the copy of the above **ip.shared** file up to date  
- merge its contents with the **ip.blacklist** files in your local /etc/fail2ban folders

If something unfortunate happens to any copy of the list, as long as a list still exists in one of the nodes, it will be restored in full in all the nodes. To remove an IP address from it, the nodes would have to agree to start censoring the list. So make sure to whitelist your home IP in fail2ban! 

NB: the list won't grow forever but it retains the last 1000 banned IPs. 

To start or stop receiving the daily emails please edit the config section of the /etc/cron.daily/ip_blacklist or the install.sh script before running it.

To merge more frequently than once a day you can simply move the cron file or add a line to the cron list: 

```
0 * * * * /etc/cron.daily/ip_blacklist 2> /dev/null
```

Prerequisites:

- fail2ban
- permanent bans in the /etc/fail2ban/ip.blacklist file
- server with SSH access to this repository

☭



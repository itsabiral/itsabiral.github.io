---
layout: post
title: linux temperature logger
tldr: script to log temperature from multiple linux systems to one server
date: 2026-03-10
---
<a href="https://github.com/itsabiral/linux-temp-log" target="_blank" rel="noopener noreferrer">
**_github repo_**
</a><br>

log temperature of multiple linux systems to one server, used in debain/ubuntu homelab.<br>

place the python script in a temperature server<br>
then schedule the bash script in each server, which sends a curl post to the temperature server.

```
POST /temperature - to post temperature from sepecific server (our log_temp.sh does this)
GET /temperature - to get temperature in all servers.
```
**_GET /temperature_**<br>
Response
```json
[
  {
    "sensors": [
      {
        "sensor": "cpu-thermal",
        "temperature": "31.2 °C"
      }
    ],
    "server": "jhilke-pi",
    "updated_at": "2026-03-20_05-15-01"
  },
  {
    "sensors": [
      {
        "sensor": "acpitz",
        "temperature": "27.8 °C"
      },
      {
        "sensor": "acpitz",
        "temperature": "29.8 °C"
      },
      {
        "sensor": "x86_pkg_temp",
        "temperature": "44.0 °C"
      }
    ],
    "server": "jhilke-proxmox",
    "updated_at": "2026-03-20_05-14-01"
  }
]
```
**Installation**
```bash
git clone https://github.com/itsabiral/linux-temp-log.git
chmod +x linux-temp-log/log_temp.sh # exectuable permission

crontab -e # add to crontab
*/8 * * * * /home/jhilke-pi/scripts/linux-temp-log/log_temp.sh >> /home/jhilke-pi/temp_cron.log 2>&1 # run the curl script every 8 minutes


# add this to the temp server's cron to reopen on reboot/shutdown
@reboot nohup python3 /home/jhilke-pi/scripts/linux-temp-logger/server/log_temp.py > log_temp_server.log 2>&1 &
```

usecase can be tracking temperature in your homelab dashboard.

<a href="https://github.com/itsabiral/m5-dump/blob/main/homelab_temperature.py"  target="_blank" rel="noopener noreferrer"> i used it in my m5 stack</a>
<div style="display: flex; gap: 1rem; flex-wrap: wrap; justify-content: center;">
  <img
    src="{{ '/assets/images/portfolio/temp/m5stack.jpg' | relative_url }}"
    alt="m5stack"
    style="width: 500px; max-width: 100%; display: block;"
  />
</div>
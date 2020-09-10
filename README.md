# monitbot-telegram

This guide is refered from https://github.com/matriphe/monit2telegram/ . Goals:
* Monitoring database, website and ping.
* If fail, it will send notification via bot.

### Requirements
* Bot Telegram , you can create from eg: @botfather. Remember the token!
* Curl
* Bash
* JQ
* Cron

### Chat ID

```
$ curl --silent "https://api.telegram.org/bot{TOKEN}/getUpdates" | jq
```

### Deployment

```
cd /opt
git clone https://github.com/misskecupbung/monitbot-telegram
cd monitbot-telegram
vim monit-token
...
TOKEN={{ Telegram Bot Token }}
CHATID={{ Chat ID }}
...

#If you want to custom token path, you must edit :

vim monitbot-telegram/telegramrc
...
elif [ -f /path/custom ]; then . /path/custom;
...

```
### Testing
```
chmod +x pingcheck && ./pingcheck
chmod +x dbcheck && ./dbcheck
chmod +x httpcheck && ./httpcheck

```

## Cron
We use cronjob for monitoring everyday. Eg: if every 3 minutes website don't give a response, it will send notification via bot to telegram :

```
crontab -e
...
*/3 * * * * /opt/monitbot-tele
*/3 * * * * /opt/monitbot-tele
*/3 * * * * /opt/monitbot-tele
...
```
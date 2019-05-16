# upload-dokuwiki-backup-to-google-drive


## cron

put this cron task to /etc/cron.daily/dokuwiki-backup

```
#!/bin/sh

DOKUWIKI_DIR="/opt/www/dokuwiki"
STORE_DIR="/home/ubuntu/dokuwiki.backup"
NEW_FILE_NAME=${STORE_DIR}/dokuwiki.backup.$(date +%Y%m%d).tar.gz
OLD_FILE_NAME=${STORE_DIR}/dokuwiki.backup.$(date +%Y%m%d --date '4 days ago').tar.gz

cd $STORE_DIR && \
  tar zcvf $NEW_FILE_NAME $DOKUWIKI_DIR && \
  rm -f $OLD_FILE_NAME &&
  node backup-to-google-drive.js
```

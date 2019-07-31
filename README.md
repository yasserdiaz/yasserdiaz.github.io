## Purge dependency Maven repository

`mvn dependency:purge-local-repository -DactTransitively=false -DreResolve=false`

## Backup cron

`#!/bin/sh`

`find /var/backup/*.gz -mtime +6 -exec rm -f {} \;`

`mysqldump -u root -p"password" --lock-tables=false dbName | gzip -9 > /var/backup/$(date +%F)_FileName.sql.gz`

`tar zcvf $(date +%F)_site_backup.tar.gz --exclude="/var/www/html/wp-content/uploads" /var/www/html/`

## Backup Database Mysql

`mysqldump -u root -p"password" --lock-tables=false comunim3_CCRM | gzip -9 > fileName.sql.gz`

## Pack

`tar zcvf site_backup.tar.gz /var/www/html/`

`tar zcvf site_backup_lite.tar.gz --exclude="/var/www/html/wp-content/uploads" /var/www/html/`

## Unpack

`tar -zxvf site_backup.tar.gz`

## Table size

`SELECT table_name AS TableName, round(((data_length + index_length) / 1024 / 1024), 2) Size in MB FROM information_schema.TABLES WHERE table_schema = "$DB_NAME"`

## SET Permissions Site Folder & Files

`find * -type d -print0 | xargs -0 chmod 0755 # for directories`

`find . -type f -print0 | xargs -0 chmod 0644 # for files`

## SET Owner

`chown apache:apache -R folder`

`chown apache:apache -R folder/*`

## Count 

`Get-Content .\file.ext -ReadCount 10 | foreach { $_ -match "textFind" }`

## Replace

`Get-Content .\file.ext | Foreach-Object {$_.Replace('textFind', 'textReplace')} | Set-Content fileResult.ext`

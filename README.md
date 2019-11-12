## Purge dependency Maven repository

`mvn dependency:purge-local-repository -DactTransitively=false -DreResolve=false`

## Backup cron

`#!/bin/sh`

`find /dir/to/backup/*.gz -mtime +6 -exec rm -f {} \;`

`mysqldump -u root -p"password" --lock-tables=false dbName | gzip -9 > /dir/to/backup/$(date +%F)_FileName.sql.gz`

`tar zcvf $(date +%F)_site_backup.tar.gz --exclude="/dir/folder/tar/exclude" /dir/folder/tar/`

## Backup Database Mysql

`mysqldump -u root -p"password" --lock-tables=false dbName | gzip -9 > fileName.sql.gz`

## Pack

`tar zcvf site_backup.tar.gz /var/www/html/`

`tar zcvf site_backup_lite.tar.gz --exclude="/dir/folder/tar/exclude" /dir/folder/tar/`

## Unpack

`tar -zxvf site_backup.tar.gz`

## Table size

`SELECT table_name AS TableName, round(((data_length + index_length) / 1024 / 1024), 2) Size in MB FROM information_schema.TABLES WHERE table_schema = "$DB_NAME"`

## SET Permissions Site Folder & Files

`find . -type d -print0 | xargs -0 chmod 0755 # for directories`

`find . -type f -print0 | xargs -0 chmod 0644 # for files`

`chmod 440 wp-config.php`

`chmod 444 .htaccess`

## SET Owner

`chown apache:apache -R folder`

`chown apache:apache -R folder/*`

## Count on Power Shell Windows

`Get-Content .\file.ext -ReadCount 10 | foreach { $_ -match "textFind" }`

## Replace on Power Shell Windows

`Get-Content .\file.ext | Foreach-Object {$_.Replace('textFind', 'textReplace')} | Set-Content fileResult.ext`

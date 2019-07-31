# CODES

Purge dependency Maven repository
`mvn dependency:purge-local-repository -DactTransitively=false -DreResolve=false`

`#!/bin/sh`
`find /var/backup/*.gz -mtime +6 -exec rm -f {} \;`
`mysqldump -u root -p"password" --lock-tables=false dbName | gzip -9 > /var/backup/$(date +%F)_FileName.sql.gz`
`tar zcvf $(date +%F)_site_backup.tar.gz --exclude="/var/www/html/wp-content/uploads" /var/www/html/`

Backup Database Mysql
`mysqldump -u root -p"password" --lock-tables=false comunim3_CCRM | gzip -9 > fileName.sql.gz`

Pack
`tar zcvf site_backup.tar.gz /var/www/html/`
`tar zcvf site_backup_lite.tar.gz --exclude="/var/www/html/wp-content/uploads" /var/www/html/`

Unpack
`tar -zxvf site_backup.tar.gz`

Table size
`SELECT table_name AS TableName, round(((data_length + index_length) / 1024 / 1024), 2) Size in MB` 
`FROM information_schema.TABLES` 
`WHERE table_schema = "$DB_NAME"`

SET Permissions Site Folder & Files
`find * -type d -print0 | xargs -0 chmod 0755 # for directories`
`find . -type f -print0 | xargs -0 chmod 0644 # for files`

SET Owner
`chown apache:apache -R folder`
`chown apache:apache -R folder/*`

Count 
`Get-Content .\file.ext -ReadCount 10 | foreach { $_ -match "textFind" }`
Replace
`Get-Content .\file.ext | Foreach-Object {$_.Replace('textFind', 'textReplace')} | Set-Content fileResult.ext`

Wordpress htaccess
`<IfModule mod_rewrite.c>
    RewriteEngine On
    RewriteBase /
    RewriteRule ^index\.php$ - [L]
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule . /index.php [L]

    # Redirect all to www.
    #RewriteCond %{HTTP_HOST} !^www\.​
    #RewriteRule ^(.*)$ http://www.%{HTTP_HOST}/$1 [R=301,L]

	#disable hotlinking of images with forbidden or custom image option
	#RewriteCond %{HTTP_REFERER} !^$
    #RewriteCond %{HTTP_REFERER} !^http(s)?://(www\.)?hostname.com [NC]
    #RewriteCond %{HTTP_REFERER} !^http(s)?://(www\.)?hostname.com[NC]
    #RewriteRule \.(jpg|jpeg|png|gif)$ – [NC,F,L]
</IfModule>

# EXPIRES CACHING
<IfModule mod_expires.c>
	ExpiresActive On
	ExpiresDefault "access plus 1 weeks"
	ExpiresByType image/x-icon "access plus 1 month"
	ExpiresByType image/jpeg "access plus 1 month"
	ExpiresByType image/png "access plus 1 month"
	ExpiresByType image/gif "access plus 1 month"
	ExpiresByType application/x-shockwave-flash "access plus 1 month"
	ExpiresByType text/css "access plus 2 weeks"
	ExpiresByType text/javascript "access plus 1 month"
	ExpiresByType application/javascript "access plus 1 month"
	ExpiresByType application/x-javascript "access plus 1 month"
	ExpiresByType text/html "access plus 1 weeks"
	ExpiresByType application/xhtml+xml "access plus 1 weeks"
</IfModule>
# EXPIRES CACHING

# BEGIN Cache-Control Headers
<filesMatch "\.(ico|jpe?g|png|gif|swf)$">
	Header set Cache-Control "public"
</filesMatch>
<filesMatch "\.(css)$">
	Header set Cache-Control "public"
</filesMatch>	
<filesMatch "\.(js)$">
	Header set Cache-Control "private"
</filesMatch>	
<filesMatch "\.(x?html?|php)$">
	Header set Cache-Control "private, must-revalidate"
</filesMatch>	
# END Cache-Control Headers

<IfModule mod_deflate.c>
	# Compress HTML, CSS, JavaScript, Text, XML and fonts
	AddOutputFilterByType DEFLATE application/javascript
	AddOutputFilterByType DEFLATE application/rss+xml
	AddOutputFilterByType DEFLATE application/vnd.ms-fontobject
	AddOutputFilterByType DEFLATE application/x-font
	AddOutputFilterByType DEFLATE application/x-font-opentype
	AddOutputFilterByType DEFLATE application/x-font-otf
	AddOutputFilterByType DEFLATE application/x-font-truetype
	AddOutputFilterByType DEFLATE application/x-font-ttf
	AddOutputFilterByType DEFLATE application/x-javascript
	AddOutputFilterByType DEFLATE application/xhtml+xml
	AddOutputFilterByType DEFLATE application/xml
	AddOutputFilterByType DEFLATE font/opentype
	AddOutputFilterByType DEFLATE font/otf
	AddOutputFilterByType DEFLATE font/ttf
	AddOutputFilterByType DEFLATE image/svg+xml
	AddOutputFilterByType DEFLATE image/x-icon
	AddOutputFilterByType DEFLATE text/css
	AddOutputFilterByType DEFLATE text/html
	AddOutputFilterByType DEFLATE text/javascript
	AddOutputFilterByType DEFLATE text/plain
	AddOutputFilterByType DEFLATE text/xml

	# Remove browser bugs (only needed for really old browsers)
	BrowserMatch ^Mozilla/4 gzip-only-text/html
	BrowserMatch ^Mozilla/4\.0[678] no-gzip
	BrowserMatch \bMSIE !no-gzip !gzip-only-text/html
	Header append Vary User-Agent
</IfModule>`

Wordpress optimization (Move js to end body)
`function scripts_footer() {
    remove_action('wp_head', 'wp_print_scripts');
    remove_action('wp_head', 'wp_print_head_scripts', 9);
    remove_action('wp_head', 'wp_enqueue_scripts', 1);
 
    add_action('wp_footer', 'wp_print_scripts', 5);
    add_action('wp_footer', 'wp_enqueue_scripts', 5);
    add_action('wp_footer', 'wp_print_head_scripts', 5);
}
add_action( 'wp_enqueue_scripts', 'scripts_footer' );`



# **OpenWrt Daloradius V2.0 Hotspot Voucher - Fw OpenWrt 23.05.0 RC2 Clash-Wall 14.07.23 by @reyre**
![Hotspot-Login](https://github.com/masbroo69/OpenWrt-Daloradius-V2.0/assets/28827754/2b782498-335d-40ab-84dd-b0bde293a443)
![Hotspot-Login](https://github.com/masbroo69/OpenWrt-Daloradius-V2.0/assets/28827754/28e5524e-d61d-42aa-b6fe-e85f3b437d83)

daloRADIUS is an advanced RADIUS web management application aimed at managing hotspots and general-purpose ISP deployments. It features user management, graphical reporting, accounting, a billing engine and integrates with GoogleMaps for geo-locating.


![Daloradius](https://github.com/masbroo69/OpenWrt-Daloradius-V2.0/assets/28827754/ca111c49-953f-4b0a-98aa-c3e1e434a172)
daloRADIUS is written in PHP and JavaScript and utilizes a database abstraction layer which means that it supports many database systems, among them the popular MySQL, PostgreSQL, Sqlite, MsSQL, and many others.

![Hotspot-Login](https://github.com/masbroo69/OpenWrt-Daloradius-V2.0/assets/28827754/dfcbfc48-1c6b-4af1-b43d-93f1d96cb337)

It is based on a FreeRADIUS deployment with a database server serving as the backend. Among other features it implements ACLs, GoogleMaps integration for locating hotspots/access points visually and many more features.


![LuCI](https://github.com/masbroo69/OpenWrt-Daloradius-V2.0/assets/28827754/bdfa46e7-fed6-41f0-b5d8-fca1a79124d2)
OpenWrt 3.05.0 RC2 for ZTE B860H and FiberHome HG680P with more packages ported, more devices supported, better performance, and special optimizations for users. Compared the official one, we allow to use hacks or non-upstreamable patches / modifications to achieve our purpose. Source from anywhere.

**Firmware information:**
    
    - Firmware OpenWrt 23.05.0 RC2 Clash-Wall 14.07.23 by @reyre
    - Tested on STB HG680P, B860H V1 and X96-Mini
    - Themes AlphaOS by @derisamedia
    - Freeradius3, CoovaChilli, PHP8, MariaDB, etc
    - Default IP: 192.168.1.1
    - Default username: root
    - Default password: indonesia
    - Default WIFI name: WiFi
    - Default WIFI password: none

**This is a list of luci applications installed in this firmware:**
    
    - Pass Wall 
    - OpenClash
    - ZeroTire
    - NetMonitor
    - Amlogic Service
    - File Manager
    - etc

**Features Fix for Daloradius:**
    
    - Server Status and Information
    - Users and Hotspots Management Graphs
    - Batch Add Users Management (Random User, Pass and PIN)
    - List Profiles Configuration
    - Printable Tickets with Logo
    - Plans Management Currency with IDR
    - WISPr-Bandwidth-Max-Up (Upload not leaking)
    - Login by role (Voucher, Member and Trial)
    - Responsive Web-UI for phone or tablet
    

**Credits:**

    https://github.com/lirantal/daloradius
    https://github.com/derisamedia
    https://www.youtube.com/@reyre

<h2 dir="auto"><a id="user-content-installation" class="anchor" aria-hidden="true" href="#installation"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Installation</h2>
<ol dir="auto">
<li>opkg install freeradius3 freeradius3-common freeradius3-mod-attr-filter freeradius3-mod-exec freeradius3-mod-expiration freeradius3-mod-expr freeradius3-mod-files freeradius3-mod-logintime freeradius3-mod-mschap freeradius3-mod-pap freeradius3-mod-preprocess freeradius3-mod-radutmp freeradius3-mod-realm freeradius3-mod-sql freeradius3-mod-sql-mysql freeradius3-mod-sql-null freeradius3-mod-sqlcounter freeradius3-mod-unix freeradius3-utils</li>
<li>opkg install mariadb-server mariadb-server-extra mariadb-client mariadb-client-extra</li>
<li><code>/etc/config/mysqld <code>option enabled '1'</code>
mysql_install_db --force
mysql_secure_installation -u root</code></li>

<li><code># Change working directory
cd /var/www/html/</code></li>

<li># Download the daloRADIUS source code</li>
<li><code>wget https://github.com/lirantal/daloradius/archive/refs/tags/1.3.tar.gz</code></li>
<li># Extract daloRADIUS source code</li>
<li><code>tar -xf 1.3.tar.gz</code></li>
<li># Verify extracted directory</li>
<li><code>ls</li></code></li>
<li># Rename directory to `daloradius`</li>
<li><code>mv daloradius-1.3 daloradius</code></li>
<li># Verify changed directory name to daloradius</li>
<li><code>ls</li></code></li>

<li>
# CREATE DATABASE</li>
<li><code>mysql -u root -pradius -e "CREATE DATABASE radius CHARACTER SET utf8;"
mysql -u root -pradius -e "GRANT ALL ON radius.* TO 'radius'@'127.0.0.1' IDENTIFIED BY 'radius' WITH GRANT OPTION;"
ln -s /usr/share/daloradius-master /www/daloradius
ln -s /usr/share/hotspotlogin /www/client
mysql -u root radius -p < /www/daloradius/contrib/db/fr2-mysql-daloradius-and-freeradius.sql
mysql -u root radius -p < /www/daloradius/contrib/db/mysql-daloradius.sql
</code></li>
<li><code>curl -L http://pear.php.net/go-pear.phar --output go-pear.phar
ln -s /usr/bin/php-cli /usr/bin/php</code></li>

<li><code>opkg remove libgd --force-depends
opkg install php8-cli php8-mod-gd php8-mod-simplexml php8-mod-xml</code></li>

<li><code>php go-pear.phar
opkg install php8-mod-mysqli
pear install DB</code></li>

<li><code>opkg install coova-chilli
chmod a+x /etc/init.d/chilli
/etc/init.d/chilli start</code></li>

<li><code>cd /etc/freeradius3/sites-enabled
ln -s ../sites-available/daloradius daloradius
ln -s ../sites-available/inner-tunnel inner-tunnel

cd /etc/freeradius3/mods-enabled/
ln -s ../mods-available/sql
ln -s ../mods-available/sqlcounter</code></li>
</ol>

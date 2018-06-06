# how to create a deamon

First look at 
https://forum.hardware.fr/hfr/OSAlternatifs/Codes-scripts/lancer-demarrage-linux-sujet_61866_1.htm

thent add this parameter at the top of the script 
https://www.debian-fr.org/t/installation-de-script-missing-lsb-tags-and-overrides/23043/12


it will probably don't work after it due to your distribution 
 you have to run this instruction : https://mycyberuniverse.com/error/how-to-fix-setting-locale-failed.html
 
 and restart your machine
 
 ## sample 
 
 For [majestic](https://gitlab.com/cosdtw/x1-majestic) i have made this one 
 ```
 #!/bin/sh
### BEGIN INIT INFO
# Provides:          Majestic server
# Required-Start:    $remote_fs $syslog
# Required-Stop:     $remote_fs $syslog
# X-Start-Before:    nis
# X-Stop-After:      nis
# Default-Start:     2 3 4 5
# Default-Stop:	     0 1 6
# Short-Description: Start the Advanced Configuration for Majestic service
# Description:       TO DO...
### END INIT INFO
set -e

do_start(){
  cd /var/www/x1-majestic/
  DEBUG=1 python -m server.wsgi
 }

case "$1" in
  start)
    do_start
    ;;
  stop)
    echo "you can t stop majestic"
    ;;
  restart)
    $0 stop
    sleep 1
    $0 start
    ;;
  reload|force-reload)
    echo "reload or force-reload : not yet implemented"
    ;;
  status)
    echo "Status : not yet implemented"
    ;;
  *)
    echo "Usage: /etc/init.d/majestic_server {start|stop|restart|reload|force-reload|status}"
    exit 1
esac

````


# reset root passwd
1. reboot machine and press ESC to select enter mode
2. #mount -o remount,rw /
3. #passwd
4. #touch /.autorelabel
5. #exec /sbin/init

Raspberry Pi 4B + BC-11AH-A2 （802.11ah HAT）がセットされた構成に対し、電源起動時に、MESH MPP/MPのどちらで起動するかを自動判定起動するためのサービススクリプト集です。

halow_autorole.tar.gz
をダウンロードし、/HOME/pi/ディレクトリ下で解凍します。

pi@raspberrypi:~/ $ tar xfvz halow_autorole.tar.gz
pi@raspberrypi:~/ $ cd halow_autorole
pi@raspberrypi:~/halow_autorole/$ ./install.sh
[+] Added watchdog entry to rc.local:
    nohup /usr/local/bin/halow_watchdog_loop.sh >/var/log/halow_loop.log 2>&1 &
Created symlink /etc/systemd/system/multi-user.target.wants/halow_autorole.service → /etc/systemd/system/halow_autorole.service.
pi@raspberrypi:~/halow_autorole $ cat install.sh
sudo cp mesh_status.sh /usr/local/bin/
mv -n ~/nrc_pkg/script/start.py ~/nrc_pkg/script/start.py.orgin
cp start.py ~/nrc_pkg/script/
sudo cp halow.conf /etc/dnsmasq.d/
sudo cp halow_autorole.sh /usr/local/bin/
sudo cp halow_watchdog.sh /usr/local/bin/
sudo cp halow_watchdog_loop.sh /usr/local/bin/
sudo cp add_to_rc_local.sh /usr/local/bin/
sudo cp halow_autorole.service.mp /etc/systemd/system/halow_autorole.service
sudo /usr/local/bin/add_to_rc_local.sh
sudo systemctl daemon-reload
sudo systemctl enable halow_autorole.service

以上でインストール完了。
再起動して、ターミナル、またはSSH接続して wlan0 にアドレスへの割当てがあることを確認して下ださい。

接続可能なMPPが無い場合はMPPで起動します。
既に接続可能なMPPがあれば、MPとして自動で参加できるようになります。
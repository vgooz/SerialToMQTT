# SerialToMQTT
Read Serial Port data and publish it into MQTT topic

1. Install Serial library

`sudo python -m pip install pyserial`

2. Install Paho MQTT library

`sudo pip install paho-mqtt`

3. Download program and place it into /opt folder

```
sudo wget -P /opt https://raw.githubusercontent.com/vgooz/SerialToMQTT/master/SerialToMQTT.py
sudo chmod 774 /opt/SerialToMQTT.py
```

4. Create SerialToMQTT.service file with following text below

`sudo nano /etc/systemd/system/SerialToMQTT.service`

```
[Unit]
Description=Read serial data and publish it into MQTT topic
After=meadiacenter.service
[Service]
#If User and Group are not specified, then by default systemd ExecStart runs as root
User=root
Group=root
Type=simple
ExecStart=/usr/bin/python /opt/SerialToMQTT.py
ExecStop=/usr/bin/pkill -f /opt/SerialToMQTT.py
Restart=always
[Install]
WantedBy=multi-user.target
```

5. Register and enable SerialToMQTT service
```
sudo systemctl enable SerialToMQTT
sudo systemctl start SerialToMQTT
sudo systemctl status SerialToMQTT
```

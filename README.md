# WVC-inverters

Bash script to process data from WVC inverters via a the Wireless serial modem connection.  it uses the interceptty  to sniff serial connecton  between your computer and  the modem. please install interceptty ( https://github.com/geoffmeyers/interceptty) before usage.
once installed
 you simply  run wvc with the command arg  wvc port inverter.list modemID
 
 example:

wvc /dev/ttyUSB0 inverters f3b67ac4 or wvc /dev/ttyUSB0 /home/user/wvc.ini f3b5a2c5

you will need to create a inverter list in the format  WVC1200/cb76 on each new line -

WVC1200 is the inverter type  cb76 is the inverter ID

supported inverters are WVC295, WVC300, WVC350, WVC600, WVC850 and WVC1200

it support  multiple incidences  of it self connect to differnt  serials inverter.list and modemsID 

if using my version on energy monitor  just edit the host to point to the location energy router  other wise edit bash script  to point to your own energy monitor  in the format it likes IE emoncms  or other 

energy monitor
https://github.com/krywenko/BPI-R1_Zigbee2mqtt-energymonitor-openwrt
https://github.com/krywenko/Zero-Orange-Pi--MQTT-openwrt

if you have isue contact me here
https://community.openenergymonitor.org/t/data-logging-wvc-gti-inverters-with-wireless-serial-modems/12302/2

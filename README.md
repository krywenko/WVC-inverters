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

if using my version on energy monitor  just edit the host to point to the location energy router  otherwise edit bash script  to point to your own energy monitor  in the format it likes IE emoncms  or other 
its output to bash\

./wvc /dev/ttyUSB0 WVC.ini fb041187 \
 Using modem  fb 04 11 87  at port  /dev/ttyUSB0   Using  inverter list  WVC.ini \
virtural port  /dev/ttyWVCDUMMY0 

Inverter Type WVC1200 \
 no  input from inverter  cb98

 no COM  detected \
 restarting COM\
started

Inverter Type WVC1200\
Inverter ID  c784\
Temp  17\
VAC   108.527\
AAC   0.185\
VDC   32.08\
ADC   0.6666\
Panel Efficiency .93\
AC watts  20.07\
DC watts  21.38\
Overall Efficiency  .93 # the overall efficiency of the panel group

 internally it sends the data via mqtt to my energy monitors 
 
https://github.com/krywenko/BPI-R1_Zigbee2mqtt-energymonitor-openwrt

https://github.com/krywenko/Zero-Orange-Pi--MQTT-openwrt

if you have issue contact me here

https://community.openenergymonitor.org/t/wvc-inverter-mqtt-data-logging-for-all-versions-of-inverters/12352

prerequisite additional software:
interceptty ( serial sniffer), 
jq ( Json query software)

if you wish to install as stand alone device. orangepi Zero works well or any pi device  -  just install armbian (https://www.armbian.com/download/ ) influxdb chronograf and kapacitor ( for database )  if you wish automatic  data collection then install collectd 5.8  with Mqtt  plugin  and set collectd to send  data to influxdb. you can either visulize with chrongraf or grafana ( but chronograf  is not nearly as resource hungry as grafana is so i prefer chronograf )

example  enable mqtt plugin in collecd.conf  set subscribe  topic to  incoming/#  https://collectd.org/wiki/index.php/Plugin:MQTT
to enable collectd to influxdb https://docs.influxdata.com/influxdb/v1.7/supported_protocols/collectd/ or https://www.cyberpunk.rs/system-monitoring-with-grafana-influxdb-collectd

or manually install influxdb 

wget https://dl.influxdata.com/influxdb/releases/influxdb-1.6.2_linux_armhf.tar.gz

tar xvfz influxdb-1.6.2_linux_armhf.tar.gz

wget https://dl.influxdata.com/chronograf/releases/chronograf-1.7.5_linux_armhf.tar.gz

tar xvfz chronograf-1.7.5_linux_armhf.tar.gz

wget https://dl.influxdata.com/kapacitor/releases/kapacitor-1.5.2_linux_armhf.tar.gz

tar xvfz kapacitor-1.5.2_linux_armhf.tar.gz

once set up data collection is automatic

for openwrt Compatiblity _
install bash grep stty bc tac  the openwrt binary for intercepty are found in the interceptty folder plus you need  to modify line 37 in wvc and remove the ps arguements -efww

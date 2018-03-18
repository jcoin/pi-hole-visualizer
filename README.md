# Pi-hole Visualizer  - UnicornHat Version
Pi-hole Visualizer is a Python script used to display DNS traffic in a colorful and informative way on the Unicorn-HAT. It depends on the Pi-hole ecosystem and specifically the FTL daemon to retrieve statistics about DNS queries and ads blocked on the local network.  

Column height represents the relative level of traffic generated for a specific time interval in the previous 24-hour timeframe. Color is used to represent either the aforementioned traffic level or the relative percentage of ads blocked. Pi-hole visualizer can also alternate between the color coding systems at regular intervals. If you desire a more 'aesthetic' experience try the ripple option. The program is either manually run from the command line or enabled as a systemd service to run automatically at boot.  

![sense-hat display](https://github.com/jcoin/pi-hole-visualizer-unicorn/blob/master/images/unicorn_hat.mp4)

### Requirements
* To install Pi-hole, run `curl -sSL https://install.pi-hole.net | bash`
* To install the UnicornHat library, please check the [pimoroni github page](https://github.com/pimoroni/unicorn-hat) 

### Usage
**`sudo dns_stats.py [-h] [-c {basic, traffic, ads, alternate}] [-r] [-a ADDRESS] [-o {0, 90, 180, 270}] [-ll]`**  

#### Options  
`-h, --help`  
Show this help message and exit.  

`-i {10, 30, 60, 120}, --interval {10, 30, 60, 120}`  
Specify interval time in minutes. Defaults to one hour.

`-c {traffic, ads, alternate}, --color {traffic, ads, alternate}`  
Specify 'basic' to generate the default red chart, 'traffic' to represent the level of network traffic, 'ads' to represent the percentage of ads blocked, or 'alternate' to switch between traffic level and ad block percentage.  

`-r, --ripple`  
Generates a ripple effect when producing the chart.  

`-a ADDRESS, --address ADDRESS`  
Specify address of dns server, defaults to localhost.

`-o {0, 90, 180, 270}, --orientation {0, 90, 180, 270}`  
Specify orientation of display so that RPi may be installed in non-default orientation.

`-ll, --lowlight`  
Lower LED matrix brightness for use in low light environments.

`-cl, --critlogs`  
Record only critical logs (as there are not critical logs in the code, it deactivate logging).

 ### To Install As a System Service  -- Not yet tested

 1. Make the script and unit file executable:  
 `sudo chmod +x dns_stats.py`  
 `sudo chmod +x dns_stats.service`  
 
 2. Check that the path in the unit file after `ExecStart` matches the path of your script.  
 
 3. Copy the unit file to the system directory:  
 `sudo cp dns_stats.service /lib/systemd/system`  
 
 4. Enable the service to run at startup:  
 `sudo systemctl enable dns_stats`  
 
 5. Reboot:  
 `sudo reboot`  
 
 6. To check the status of the service:  
 `sudo systemctl status dns_stats`

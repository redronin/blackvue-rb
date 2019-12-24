# Blackvue-rb

A simple ruby CLI script for downloading vidoes from a Blackvue Dashcam. 
In particular, the DR900S-2CH w/ front & rear cameras.


## Background

Blackvue dashcam can be accessed by http either by having the dashcam connect
to your home network, or by connecting your computer/device to its wifi access
point.

The easiest is to configure your dashcam to connect to the Blackvue Cloud 
automatically when in range of your home network.  It's probably easiest to 
create a DHCP IP reservation for your dashcam so it has the same IP address 
each time.

Once your dashcam connects to your network, you can access the dashcam via it's
IP address. Here are some commands (if dashcam is at 192.168.2.111):

      http://192.168.2.111/blackvue_vod.cgi  => lists all files available
      http://192.168.2.111/Config/version.bin => version info
      http://192.168.2.111/Config/config.ini  => config info
      http://192.168.2.111/blackvue_live.cgi     => live view of camera
      http://192.168.2.111/blackvue_live.cgi?direction=R => live view of camera
      http://192.168.2.111/Record/<filename>.mp4 => a video file
  
      format of <filename> is YYYYMMDD_HHMMSS_<type><camera>.mp4
      where:
        <type> is NPEM for Normal | Park | Event | Manual
        <camera> is FR for Front | Rear

      eg: 20191224_113912_NF.mp4
          For Dec 24, 2019 at 11:39:12 - Normal Front camera recording

(Thanks to https://github.com/johnhamelink/blackvue/wiki and 
https://github.com/Digital-Nebula/hackvue for the info)

Alternatively, you can connect to your dashcam by connecting to it's wifi access
point. By default the IP address of the dashcam in this case would be 10.99.77.1


## Script Usage

Create a ~/.blackvue_config.yml file your home directory. An example is 
shown in the sample file and set your dashcam_ip address and where to download
the video files.


    > ./blackvue.rb

    prints out the current config settings of the script,
    counts # of video files on the Dashcam, and version information of the
    dashcam.

    {"DASHCAM_IP"=>"192.168.2.111", "STORAGE_PATH"=>"/Volumes/Media/blackvue"}
    found 191 files
    [firmware]
    version = 1.012
    model = 900S2
    language = English
    [config]
    version = 1.071


    > ./blackvue.rb -l

    Lists all files found on dashcam

    > ./blackvue.rb -d

    Downloads all files - this could take a while.
    If file already exists, and is larger than 10mb, it skips it.
    If file exists but is empty or smaller than 10mb (to handle cases where
    previous download failed), or doesn't exist it will download it.



### More to come

### Using on a synology

My use case was to run this on my Synology NAS so that the video files would
get automatically downloaded to my NAS.

I created a custom task that runs every few hours. Still working on 
process and will refine readme and script once I get things working properly.




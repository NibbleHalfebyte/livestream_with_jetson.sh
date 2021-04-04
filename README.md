Video Game Capture with a NVIDIA Jetson Nano: Internet live streaming and compressed recording
Stream video games live with this Linux script to Twitch TV (or YouTube with some modifications) and capture the video on usb memory stick or usb hard drive. This script is written for NVIDIA Jetson Nano and makes use of the NVENC, NVJPEG hardware decoder and encoder units of the Jetson Nano. It captures any video game content from 480p to 1080p and encodes it into high quality H.264 video with 1080p@30 or 720p@30, AAC sound, into a Flash video container with a bandwidth of 4.5 mbits or 3.5 mbits for transfer to an ingest server.

You need a NVIDIA Jetson Nano 4GB with display, keyboard, mouse and running X-Server. Flash a SD card (>32 GB) with Jetpack 4.5.1 Ubuntu 18.04 Linux for Jetson Nano. All you need is included in Jetpack 4.5.1. Then you need a USB sound card with some adapters, a Macro Silicon 2109 HDMI2USB stick for around 15 $/€, a Logitech C270 or better webcam with MJPEG video support and a USB3 memory stick or hard drive for recording (optional). A USB3 hub is a good investment, because the Jetson Nano 4 GB has only four USB3 inputs. Very important: Don't forget to buy a 5.5 mm, 2.15 mm barrel jack power supply with minimal 5 Volt, 4 Ampere, (20 Watt,) if you use magnetic hard disc drives (up to 10 Watt for spin up from standby)!

List of equipment and tested:

NVIDIA Jetson Nano (4GB) with Jetpack 4.5.1 on SD card
Macro Silicon 15 $/€ 2109 HDMI2USB video capture stick
Behringer UCA 202 USB sound card (with external TOS too stereo Cinch or HDMI too Stereo Cinch extractor)
Logitech C270 USB webcam (or better with MJPEG support)
A video gaming device with up to 1080p output (PC, Xbox One, Xbox 360, Xbox, Playstation 1/2/3/4, Sega, Nintendo)
optional, analog video to HDMI converters
optional, Intel 8265NGW WiFi/Bluetooth Key-E M.2 module (others won't work with Ubuntu 18.04)

If you got everything plugged and together, log into your Jetson Nano. Create a user account with a home directory. Open an xterminal (or command line window) and enter, git clone https://github.com/NibbleHalfebyte/livestream_with_jetson.git, which will download the shell script into the directory /home/<your user name>/livestream_with_jetson. Change into this directory with cd (for change directory), cd livestream_with_jetson (TAB key will complete file and directory names). This directory includes bg_black.0000.jpg (black background JPEG picture), grid.0000.jpg (simple grid b/w background), ingest_server.lst (a text copy of http://twitchstatus.com/, a GNU Public Licence text, a README.md text and the shell script livestream_with_jetson.sh. Make the shell script executable with the command chmod a+x livestream_with_jetson. After you've typed it check with ls -l (list with list option) if the script is executable. The output should look like: "-rwxrwxr-x 1 yourname yourgroup 104136 Apr 3 14:07 livestream_with_jetson.sh". Run (start) the script from your terminal window inside its directory by typing ./livestream_with_jetson.sh and pressing the return (or enter) key. The shell script is written in POSIX shell (file ending .sh for shell like Royal Dutch. (This oil company.)) and not bash, ash, zsh etc. A shell script is the UNI* version of a batch program under DOS.

The script will ask you a few questions and copy some files from its installation directory to /home/<your username>/.config/livestream_with_jetson_conf, which is a hidden configuration directory in your home directory (You can list it from there with ls -al and change into it with cd.). Please, if you install a new version of livestream_with_jetson.sh, backup and delete the file videoconfig.cfg in this directory, mv videoconfig.cfg videoconfig.cfg~ (move file to another directory or file name). Some details in the config file may have changed and can cause problems.

The first two things the script asks for is your Twitch stream key from your payed (or included in Amazon Prime) Twitch account dashboard and the which ingest server you want to use for your country. Write the stream key (copy and paste) into the terminal and it will be saved into the config directory. Next it shows you a list of ingest servers (from the file ingest_server.lst). Choose one in your region. It will be saved into the config directory for the next run or you can change both things with the next run of the script. When you start the script next time it will ask you YES or no for changing the stream key or ingest server.

The script lists some hardware in the x-terminal. Feel free to scroll up in the text with your mouse wheel and check the output. The script makes sometimes short breaks of seven seconds (It has to do with Video for Linux commands.). Please, be patient. In the next dialog the script asks you about START, change or quit. You see the number of the last preset you've chosen from the last script run. You can proceed and start with the last settings, if you want. You can create a new preset and it will be saved to the other presets in videoconfig.cfg (in case you have different consoles with different video output resolutions or you want different screen layouts and record the video or not). Or, you can exit the script at this point.

When you choose change you see a list of presets (scroll up to see all or change the size of the window). The standard preset is figure one with 1920x1080p video in and 1920x1080p@30 video out to the ingest server. Figure one can't be deleted. Write figure 2 (see 2) NEW (Create a new preset) in the text window) to create a new preset (video configuration). By writing DELETE and pressing return or enter you can delete the current preset you've been switched to (See the number in the the text line Your current configuration is set to no..). By typing a number from the preset list and return (or enter) you can change to this preset.

The first question for a new preset is your main video input or frame grabber. In Linux every hardware device has a file in the directory structure in the /dev directory. Read the script text and check if the /dev/video* (* number) is your HDMI to USB capture stick. Write yes, if so or write the path into the script. E. g. /dev/video0, if your webcam is /dev/video1 or in case you use more than one frame grabber device.

Choose a figure from the table of possible input resolutions and press return (or enter). You can choose between 16 to 9 and 4 to 3 aspect ratio for old gaming consoles. If you use analog video input converted to HDMI with a converter you must crop the border of the video signal. Choose YES or no for cropping the border of the screen about 3.5%.

Next you can choose between 1080p30 or 720p30 highly compressed H.264 video out to the ingest server. 1080p will be transmitted with 4.5 mbits and 720p with 3.5 mbits.

In the next dialog you will be asked about brightness, contrast, saturation and hue of the capture input. The image may be to dark with the cheap Macro Silicon 2109 frame grabber.

I prefer (Macro Silicon 2109 15 bucks capture stick):

brightness=-3 (default is too dark)
contrast=148 (default)
saturation=173 (default is too high)
hue=0 (default)
You will see 20 seconds the video signal from the capture card in an full screen overlay. Please, be patient. After, you can write ok or re-adjust the image. That's a little bit time consuming, because what you see on screen can vary with the result you see streamed on Twitch! Note values you think they are ok. And, be careful if you try to edit the values with an text editor directly in the videoconfig.cfg file!

Now you are asked about a border around your main video from the frame grabber and a background picture. The default background is in any case this black JPEG picture, which came with the download from Github. If you try yes, enter the full path to a directory with the custom background, mostly /home/<your username>/Pictures (Don't use the tilde '~' short cut for the file path!). The filename of the image should include zeros, like picture-0000.jpg or image.000.jpg. Rename your image file. The image should have a HD/HD Ready format, 1080p/720p e. g. The filename you have to enter now differs from the real filename! Your image file has the name image-0000.jpg, then you must write into the scripts dialog for the filename image-%04d.jpg! This is very important! Or, another example. Your image filename is cup.000.jpg, then the name in the script must be cup.%03d.jpg! This is because the image is looped with 30 frames per second and you can do more. You can use sequences of JPEG images, numbered e. g. sofa-0000.jpg, sofa-0001.jpg, sofa-0002.jpg..., which will give an background animation played in a row in an endless loop starting with image zero. (In this sofa you must type sofa-%04d.jpg into the scripts dialog.) Remember, 30 picture are a second. For one minute of animation you will need 1800 JPEG pictures! Make use of an CGI animation program to do this.

The next thing are the webcam settings. Read the devices list in the text and set the path to the webcam, e. g. /dev/video1 in the most cases, or type yes. Choose a lower resolution for the web cam. The resolution in the video stream is scaled down to 480x270p@30 picture in picture for 1080p output. Now choose the figure in the list for the camera pip position. You can choose between the four screen corners. The next dialog will adjust the cameras brightness and so on like before for the frame grabber. The picture adjustments won't work with the Logitech C270 (for me). With newer Logitech webcams it should work. You will see 20 seconds an onscreen overlay with the camera video. Write ok into the text line to accept or adjust for re-adjustment of the camera settings.

After that you will be asked to record your live stream to disc or memory stick. Try no or YES. With YES you'll be asked about the full path to the recording directory, e. g. /media/<your username>/<your storage name>/<your storage directory>.

Be patient. Write the correct path to the recording directory. If you make a mistake, you can only delete the wrong preset and redo a new one. Don't use CTRL+C to exit the script in the preset configuration! This will end in a corrupted videoconfig.cfg file!

The script will switch to the newly created preset. You can also switch to another preset at this point.

Type START to begin with the live stream. Be patient, you will see an onscreen overlay of your webcam. Write ok, last chance to get the webcam into position, or quit for exiting the script. You will see next a full screen window with the video from the frame grabber. The video stutters and will take 10 seconds. Please, be patient. It's to reset the video pipeline of GStreamer! Last, you'll be asked to START or quit the live stream. Your chance or your last for career as newbie.

Have fun!

Important tips: The Ubuntu version for Jetson Nano has power savings enabled, because most people built edge applications and robots with it. To unlock the full CPU speed you must switch the power mode to MAXN. (Top left corner of the deskop, where you see NVIDIA symbol in the top menu bar.) It's better to run jetson_clocks from the commandline to disable dynamic clocking of the CPU, GPU and accelerator units. You can put it into a start up script /etc/rc.local to run it after every reboot. Don't do any other task with the Jetson Nano, when you run livestream_with_jetson.sh. It's an embedded computer and has not much more CPU compute power than a Raspberry Pi (4x1.5 GHz ARM Cortex). The only difference are the 128 CUDA GPU cores and the NVENC, NVDEC, NVJPEG co-processing units. The main task of the CPU is memory management and shuffling data to the co-processor units!

Tested and works:
in 1920x1080 HD 16:9 -> out 1920x1080p@30
in 1920x1080 HD 16:9 -> out 1280x720p@30
in 720x480 NTSC 4:3 -> out 1920x1080p@30

Untested:
in 1360x768 HD Ready 16:9 -> 1920x1080p@30
in 1360x768 HD Ready 16:9 -> 1280x720p@30
in 1280x720 HD Ready 16:9 -> 1920x1080p@30
in 1280x720 HD Ready 16:9 -> 1280x720p@30
in 720x576 PAL 16:9 -> 1920x1080p@30
in 720x576 PAL 16:9 -> 1280x720p@30
in 720x576 PAL 4:3 -> 1920x1080p@30
in 720x576 PAL 4:3 -> 1280x720p@30
in 720x480 NTSC 16:9 -> out 1920x1080p@30
in 720x480 NTSC 4:3 -> out 1280x720p@30
in 640x480 SDTV 16:9 -> out 1920x1080p@30

Error, does not work (at the moment):
in 640x480 SDTV 4:3 -> out 1920x1080p@30

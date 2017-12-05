# Agora SDK Demo Docker Containers

- **Purpose**
	* To enable agile/iterable, containerized/platform-independent testing of Agora SDKs without the hassle of dependencies (Linux, Node.js, Nginx, C compilers etc.) 

- **Benefits**
	* Cross platform, runnable on Windows 7/8/10, MacOS, Ubuntu/Mint, CentOS/Fedora, Raspbian (Raspberry Pi) etc.
	* Hassle-free, with no need to install dependencies for the test environments on host OS: Nodejs/Nginx, C compilers etc.
	* Highly flexible and agile - one can make any changes of your own to an image container with confidence to revert back to the original state or that of any point in time
	* Highly customizable - one can commit changes, i.e. update SDK versions,  import code/packages, etc., to the base image to create new, separate images, so as to create a repository of images of different SDK versions ready for instant fire-up and testing


- **Containers**
	* [agora-recording-linux](https://pan.baidu.com/s/1c15m4Oo)
	
			CentOS 6.6, C Dev Tools, Agora Recording SDK and its compiled executable
		 
	* [agora-livebroadcast-nodejs](https://pan.baidu.com/s/1o7DF31C)
	
			Node.js, Express.js, Agora WebRTC SDK, WebRTC Live Broadcast Demo
			
	* [agora-webrtc-nginx](https://pan.baidu.com/s/1hss3nrI)
	
			Nginx, Agora WebRTC SDK, WebRTC Communication Demo

- **Prerequisites**:
	* Install [Docker](https://www.htpcbeginner.com/what-is-docker-docker-vs-virtualbox/) for [Windows](https://docs.docker.com/docker-for-windows/#shared-drives-on-demand) or [Linux](https://www.howtoforge.com/tutorial/docker-installation-and-usage-on-ubuntu-16.04/) ([MacOS](https://docs.docker.com/docker-for-mac/install/#install-and-run-docker-for-mac)/[Ubuntu](https://www.howtoforge.com/tutorial/docker-installation-and-usage-on-ubuntu-16.04/) etc.), and verify the application is up and running
	* Download the containers [here](https://pan.baidu.com/s/1slbVOYT)



- **Usage (*agora-livebroadcast-nodejs*)**
	Load the downloaded image to local repository::

		# docker load -i /path/to/images/agora-livebroadcast-nodejs.tar 
		c01c63c6823d: Loading layer [==================================================>] 129.3 MB/129.3 MB
		d9a5f9b8d5c2: Loading layer [==================================================>] 45.45 MB/45.45 MB
		2f9128310b77: Loading layer [==================================================>] 126.8 MB/126.8 MB
		63866df00998: Loading layer [==================================================>] 332.2 MB/332.2 MB
		bf3841becf9d: Loading layer [==================================================>] 352.8 kB/352.8 kB
		0da372da714b: Loading layer [==================================================>] 133.6 kB/133.6 kB
		ea2e97e9408f: Loading layer [==================================================>] 62.49 MB/62.49 MB
		072b714c90b8: Loading layer [==================================================>] 4.183 MB/4.183 MB
		0334ef88e616: Loading layer [==================================================>] 14.93 MB/14.93 MB
		Loaded image: node:latest
			Loaded image ID: sha256:b5145631b0646a42497dafbb975a8c182d5de3da52af745b430511a54c53f835
		Loaded image ID: sha256:c1d02ac1d9b4de08d3a39fdacde10427d1c4d8505172d31dd2b4ef78048559f8
	Verify that image has been properly loaded:

		# docker images
		REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
		agora/livebroadcast/nodejs   latest              b5145631b064        13 hours ago        688.3 MB
	Start the container, and browser to the host:port for testing :

		# docker run -d -p /port number on host, i.e. 2333/:80 agora-livebroadcast-nodejs startlivebcdemo
Verify the details of the running container and note the container is automatically named *"objective_borg"*:

		#docker ps
		CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                      PORTS               NAMES
		550c63477ab8        c1d02ac1d9b4        "bash"                   26 hours ago        Exited (0) 24 hours ago                         objective_borg
	Change app ID and certificate:

		# docker exec objective_borg changeappid /replace with app id/
		# docker exec objective_borg changeappcert /replace with app cert/
	Restart the container for the new ID and certificate to take effect:

		# docker restart objective_borg
	Start or stop an existing container

		# docker stop objective_borg
		# docker start objective_borg
	Access the shell of the container

		# docker exec -it objective_borg bash

- **Usage (*agora-recording-linux*) **
	Load the downloaded image:

		# docker load -i /path/to/images/agora-recording-linux.tar 
	Verify that image has been properly loaded:

		# docker images
		REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
		agora/recording/linux   latest              7d145631t233        13 hours ago        636 MB
	Start the image and run the recording executables:

		# docker run -it  -v /tmp/recording:/tmp/recording agora/recording/linux bash
		# Recorder_local 
		Usage: 
	      ./RECORD_APP --appId STRING --uid UINTEGER32 --channel STRING --appliteDir STRING --channelKey STRING --channelProfile UINTEGER32 --isAudioOnly 0/1 --isMixingEnabled 0/1 --decryptionMode STRING --secret STRING --idle INTEGER32 --recordFileRootDir STRING --cfgFilePath STRING --lowUdpPort INTEGER32 --highUdpPort INTEGER32
           --appId     (App Id/must) 
           --uid     (User Id default is 0/must)  
           --channel     (Channel Id/must) 
           --appliteDir     (directory of app lite 'video_recorder', Must pointer to 'Agora_Recording_SDK_for_Linux_FULL/bin/' folder/must) 
           --channelKey     (channelKey/option) 
           --channelProfile     (channel_profile:(0:COMMUNICATION),(1:broadcast) default is 0/option) 
           --isAudioOnly     (Default 0:ARS (0:1)/option) 
           --isMixingEnabled     (Mixing Enable? (0:1)/option) 
           --mixResolution      (format:width,high,fps,kbps 'change default resolution for video mix mode/option') 
           --mixedVideoAudio      (0:seperated Audio,Video) (1:mixed Audio & Video), default is 0, only for mix mode  
           --decryptionMode     (decryption Mode, default is NULL/option) 
           --secret     (input secret when enable decryptionMode/option) 
           --idle     (Default 300s, should be above 3s/option) 
           --recordFileRootDir     (recording file root dir/option) 
           --lowUdpPort            (default is random value/option) 
           --highUdpPort            (default is random value/option) 
           --getAudioFrame          (default 0 (0:save as file, 1:get framebuffer) /option) 
           --getVideoFrame          (default 0 (0:save as file, 1:get framebuffer) /option)
           --cfgFilePath           (config file path/option_)

- **Usage (*agora-recording-linux*) **
	Load the downloaded image to local repository:

		# docker load -i /path/to/images/agora-webrtc-nginx.tar
	Same as *agora-livebroadcast-nodejs* for rest of steps

- **Version History**
	* 2017/12/06 - 1.0
		+ initial release 









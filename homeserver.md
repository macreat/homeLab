# home server set up 


# hardware

see spefcs: 
    - CPU 
    - RAM -> basic server applications 
    - HDD device and verify 
        - need two? 


# software 


## tools 
 
    - jellfyn to translate media

# set up

## install OS

    - make a usb bootable 
        - install UBUNTU server / debian 
            - use an ISO and flash the USB using specific software 

    - connect the USB and install OS 
        -  on GUIDED STORAGE CONFIGURATION 
            - DISELECT : _set up this dis as an LVM group_ 

        - SSH CONFIGURATION (Install OpenSSH server)


## log in OS 
    
    - enter to our OS using the credentials putted (user and password - not userServer )

    - here i can see my IPV4 adress for my current partition: 192...(save it) 

        - sudo nano /etc/systemd/logind.conf (if im on a PORTATIL)
            -  AND CHANGE : 
                - dismark HandleLidSwitch, HandleLidSwitchExteernalPower, HandleLidSwitchDocked and LidSwitchIgnoreInhibited, also changes to ignore, ignore, ignore and no respectivly 

                _THIS FORCES TO USE THE PC even its closed_

            - then reboot  ( ONCE here i have one server to CONFIGURATE) 


## connect to server
    using SSH protocol communication: 
        - ssh username@IPV4... 

### update server 
    
    use :
        - sudo apt update & ... 
        . sudo apt upgrade ... 
            now reboot system : 
                - sudo reboot 


## server configuration 

_First install an interactive dash board for easily installation apps_

### casa OS 
        - run the curl... command prompt via the CLI 
            _curl -fsSL https://get.casaos.io | sudo bash_ , ref: https://casaos.zimaspace.com/ 


        - once is installed, i can go to  the server and create an account to log in with credentials into CASA OS 

#### apps 
    i can install some usefull apps:
    
        - JELLYFIN -> plex : hosting my own media server 
            - open and set up. 
                - set user name 
                    - configurate and track each path (customizable) 
        
        - to reproduce some files, it cause troubles for the hardware server so, i can use hardware acceleration into transcoding: 
            - goes to : 
                - profile, then, on adiministraton : Dashboard/Playback/transcoding -> Hardware acceleration : Intel QuickSynce (QSV) 
                    _THIS REDUCES COST COMPUTATIONAL_   

        - ARR ON search apps and , see : RADARR, PROWLARR, SONARR : automating the procurement of media. -> sailling the high seas. 


##### photos BACKUP
    
    save photos from my phone directly into my homeserver ( as alternative as iCloud / google servers) 
    - app store: immich or immich without machine learning and install: 
        - open it: 
            - save credentials as admin. 
                and login. 
                    - set up (let as default) 
                        - download the image app and log in on the phone with the _SERVER ENDPOINT URL_ using my IP ADRESS for the immich on the browser. 

                            - 192...:xxxx ... and the password... 


##### minecraft server jj

    - ... install craffty. 
        - set up credentials 
             username: ... 
             password : casaOs/files/appdata/craffty/config/default_creds.txt and put credentials. 

        - set up a local serer

    - to make a online serer, use _PLAY.GG_




##### PI- HOLE
    a black hole for internet advertisments

##### TailScale

    use wwireGuard and 2FA
        - access server from anywhere

     
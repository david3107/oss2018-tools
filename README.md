

# Docker and emulator setup


This document provides a steb by step guide on how to build the docker container, use Genymotion to emulate Android devices and use the container to run the test.

## On the host machine

1. Install [Genymotion "personal use"](https://www.genymotion.com/fun-zone/) and run an instance of Android
2. Create a folder with the .apk 
3. Build the image using the Dockerfile (see below)
4. Run the image and mount the folder with APK and tests (see below)
	
	
### Build the image using the Dockerfile 

From the docker directory run

`docker build -t "mobile_testing_automation:calabash_android" .`

### Run the image and mount the folder with APK and tests


`docker run -v /PATH/TO/YOUR/FOLDER/WITH/APK/AND/TESTS:/masvs_automation --privileged  -i -t mobile_testing_automation:calabash_android /bin/bash`



## From the container

### Connect the emulator

`adb connect IP_OF_THE_EMULATOR_ON_THE_HOST`

To get the IP of the emulator run `adb devices -l` from the host machine.

### Create the feature folder

Run `calabash-android gen` to generate the feature folder

It will create a Cucumber skeleton in the current folder like this:


    features
    |_support
    | |_app_installation_hooks.rb
    | |_app_life_cycle_hooks.rb
    | |_env.rb
    | |_hooks.rb
    |_step_definitions
    | |_calabash_steps.rb
    |_my_first.feature
    
 where `my_first.feature` will contain the gherkin syntax and `calabash_steps.rb` will contain the Ruby code 

### Run the test with Calabash

`calabash-android run APP.apk`


# Troubleshooting:

### TLS/ problem:

On the host machine run

`sysctl -w net.ipv4.tcp_mtu_probing=1net.ipv4.tcp_mtu_probing = 1`



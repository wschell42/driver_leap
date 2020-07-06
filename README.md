[![Build status](https://ci.appveyor.com/api/projects/status/2pc49d2hpt2hx944?svg=true)](https://ci.appveyor.com/project/SDraw/driver-leap) [![Release](http://img.shields.io/github/release/SDraw/driver_leap.svg)](../../releases/latest)

Fork with updated vendor libraries and extended features.

[![](./.github/repository_img.png)](https://www.youtube.com/playlist?list=PLiEPsxTlqsDk5GKcgsmeDQNRs7KV8lI-s)
  
### Installation (for users)
* Install [latest Orion Beta](https://developer.leapmotion.com/get-started)
* **Method #1:**
  * Create 'leap' folder in '<SteamVR_folder>/drivers'
  * Grab [latest release archive](../../releases/latest) for your platform
  * Extract archive to '<SteamVR_folder>/drivers/leap'
  * Add line in section 'steamvr' of '<Steam_folder>/config/steamvr.vrsettings' file:
  ```JSON
  "activateMultipleDrivers": true,
  ```
* **Method #2:**
  * Install [base project driver](https://github.com/cbuchner1/driver_leap/releases/tag/alpha8)
  * Grab [latest release archive](../../releases/latest) for your platform
  * Extract archive to '<base_project_installation_folder>/leap'

### Building (for developers)
* Open 'driver_leap.sln' solution in Visual Studio 2013
* Build your platform:
  * x64 - build output is in 'bin/win64'
  * x86 - build output is in 'bin/win32'
* Copy build files to 'leap/bin/<your_platform>':
  * driver_leap.dll
  * gesture_checker.exe
  * leap_monitor.exe  
**Note:** There are post-build events for projects to copy build files directly to SteamVR driver folder that can be enabled manually.
* Copy additional shared libraries to 'leap/bin/<your_platform>':
  * vendor/LeapSDK/bin/<your_platform>/LeapC.dll
  * vendor/openvr/bin/<your_platform>/openvr_api.dll
* Copy 'resources' folder from solution root to driver's 'leap' folder. 
  
### Control configuration and inputs
Driver can emulate HTC Vive controllers and Valve Index controllers with skeletal animation and work in desktop and HMD orientations. It's adjusted by editing settings.xml in 'resources' folder.  
There are more configurable restrictions, such as global input, trackpad, trigger, grip and etc.  
Controls are changed by game profiles that are enabled automatically when game is started from Steam.  
Available hotkeys in NumLock active state:
* **Ctrl-P:** Enable/disable right hand controller.
* **Ctrl-O:** Enable/disable left hand controller.

### HTC Vive controllers emulation
Game profiles:
  * **vrchat** - profile for VRChat. Control restrictions are ignored.  
  Controls list:
    * Gun - corresponding hand gesture
    * V-shape - corresponding hand gesture
    * Point - corresponding hand gesture
    * Rock out - corresponding hand gesture
    * Thumbs up - corresponding hand gesture
    * Spread hand - corresponding hand gesture. Also corresponds to grip button.
    * Trigger - grab gesture
    * Application menu - formed T-shape with two hands
  * **default** - profile for other games.  
  Controls list:
    * Trigger - bending of the index finger
    * Grip - grab gesture
    * System menu - formed T-shape with two hands
    * Application menu - hand with palm directed towards face
    * Touchpad - thumb press
    * Touchpad circle - index finger of another hand directed to palm
    
### Valve Index controllers emulation 
Game profiles:
  * **vrchat** - profile for VRChat. Note: game gestures are not implemented due to finger tracking, grip input profile should be used.  
  Controls list:
    * Trigger - bending of the index finger
    * Grip - grab gesture
    * Game menu - formed T-shape with two hands
  * **default** - profile for other games.  
  Controls list:
    * Trigger - bending of the index finger
    * Grip - bending of middle, ring and pinky fingers
    * Touchpad - thumb press
    * Touchpad circle - index finger of another hand directed to palm
    * Thumbstick press - touching of thumb finger tip and index finger tip of another hand
    * Thumbstick direction - arrow keys for left hand, Num2/8/4/6 keys for right hand; available when NumLock is active
    * Button A - touching of thumb and middle finger tips
    * Button B - touching of thumb and pinky finger tips
    * System button - formed T-shape with two hands

### Troubleshooting
Sometimes installation of [base project driver](https://github.com/cbuchner1/driver_leap) doesn't register driver folder for SteamVR. To manually add it:
* Open console as administrator in '<SteamVR_folder>/bin/win32' (or '<SteamVR_folder>/bin/win64') and execute command:
```
vrpathreg adddriver "path_to_leap_folder"
```
* Check if driver folder is added by calling 'vrpathreg' without any arguments
* Open '<Steam_folder>/config/steamvr.vrsettings' file and add line in 'steamvr' section:
```JSON
"activateMultipleDrivers": true,
```

### Additional Configuration to Make it work:
from [VR Software Wiki](https://sites.google.com/view/brown-vr-sw-review-2018/vr-hardware/hardware-emulators/null-driver-tutorial)

### Configuring the null Driver
1. Navigate to your Steam install folder.

On Windows, it is usually 'C:\Program Files\Steam'
On Mac, it is usually '/Users/<your user name>/Library/Application Support/Steam'
On Linux, it varies by distro, but is often at '~/.steam/steam' or '~/.local/share/Steam'
2. Navigate to the 'config' folder.

3. Open 'steamvr.vrsettings' in a text editor.

4. Copy the following within the outer layer of brackets and after whatever is there. Be sure to include the comma after the last preexisting item.

You don't strictly need the "window" parameters. If you leave them off, you'll need to use the display mirror to see what the headset sees.
,
```JSON
"driver_null" : {
      "enable" : true,
      "id" : "Null Driver",
      "windowHeight" : 1080,
      "windowWidth" : 1920,
      "windowX" : 100,
      "windowY" : 100
   },
```

### Enabling the null Driver
1. Simply set "enable" to true in the configuration seen above.

### Disabling the null Driver
Simply set "enable" to false in the configuration step seen above.

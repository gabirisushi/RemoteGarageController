 # Remote-Garage-Door-Controller
Remotely garage monitoring and control door through Particle Cloud, IFTTT

![Remote Interfaces Diagram](*going to input later*)

## Hardware:
At the heart of this project is a cellular and BLE-enabled hardware [Particle Boron](https://store.particle.io/products/boron-2g-3g-kit?pr_prod_strat=description&pr_rec_pid=1555786563653&pr_ref_pid=1654236086341&pr_seq=uniform), connected to the Particle Cloud. **It's possible to change for [Particle Electron](https://store.particle.io/products/electron-3g-kit-intl)+[NRF-51 kit](https://www.nordicsemi.com/Software-and-Tools/Development-Kits/nRF51-DK).** An generic range finder attached to the Particle measures distance from the sensor, installed in the rafters or from the ceiling of the garage and pointing downward, to either the rolled-up garage door, car, or the floor of the garage. Range measurements are interpreted as one of three states: the garage door is open, the garage door is closed and a car is present (passing), or the garage door is closed and no car is present.  A [3V Relay Shield](https://wiki.seeedstudio.com/Relay_Shield_v3/) connecting the Boron to the garage door opener's momentary toggle button terminal (in parallel with the existing garage door opener button we already have in the garage).

![Hardware Topology Image](*going to input later*)


## Repository Contents:
| File        | Target           | Description  |
| :------------- | :------------- | :--- |
| garage_controller.ino | Arduino sketch for Partile + NRF, configures Particle interfaces and handles hardware functions |
| GarageDoorController_fritzing.jpg |  | Fritzing diagram |
| GarageControllerHardwareLayout.jpg |  | Physical topology |
| GarageControllerRemoteInterfaces.jpg |  | Remote interfaces block diagram |


## Remote Interfaces

### Particle Cloud Interface:
Once the hardware has been configured and installed and firmware flashed, key variables and states from the sketch running on the board will **luckily** be available for remote viewing via either the Particle mobile app ([iOS](https://itunes.apple.com/us/app/particle-build-iot-projects/id991459054?mt=8) or [Android](https://play.google.com/store/apps/details?id=io.particle.android.app&hl=en)), or through a custom app or html5 page ([Remote opener](https://remoteaccess.mobility46.se/locations). You can also use these interfaces to send "open", "close", "toggle", and "check" commands to the boron (as string arguments to the command() function).  The Particle publishes events to the Particle Cloud when the door opens or closes, when a car arrives or departs, and when the door has been left open for an integer number of hours.

### [IFTTT](https://ifttt.com/) Integration:
Events published from the Boron to the Particle Cloud may be used as triggers for [IFTTT](https://ifttt.com/) recipes to alert you when the garage door opens or closes, a car arrives or departs, or when the garage door has been left open for an extended period of time. You can also use IFTTT to automatically respond to "gate opened for X hours" events by sending the close command to the controller.

## Deployment procedure:
1. **Connect the range sensor, relay shield to the Boron as shown in the attached diagram.**
!Fritzing Diagram *gonna input it later*
2. **Flash the garage_controller.ino to the Boron**
  * Experiment with range sensor measurements to verify general functionality.  
  * After installation, you may need to reconfigure the range values according to the height of the sensor.
3. **Install the Garage Controller in the garage.**
  1. Connect the relay to the terminal block on the garage door opener, or splice into wires going to an existing garage door toggle button.
  2. Test the configuration via the Particle cloud or mobile app, etc.
  3. If everything works well, you now can remotely check the state of the door and command it to open or close.
4. **Create IFTTT recipes**
  * Still working on it

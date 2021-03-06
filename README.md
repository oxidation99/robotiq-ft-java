[![GitHub tag](https://img.shields.io/github/tag/nnadeau/robotiq-ft-java.svg?maxAge=2592000?style=flat-square)](https://github.com/nnadeau/robotiq-ft-java/releases)
[![Build Status](https://travis-ci.org/nnadeau/robotiq-ft-java.svg?branch=master)](https://travis-ci.org/nnadeau/robotiq-ft-java)
[![Dependency Status](https://www.versioneye.com/user/projects/57d87a3d4307470032353a01/badge.svg?style=flat-square)](https://www.versioneye.com/user/projects/57d87a3d4307470032353a01)
[![](https://jitpack.io/v/nnadeau/robotiq-ft-java.svg)](https://jitpack.io/#nnadeau/robotiq-ft-java)

# Robotiq FT Sensor - Java
An unofficial Java package for cross-platform serial communication with a Robotiq FT Sensor

## Communication Protocol
The communication protocol (and basis for `config.properties`) for using a FT Sensor can be found [here](http://support.robotiq.com/pages/viewpage.action?pageId=9601256).

## Usage
### Tested Platforms
- Windows 10 x64
- OSX 10.11.5 x64

### Quick Tests
- Run `SerialUtilities.java` to list available serial ports (sensor should be connected and seen here)
- Update `comm_port` in `config.properties` to the proper serial port (e.g., `COM3` for Windows, `cu.usbserial-FTXU0M1B` for OSX)
- Run `RobotiqFtMaster.java` for a 20 second burst of data printed to the console

### Example
```java
public static void main(String[] args) {
    Logger.info("Running simple RobotiqFT connection test");
    RobotiqFtMaster robotiqFtMaster = new RobotiqFtMaster();
    try {
        robotiqFtMaster.connect();

        int maxTime = 20;
        Logger.info(String.format("Reading from sensor for %d seconds", maxTime));
        long startTime = System.currentTimeMillis();
        while ((System.currentTimeMillis() - startTime) < (maxTime * 1000)) {
            try {
                System.out.println(Arrays.toString(robotiqFtMaster.getCompleteMeasure()));
            } catch (ModbusException e) {
                Logger.error(e);
            }
        }
    } catch (Exception e) {
        Logger.error(e);
    }
}
```

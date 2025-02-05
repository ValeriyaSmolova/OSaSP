# Projects Documentation
## Contents
- [Description of models](#description-of-models)
- [Description of scripts](#description-of-scripts)
- [Installation and assembly](#installation-and-assembly)
- [Execution instructions](#execution-instructions)

## Description of models
| Project Name | Description |
|-------------|-------------|
| **[HTCTest](#htctest)** | Program for testing humidity and temperature controllers inside scanners. |
| **[RF603Logger](#rf603logger)** | Module for working with the RF603 device via a serial port to obtain measurements and record this data into a file over a specified period. |
| **[VIDEO_RECORDER](#video_recorder)** | Module for recording video from a connected camera. |
| **[Auracl](#auracl)** | Sends train wheelset data to the server and adjusts parameters. |
| **[Autorun](#autorun)** | Manages connected modules. |
| **[Bin2svg](#bin2svg)** | Converts binary files to SVG images. |
| **[Calibration](#calibration)** | Scanner calibration utility for 3DWheel measurement system. Used to configure parameters and check the accuracy of scanning. |
| **[Controller](#controller)** | Manages peripherals connected via an Ethernet-to-RS485 converter. |
| **[Converter](#converter)/[Converter_moxa](#converter_moxa)** | Transfers data between devices with different interfaces. |
| **[Cw6300](#cw6300)** | Controls the cooling system in lasers. It processes commands from other modules (Autorun, WebServer, etc), supports logging, and sends the current system status in JSON format. |
| **[Dumper](#dumper)/[Dumper60x](#dumper60x)** | Module for processing measurements, generating reports, sending results by e-mail, recording in the database. |
| **[Ecat2000](#ecat2000)** | Controls devices based on EtherCAT, using the NanotecC5E library and other modules for managing the washing and drying cycle. |
| **[Extractikp](#extractikp)** | Processes and extracts data from a file containing an IKP profile. |
| **[Genfilters](#genfilters)** | Generates files with filters based on settings from the .ini configuration file. |
| **[Genrep1](#genrep1)** | Module designed for processing and analyzing data related to the wheelschemes of trains. Extracts wheel and wheelset parameters from JSON files, generates reports and saves them to CSV files. |
| **[Genrequestkey](#genrequestkey)** | Creates and updates the requestkey.txt file, which contains information about scanners, their serial numbers, board numbers, as well as a timestamp and digital signature. This file is used to identify or authorize scanners, contains request key. |
| **[Genresponsekey](#genresponsekey)** | Performs the task of processing request keys and generating responses in the form of encrypted data. Works with keys in the request key format, decrypts them, processes information about the request and generates a new file requestkey.txt. |
| **[Indsensmon](#indsensmon)** | Module used to monitor the status of industrial sensors interacting via UDP and IPC. It is designed to receive, process and analyze data from sensors, as well as to control and configure sensors. |
| **[Ipc](#ipc)** | Interprocess communication library designed for communication between different system modules via TCP sockets. |
| **[Librf627](#librf627)** | Library designed to work with RF627 devices. |
| **[Libxlswriter](#libxlswriter)** | Library for creating Excel XLSX files. |
| **[Loader](#loader)** | Module designed to download or update the device firmware via a serial port. |
| **[MetroByWheelCalibration](#metroByWheelCalibration)** | Module for calibration data obtained from scanners. Allows to check the data for correctness, calculate parameters, visualize data and minimize parameters. |
| **[Nanotec_n5_ctl](#nanotec_n5_ctl)** | Utility for controlling motor controllers such as Nanotec N5 via a network interface by sending commands and receiving data from the device via HTTP requests. |
| **[Nport](#nport)** | Library for controlling devices connected via the RS-485 interface. Provides functions for interacting with devices by sending and receiving commands, reading and writing registers, and performing various operations such as controlling motors and reading sensor status. |
| **[RecalcRF40dump](#recalcRF40dump)** |  Module for recalculating data from a RF40-scanner by processing, generating and modifying data tables used in the calibration system. |
| **[ReprofileGUI](#reprofileGUI)** |  Program is a graphical user interface that allows you to analyze and visualize wheel profiles, comparing them with reference profiles. |
| **[ReprofilingMath](#reprofilingMath)** |  Processes and reprofiles wheel profile data based on reference profiles. |
| **[RF096](#RF096)** |  Library is designed to interact with network devices via a UDP connection. It supports device management functions, data exchange, and also has capabilities for testing and debugging via emulation mode. |
| **[RF700](#RF700)** |  Library designed to work with the RF700 controller via a serial interface. Allows to control the device, read its status, write data and update the firmware. |
| **[Rfid](#rfid)** |  Rfid device management library. Provides functionality for connecting to a device, executing commands, reading data and obtaining information about the device. |
| **[Rfidmon](#rfidmon)/[Rfidmon_eth](#rfidmon_eth)** |  Module for interacting with the RFID tag reader. |
| **[Rfmath](#rfmath)** |  Mathematics library. |
| **[Ups](#ups)** |  Library designed to interact with an uninterruptible power supply via a serial port, providing power monitoring and management functionality. |
| **[Upsmon](#upsmon)** |  Module for interacting with the uninterruptible power supply (UPS). |
| **[Webserver](#webserver)** |  HTTP-server. |
| **[Wheelui](#wheelui)** |  Program for testing the RF700 controller and Ethernet-RS485 converters. |

## Description of scripts

> **Note:** Scripts with `0` in their name are called with the flag `-minimize0`;  
> Scripts with `123` in their name are called with the flag `-minimize123`.

- **Autorun.sh** - runs the main application - autorun, as well as deleteoldfilesLoop.sh and processUnsentLoop.sh.
- **c0.sh/c123.sh** - calls metroByWheelCalibration.sh 5 times with the given parameters passed via the command line.
- **c0first.sh** - runs metroByWheelCalibration.sh with the set of parameters passed to the script, plus the additional options `-preEstimateY`, `-minimize0`, and `-save`.
- **c0step.sh** - runs metroByWheelCalibration.sh with the set of parameters passed to the script, plus the additional options `-minimize0`, and `-save`.
- **c1.sh** - does the same as c0step.sh, tells the program to perform the minimization with a certain number of iterations, equal to the value of the variable `ITERS`.
- **c123aWheel.sh** - does the same as c0.sh, with the addition of a new flag `-aWheel`.
- **c123aWheelStep.sh** - does the same as c0step.sh, with the addition of a new flag `-aWheel`.
- **c123first.sh** - does the same as c0first.sh, with the addition of flag `-orthonormalizeInput`.
- **c123step.sh** - does the same as c0step.sh.
- **c1test.sh** - runs metroByWheelCalibration.sh for left side.
- **cAll.sh** - runs the script c123first.sh, as well as scripts c123.sh, c0first.sh and c0.sh with the flag `-supressOutput`.
- **cAllaWheel.sh** - runs the script c123first.sh, as well as scripts c123.sh, c123aWheel.sh,c0first.sh and c0.sh with the flag `-supressOutput`.
- **cNot.sh** - runs metroByWheelCalibration.sh without any flags.
- **cleansedvideodetectionirkutsk.py/cleansedvideodetectionnovosib.py** - used for video processing for automatic recognition of car numbers, saving results to a file and saving the image of the current frame.
- **copyCbr.sh** - updates the cbr.ini file, making a backup copy of the current file if it exists, and replacing it with a new file from another directory.
- **copyCbrDumps.sh** - creates the specified directory and copies files from the current directory into it.
- **copyVideo.sh** - archives the files and directory, then deletes the original files and directory from the specified destination directory.
- **deleteoldfilesLoop.sh** - periodically (every 48 hours) runs the deleteoldfiles.pl script, which cleans the ~/Dumps directory from old files.
- **deleteoldfiles.pl** - perl script deletes old files and empty directories in a specified folder, creating a log file with the results of the work.
- **metroByWheelCalibration-prepare.sh** - copies the required files to the specified directory and runs the program - genfilters.
- **metroByWheelCalibration.sh** - depending on the mode 2+3 + 3+2 scanners (B2B) or 3+2 + 2+3 scanners (BIR) launches the corresponding program metroByWheelCalibration or metroByWheelCalibration32.
- **processUnsent.sh** - designed to send files from the unsent folder to the server via API. After successful sending, the file is deleted, and in case of an error sending, the file remains in place.
- **testCbr.sh** - designed to prepare, process and restore configuration files and results.
- **visWheelInfo.py** - processes data from files and visualizes the results in the form of graphs.
- **test.c** - is designed to monitor the status of control signals of the serial port (/dev/ttyS0).

## Installation and assembly

**Installation Requirements**
- **Qt**: Version 5.15.13 or higher
- **Compiler**: GCC
- **OS**: Linux

**Using Qt Creator**
1. Open `*.pro` (if using qmake) or `CMakeLists.txt` (if using CMake).
2. Select the required compiler and Qt version.
3. Select "Build".

**Using Terminal**
- **qmake:**
  ```sh
  qmake project.pro
  make
  ```
- **cmake:**
  ```sh
  mkdir build && cd build
  cmake ..
  make
  ```

**Perl Script Execution**
- Check if Perl is installed:
  ```sh
  perl -v
  ```
- If missing, install:
  ```sh
  sudo apt install perl
  ```
- Install required module:
  ```sh
  cpan install Date::Calc
  ```
- Run Perl script:
  ```sh
  ./script_name.pl /path/to/folder
  ```
**Python Script Execution**
- Check Python version:
  ```sh
  python3 --version
  ```
- If missing, install:
  ```sh
  sudo apt update && sudo apt install python3 -y
  ```
- Install required libraries:
  ```sh
  pip3 install opencv-python numpy matplotlib
  ```
- Run Python script:
  ```sh
  python3 script_name.py --video /path/to/video
  ```
**Running Shell Scripts**
- Execute a shell script:
  ```sh
  ./script_name.sh
  ```

---

## Execution instructions

### RF603Logger
Need to enter a command with four parameters that it accepts:
```sh
./rf603logger <portName> <baudRate> <outFile> <time>
```
- `<portName>` - name of the port device is connected to;
- `<baudRate>` - data transfer rate for the serial port;
- `<outFile>` - file name for writing data;
- `<time>` - the time in seconds that the program will run.

### VIDEO_RECORDER
Need to install OpenCV:
```bash
sudo apt-get install libopencv-dev
```

### Auracl
To run need to have `auracl.conf` file, to read the settings and JSON file, which should contain the wheelset data.  
`auracl.conf` may contain the following data:
```ini
[General]
verbose=
id=""
authKey=""
urlBegin=""
urlMeasurements=""
treat299AsWarning=
```

And JSON file must contain such information:
```json
[
    [
        [
            [
                {
                    "D": 1042.4140321797554,
                    "L": 141.04669011598597,
                    "T": 71.86161922333406,
                    "oG": 2.716020463153e-312,
                    "profile": [],
                    "qR": 8.050412021050088,
                    "rO": 4.14923135823217,
                    "sD": 29.010182784153866,
                    "sH": 29.71943607451745
                },
                {
                    "D": 1052.2438579766408,
                    "L": 140.94356920920177,
                    "T": 77.0723242638328,
                    "oG": 2.716020463153e-312,
                    "profile": [],
                    "qR": 11.981696563448224,
                    "rO": 3.812256131258879,
                    "sD": 30.48156247820173,
                    "sH": 32.09406794808128
                }
            ],
            {
                "A2": 1499.5017925055909,
                "AxisRO": null,
                "B2b": 1440.0100472432352,
                "EC": 0,
                "Number": 0,
                "detectionTime": 6.312
            }
        ],
        {
            "carNumber": "3051",
            "detectionTime": 0,
            "wheelsetCount": 1
        }
    ],
    {
        "attachment": "_22.11.2022.xls",
        "dateTime": "2022-11-22T16:48:40",
        "ok": true,
        "speed": 8.5,
        "version": 2
    }
]
```

### Autorun
Depends on the ipc library. An `autorun.conf` configuration file is required to store the settings and commands that will be executed.
```ini
[General]
sourceId=12
```
The system identification number is set (indicated in reports, when writing to the database). The following are the sections for the settings of the activated modules:

```ini
[webserver]
title="Web Server"
commands="restart,log"
order=0
```
where `title` is the title displayed on the web page, `commands` is the list of allowed module control commands, `order` is the order of launch (optional); available commands: start, stop, restart, log.

### Bin2svg
Depends on the rfmath library. Uses the `.conf` configuration file.  
Example, `bin2svg.conf`:
```ini
[Image]
graphWidth=500
graphHeight=500
spacingLeft=30
spacingBottom=30
spacingTop=10
spacingRight=10
axisStep=50
```
Expects three command line parameters:
- `infile`: input binary file;
- `outfile`: output SVG file;
- `nframe`: frame number.

### Calibration
Depends on the rfmath library. The program expects several configuration files and source data:
- `params.ini`: configuration file for parameters such as `belgimL`, `belgimR`, `dumpsPath`, `side` and others;
- `results.ini`: file for storing results;
- `RF_*.bin`: files with data for calibration. The program reads binary files with points, which are supposed to be in the `dumpsPath` directory;
- `belgimL` and `belgimR`: the calibration data files for the left and right sides.

### Controller
Depends on ipc and rf700 libraries. Also loads settings from the `controller.conf` file:
```ini
[General]
dumpBaseDir=/home/riftek/Dumps
```
Sets the path to the directory for saving the drive files.

```ini
[RF700]
port=/dev/ttyS1
baud=115200
PWR_Wr=255
OUT_Wr=0
T_Sync=10
SyncOnTOut=1
```
RF700 controller settings:
- `port`, `baud` – serial port name and data exchange rate;
- The following parameters are optional:
  - `PWR_Wr` – starting value of the power control register;
  - `OUT_Wr` – starting value of the additional power register;
  - `T_Sync` – time in sec after which the system stops measuring if there is no activity from the inductive sensors;
  - `SyncOnTOut` – minimum response time of the inductive sensor in ms.

The program communicates with the RF700 device connected via serial port. Check that the correct parameters are set in `controller.conf`.

### Converter
Depends on ipc and rf096 libraries. Should include files from directory `./webserver/3rdparty`. And there must also be a configuration file `converter.conf`.
```ini
[General]
count=4
localIp=192.168.1.2
dumpBaseDir=/home/riftek/Dumps
delayMotors=100
delayModules=30
```
- `count` – number of converters (1 per module);
- `localIp` – IP address of the network interface through which data is exchanged with the converter;
- `dumpBaseDir` – path to the directory for saving the drive files (must match the value in p.2);
- `delayMotors` / `delayModules` – delay between sending commands to the motor drivers (`delayMotors` – in one module, `delayModules` – between modules).

The following are the settings sections by module:
```ini
[1]
ip=192.168.1.10
remotePort=6008
localPort=6003
coversCount=2
coverAddr1=10
coverAddr2=11
netAddr=1
htcCount=1
htcAddr1=20
invert2=true
```

`[1]` – section name, from 1 to `count`, specified in the `General` section. The section name corresponds to the module number in the system.

### Converter_moxa
Depends on nport and ipc libraries. There must be a file `converter_moxa.conf`:
```ini
[General]
count=4
autoUpdateStatesInterval=30
coversMoveTime=5
```
```ini
[0]
port=/dev/ttyr00
baud=115200
motorsCount=1
htcCount=1
```
### Converter_stub
Depends on ipc library. The program uses `converter_stub.conf` file:
```ini
[General]
addr1=
addr2=
addr3=
addr4=
steps=4000
dir=-1
readStateInterval=1000
```

- `addr1`, `addr2`, `addr3`, `addr4` – IP addresses for the devices;
- `steps` – number of steps the motors move per command;
- `dir` – direction of movement;
- `readStateInterval` – interval (in ms) to read motor states.

### Cw6300
Depends on ipc and modbus. The `upsmon.conf` configuration file specifies parameters such as timeout settings and logging levels. Make sure it exists and contains the correct values for the parameters.

### Dumper
Includes ipc library and files:
- `dumper.conf`: ini file with configurations;
- `responsekey.txt`: file containing encrypted response for the license.

Settings file – `dumper.conf`:
```ini
[General]
dumpBaseDir=/home/riftek/Dumps
```
```ini
[RF627]
count=10
```
- `count` – number of laser scanners installed in the system
```ini
[210172]
ip=35
label="P2_L0"
id=0
module=0
index=1
crossSectionPlaneBias=60
invertRefPoints=true
```
- `[section name]` – serial number of laser scanner
- `ip` – scanner number in diagram (also last part of IP address tetrad)
- `label` – scanner name in diagram;
- `id` – internal identifier;
- `module` – internal module identifier;
- `index` – element index;
- `crossSectionPlaneBias`, `inverRefPoints` – parameters used in frame calibration.
```ini
[calibration]
planesCount=7
refPointsCount=8
L=parsingOutputOf20220207_012L_correctedPlatesOrder_nonStandart25.txt
R=parsingOutputOf20220207_012R_nonStandart25PlatesOrientation.txt
ini=cbr.ini
frameDivisor=500
```
Parameters used in frame calibration.

### Dumper60x
Similar to the program *dumper*, this project also contains library and configuration file. The program supports several command options, for example:
- `-d` or `--dump` to perform a dump;
- `-t` or `--time` to set the dump execution time in seconds.

### Dumpprocessor
Uses ipc and rfmath libraries. Configuration file – `dumpprocessor.conf`:
```ini
[General]
valid_min_wheelsets=4
valid_direction=2
title=3DWheel 010 (Irkutsk)
dbapi_url=https://3dw010-irk.org.com/api/train/train-measurement
cloud_url=https://cloud.org.com/index.php/s/WebdavHash
ASUPRIG_url=http://10.1.2.3/AsutReports/Wheel3D/SvcWheel3D.asmx?appl=9235
ASUPRIG_version=2
ASUPRIG_RD=9235
generateTY18=true
generateTY17=true
generateTY28=true
generateTY_per_car=true
cyrillic_rfid=true
generateNonvalidReports=true
rebuildScheme=true
```  
- `valid_min_wheelsets` – minimum number of wheel pairs for generating a report;
- `valid_direction` – permissible directions of movement of the train: 0 – forward, 1 – reverse, 2 – in both directions
- `title` –installation name;
- `generateTY(18,17,28)` – specifies whether to generate reports of forms TY-18, 17 and 23 respectively;
- `generateTY_per_car` – indicates that separate report files will be generated for each car (required if unloading into the PRIG ACS is enabled);
- `cyrillic_rfid` – set to true if radio tags use Cyrillic characters;
- `generateNovalidReports` – means that reports will be generated even with missing values ​​of calculation parameters;
- `rebuildScheme` –includes detection of cars in case of partial movement of the train over the system;

The following parameters are optional:
`dbapi_url` – URL of the 3DWheel database recording service;
`cloud_url` – URL of the cloud service where the travel data files are saved;
`ASUPRIG_url` – ASU PRIG service URL;
`ASUPRIG_version` – service version;
`ASUPRIG_RD` – data source identifier for ACS PRIG.

```ini
[mail]
empty_debug_recepients=user1@gmail.com user2@gmail.com
debug_recepients= user1@gmail.com
recepients= user1@gmail.com user2@gmail.com official@gmail.com
smtp_server=mail.org.com
smtp_port=2525
smtp_login=railway-robot@org.com
smtp_passw=Password
```

- `empty_debug_recepients` – list of e-mail recipients to which reports on “empty” measurements will be sent (random system activations, train maneuvering, etc.);
- `debug_recepients` -- list of e-mail recipients to which reports on partial train measurements will be sent (cases of incomplete train arrival at the depot, absence of radio tags on board);
- `recepients` -- list of e-mails recipients to which reports on the full composition measurement will be sent;
- `smtp_server`, `smtp_port`, `smtp_login`, `smtp_password` – settings of the SMTP server of the mail service, with the help of which the mailing is carried out.
 

### Extractikp
This program is launched with three command line parameters:
- `infile input.ikp` — path to the input file with IKP format data (the file that the program will read);
- `outfile output.txt` — path to the output text file where the results will be written;
- `number 1` — profile number to be processed from the input file.

### Genfilters
This program is launched with two command line parameters:
- `infile path/to/cbr.ini` — path to the input INI file containing the parameters that the program will read;
- `outdir path/to/output/directory` — path to the directory where two text files will be written: filteringL.txt and filteringR.txt.

### Genrep1
Ensure the `genrep1.ini` configuration file is in the correct directory or adjust the path to it within the program.

The program expects specific values for `wheelParams` and `wheelsetParams` inside `genrep1.ini`. Also, it expects JSON files for the wheel schemes. These files should be in the working directory that you provide when running the program.

The files should be structured correctly to match the fields expected by the `CWheelScheme` class. Ensure that the JSON files contain data like `trainNumber`, `dateTime`, and relevant wheel and wheelset parameters.

### Genrequestkey
Includes RF62X-SDK. `Requestkey.txt` must be read/write.

### Genresponsekey
```sh
./genrequestkey -i request.txt -o responsekey.txt
```

### Indsensmon
Includes ipc library. Create `indsensmon.conf` in the folder with the executable file:
```ini
[General]
deviceIp=192.168.0.254
devicePort=4001
interface=192.168.0.2
port=4001
```
- `deviceIp` — IP address of the device to which packets are sent;
- `port` and `devicePort` — ports for receiving and sending;
- `interface` — local IP to which the UDP socket will be bound.

### Loader
Must include rf700 library. The launch is performed by the following command:
```sh
./loader -i firmware.bin -p /dev/ttyUSB0 -b 115200 -a 0
```
- `i firmware.bin` — path to the firmware file;
- `p /dev/ttyUSB0` — the port to which the device is connected;
- `b 115200` — baud rate;
- `a 0` — device address (default 0).

### MetroByWheelCalibration
Depends on rfmath library. This program requires several files to work correctly:
- Scanner calibration file, path:
`/your_data_folder/calibration/Cbr_new.ini`
This file should contain information about the scanners, their positions and orientations.

- Binary data files RF_xx.bin
Scanner measurement files, path:
`/your_data_folder/RF_xx.bin`
They contain wheel measurement profiles. Should match the number of scanners (Nscanners).

- Wheel profile file, path:
`/your_data_folder/etalon/wheelProfileL.txt` (or wheelProfileR.txt for the right side)
The file must contain the coordinates of the profile points in the format:
x1  y1  
x2  y2  
...
- File `wheelParams.ini`
Wheel parameters file, path:
`/your_data_folder/a/wheelParams.ini`
It stores the values ​​of the radius, width and height of the wheel.

- File `filtering.ini`
Filtering file, path:
`/your_data_folder/etalon/filtering.ini`
Used for processing profiles.

The program creates output files in the output folder, but before doing so, you need to make sure that this folder exists, otherwise it will give an error.

Calibration algorithm:
> 00. Manually copy (only first time) `Cbr.ini` and rename as `Cbr_new.ini`, `isUseNewCalibration = true`, `isSave = true`;
> 0. Set the correct side here and above (where is wheel params);
> 1. First run: `isMinimize123 = true`, `isMinimize0 = false`, `isUseAnotherWheelForR = false`, `isPreEstimateY = true`;
> 2. Next runs: `isPreEstimateY = false`;
> 3. Next+N runs: `isUseAnotherWheelForR = true`;
> 4. First run: `isMinimize123 = false`, `isMinimize0 = true`, `isPreEstimateY = true`;
> 5. Next runs: `isPreEstimateY = false`.

### MetroByWheelCalibration32
Also depends on rfmath. Includes files such as:
`configuration.ini` – contains system information:
- `mirroring mode`;
- `wBase`, `pois` – base and point parameters;
- `scanner ranges`, `glue`, `isWpositive` – scanner ranges, gluing parameters and W direction;

`session.ini` – contains information about the calibration session:
- `calibrationFileFolder` – folder with calibration data;
- `wheels information` – information about wheels:
- `side` – side (left or right);
- `dump folder` – folder with dumps;
- `index in dump` – index in dump;
- `etalon profile file` – reference profile;
- `D, H, W` – wheel parameters.

Check that the `calibrationFileFolder` folder exists and contains `cutting.txt` and `Cbr_new.ini`.

### Nanotec_n5_ctl
The program expects command line arguments:
```sh
./nanotec_n5_ctl -a 192.168.1.100 -c move 5000
```
- `-a (--address)` – IP address of the device;
- `-c (--command)` – command to execute (move);
- `Number 5000` – target motor position.

Before starting, please make sure that the Nanotec device is accessible.

### RecalcRF40dump
Depends on rfmath library. The program requires the following files:
`RF_40.bin` – binary dump file (in the specified folder);
`tz_old.tbl` – original calibration table (in the root folder with the program);
`tz.tbl` – new calibration table (in the root folder with the program).

### ReprofilingMath
Includes rfmath library. Also should contain:
`Etalon file`: The etalonFilename (e.g., BRU_Loco_29.ref) is a reference file that the program uses for comparison;
`Profile CSV files`: You need the profile files for each wheel in the profiles folder (e.g., l_0.csv, r_0.csv, etc.) in the directory specified by the dumpFolder parameter;
`Configuration file`: reprofile.conf, which is used to store configuration parameters such as the etalonFilename, maxAllowableY, minAllowableY, etc;
`Results directory`: The program will generate output files, such as reprofileResult.csv and .txt files for each processed wheel profile.

Once the program is compiled, you can run it from the terminal/command prompt:
```sh
./reprofilingMath <path_to_etalon_file> <path_to_dump_folder> [<debug_wheel_side (l|r)> <debug_wheel_index>]
```

- `<path_to_etalon_file>`: The path to the etalon .ref file;
- `<path_to_dump_folder>`: The path to the folder containing the profile data (profiles folder);
- `[<debug_wheel_side (l|r)> <debug_wheel_index>] (optional)`: For debugging, you can specify the wheel side (l for left, r for right) and the index of the specific wheel.

### Rfidmon
Must include rfid and ipc libraries, and `rfidmon.conf` file:

```ini
[General]
count=1
emailNotifications=true

[1]
port = "/dev/ttyUSB0"
baud = 9600

[2]
port = "/dev/ttyUSB1"
baud = 9600 
```

### Rfidmon_eth
Includes ipc library. Settings file – `rfidmon_eth.conf`:

```ini
[General]
interface=10.82.0.3
port=9999
```

IP address of the interface and the port to which the RFID receiver is configured to broadcast.

### Upsmon
Depends on ipc and ups libraries. Settings file – `ups.conf`:

```ini
[UPS]
port=/dev/ttyS0
baud=2400
```

- `port` – serial port name;
- `baud` – data exchange rate.

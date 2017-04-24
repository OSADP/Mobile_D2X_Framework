Open Source Overview
============================
Application name
----------------
D2X Hub 

Version number
-------------- 
Version 1.0

Application description
-----------------------
The D2X Hub provides a platform to facilitate agencies’ initiatives of data exchange between mobile devices, traffic management systems, ITS devices and vehicles.  The D2X Hub is a message handler, supporting the translation of data between different industry standards used by connected vehicles, devices, or components.  The D2X Hub uses a modular component design to facilitate the integration of its applications with the hardware or applications specific to different traffic management systems, ITS devices, connected vehicles, or other mobile devices to support this data exchange. The four main components of the D2X Hub are: (1) the Mobile Device, (2) the In-Vehicle Device, (3) the Roadside Unit and (4) the Cloud Infrastructure. The primary functions and software applications are as follows: 


Primary functions
-----------------
Mobile Device Experimental Application (MDEA):
The Mobile Device Experimental Application (MDEA) is the application that resides on the smartphone of the traveler.  It has three (3) primary sub-modules:
• Pedestrian Safety Monitor – to monitor incoming BSM messages and transmit PSM messages.
• Ride Request Monitor – to manage PMM messages and travel groups.
• MDEA User Interface – to manage user interaction with Safety and Ride monitors.

In-Vehicle Experimental Application (VEA):
The In-Vehicle Device Experimental Application (VEA) is the application that resides on the bus/taxi Onboard Unit (OBU).  It has three (3) primary sub-modules:
• VEA Pedestrian Monitor – to transmit BSM messages and monitor PSM messages.
• VEA Ride Request Monitor – to monitor PMM messages and respond to them.
• VEA User Interface – to manage user interaction with Safety and Ride monitors.

Roadside Experimental Application (REA):
The Roadside Experimental Application (REA) is the application that resides on the Roadside Unit (RSU), nearby a passenger pick-up stop.  It serves to receive and log information, as well as transmit SPaT & MAP.  SPaT is simulated for the purposes of this project.  It has two (2) primary sub-modules:
• REA Monitor – to log BSM, PSM and PMM messages received via DSRC interfaces.
• SPaT& MAP message generator – to broadcast simulated SPaT and MAP messages.

Cloud API:
The PMM Message Receiver Web API module provides a Web API interface that is utilized by both the mobile devices and the in-vehicle devices to exchange ride request information.  The Web API consists of functions which allow for requests to be added to the system, checking for pending requests, and responding to requests.

A Microsoft Azure SQL Database module provides database functionality in order for the Web Service to be able to create and modify database entries.  The database is leveraged to route PMM messages between a traveler and a vehicle prior to being within DSRC range.

Mobile DSRC Message Handler:
Mobile phones are not yet equipped with the capability to send and receive DSRC messages.  In order to provide this functionality, the mobile device is paired (via Bluetooth) to a portable Arada radio.  The Arada Portable DSRC radio is responsible for providing all the DSRC communication needs of the mobile device.  The transmission and receipt of all messages sent over DSRC will is processed on this platform as well as message decoding and formatting.  Software residing on the Arada is customized to provide functionality to the MDEA to control what messages are sent out.  The Arada also receives and passes on incoming DSRC messages from other devices. 

Installation and removal instructions
-------------------------------------
MDEA: Download and unzip zip file from OSADP.  Open in Visual Studio. Build and deploy to mobile device using Visual Studio.

VEA: Refer to the V2I Hub Documentation (https://www.itsforge.net/index.php/community/explore-applications/for-search-results#/40/125) for instructions on installing the V2I Hub core software before proceeding to add the VEA software.  The VeaPedestrianMonPlugin and VeaRideRequestPlugin are the two plugins created for D2X Hub and are installed following the same procedure as those for V2I. The following plugins should be running on the VEA CCP:

Plugin Name				Version
CCPStatus				0.0.4
CloudInterfacePlugin			0.0.29
Cohda DSRC TxRx				1.0.5
CohdaInterface (Enable Bsm=true)	0.1.1
EventLoggingPlugin (log level Info)	0.0.3
LocalLogging				0.5.0
Location				1.1.0
TMX UI Information			1.0.0
TMX UI MobileDevicesUI			1.0.0
VeaPedestrianMonPlugin			0.0.1
VeaRideRequestPlugin			0.0.1

REA: Refer to the V2I Hub Documentation (https://www.itsforge.net/index.php/community/explore-applications/for-search-results#/40/125) for instructions on installing the V2I Hub core software, which provides the D2X Hub REA. The following plugins should be running on the REA CCP:

Plugin Name				Version
CCPStatus				0.0.4
Cohda DSRC TxRx				1.0.5
CohdaInterface(Enable Bsm=false)	0.1.1
EventLoggingPlugin			0.0.3
LocalLogging				0.5.0
Location				1.1.0
Map Plugin				1.1.6
Spat Plugin				1.0.2

Cloud API: Download and unzip zip file from OSADP.  PublishProfiles have not been included.  Please recreate these to point to your Azure resources where you wish to deploy.

Mobile DSRC Message Handler: Refer to the V2I Hub Documentation for instructions on installing the V2I Hub core software before proceeding to compile the Mobile DSRC Message Handler (Arada) software.  The TMX_OAM directory must already be in place.

Compilation Instructions
• Change directory to the MIPS-Release subfolder for the project (cd MIPS-Release).
• Run cmake (cmake ..) to build the makefile.
• Run make (make) to compile the project.

Installation Instructions
• Transfer the compiled executable to the /var/bin directory of the Arada LocoMate device using standard Linux tools (e.g. scp).
• If the project contains a file named “treerepair.xml”, this file must also be transferred to the /var/bin directory of the LocoMate device.
• The user interface to the LocoMate™ ME is through a telnet connection using hardwired Ethernet.  Once a user has logged into the device, a command line interface is used to configure the device using standard Linux commands.
• A command line interface is provided by Arada (i.e. cli) that allows the user to manage the operation of the DSRC radio and its external interfaces, including automatic startup of the application.  Refer to the LocoMate User’s Guide for details

License information
-------------------
Licensed under the Apache License, Version 2.0 (the "License"); you may not use this
file except in compliance with the License.
You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0
Unless required by applicable law or agreed to in writing, software distributed under
the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
KIND, either express or implied. See the License for the specific language governing
permissions and limitations under the License.

System Requirements
-------------------------
Following are the computer system requirements for development, installation, and operation of the D2X Hub applications.  

MDEA: Built on Xamarin and Visual Studio
• PC running Windows 7 or higher
• Visual Studio 2015
• Xamarin 4.3.0.784 
• Android-compatible mobile device
• Android version minimum target: API Level 21 – Lollipop
• Xamarin.Android 7.1.0.41 

VEA: Built on V2I Hub.  V2I Hub is middleware that runs on Linux Ubuntu 14.04 LTS.  Please refer to the V2I Hub Documentation on the OSADP: https://www.itsforge.net/index.php/community/explore-applications/for-search-results#/40/125
• Battelle Common Computing Platform (CCP) (i.MX6-based single board computer with Cohda RSU could alternatively be employed, using different set of plugins)
• V2I Hub core software v2.3.1 or higher
• V2I Hub LocationPlugin v1.1.0 or higher
• CCPStatusPlugin v0.1.0 or higher
• CohdaInterfacePlugin v0.1.5 or higher

REA: Built on V2I Hub. V2I Hub is middleware that runs on Linux Ubuntu 14.04 LTS.  Please refer to the V2I Hub Documentation on the OSADP: https://www.itsforge.net/index.php/community/explore-applications/for-search-results#/40/125
• Battelle Common Computing Platform (CCP) (i.MX6-based single board computer with Cohda RSU could alternatively be employed, using different set of plugins)
• V2I Hub core software v2.3.1 or higher
• V2I Hub MAP R41 Plugin v1.1.6 or higher
• V2I Hub SPAT R41 Plugin v1.0.2 or higher
• CCPStatusPlugin v0.1.0 or higher
• CohdaInterfacePlugin v0.1.5 or higher

Cloud API:
• PC running Windows 7 or higher
• Visual Studio 2015

Mobile DSRC Message Handler:
The Mobile DSRC Message Handler application is written in C and C++ using interfaces supplied by the manufacturer.  The development for the application that resides on the DSRC radio uses Arada’s WAVE API version 1.86.  The application executes on a Linux operating system using the LocoMate™ tool chain version 1.42.  This API includes Security, GPS positioning and SAE J2735 messaging.

Documentation
-------------
- Concept of Operations.  Sharing Data Between Mobile Devices, Connected Vehicles and Infrastructure, Task 3: Concept of Operations Technical Memorandum – FINAL: http://ntl.bts.gov/lib/60000/60800/60820/FHWA-JPO-16-422.pdf   

- System Requirements.  Sharing Data Between Mobile Devices, Connected Vehicles, and Infrastructure, Task 3: System Requirements Specifications (SyRS) – FINAL: http://ntl.bts.gov/lib/60000/60800/60821/FHWA-JPO-16-423.pdf

- System Architecture and Design. Sharing Data between Mobile Devices, Connected Vehicles, and Infrastructure, Task 4: System Architecture and Design Document – FINAL:  508 PDF delivered

- Proof of Concept Experimental Plan. Sharing Data between Mobile Devices, Connected Vehicles and Infrastructure, Task 5: Prototype Proof of Concept Field Demonstration Experimental / Field Demonstration Site Plan – FINAL:  508 PDF delivered

- Acceptance Test Plan. Sharing Data between Mobile Devices, Connected Vehicles and Infrastructure, Task 6: Prototype Acceptance Test Plan – FINAL:  508 PDF delivered

- Acceptance Test Summary Report. Sharing Data between Mobile Devices, Connected Vehicles and Infrastructure, Task 6: Prototype Acceptance Test Summary Report – DRAFT:  Word doc delivered

- Proof of Concept Test Report.  Sharing Data between Mobile Devices, Connected Vehicles and Infrastructure, Task 8: Prototype Proof of Concept Test Report – DRAFT:  Word doc soon to be delivered

Web sites
---------
This software is distributed through the USDOT's JPO Open Source Application Development Portal (OSADP)
http://itsforge.net/ 

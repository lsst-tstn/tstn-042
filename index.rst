:tocdepth: 1

.. sectnum::

.. Metadata such as the title, authors, and description are set in metadata.yaml

.. TODO: Delete the note below before merging new content to the main branch.


Abstract
========

Description of the electronics cabinet that will be mounted on the dome to power and communicate with the flatfield projector. The Flat Field Central Projector is a part of the calibration system for the Rubin Telescope. This tech note describes the Flat Field Central Projector electronics system, requirements, and design. All supporting documentation is included. The electronics system was partially designed by Parker Fagrelius and the design was completed and built by Antanasia Jones in December 2023. 

Overview
========

In the center of the calibration screen, a box will be installed that will include the optics to project both white light (LEDs) and the laser. Since the Central Projector will be placed in the center of the calibration screen, there is a very stringent volume restriction on the projector box with a maximum volume of 500mmX500mmX800mm. Since many electronics are needed to power and operate the projector, a separate electronics cabinet for the projector is being utilized and will be placed underneath the projector box on the back of the calibration screen. 

The projector will need to switch between the LED system and the Laser-fed system. The fiber for the laser will come from the laser enclosure located elsewhere in the dome. Two LEDs will be used for most bands, where a dichroic will be used to combine the light from both LEDs. 

.. figure:: /_static/Projector_Mounting.PNG
 :name: Projector Mounting
 :target: ../_images/Projector_Mounting.PNG
 :alt: Projector Mounting
 :scale: 50 %

Requirements
============

Operational Requirements
------------------------
-	Able to deliver light from the Laser or LED at a variety of wavelengths
-	System needed for monitoring output light: luminance and spectral
-	The projector will need to be aligned to the calibration screen laterally and radially and in the tip and tilt to specific degrees. 

Power Requirements
------------------
The Electronics cabinet will be supplied with 220V, 50 Hz, 16 Amps, single phase, AC power. The Collimated Beam Projector (CBP) Electronics Cabinet will provide power and Ethernet to the Central Projector System due to a limited amount of power outlets available through the contractor. This set up does not affect the operation of the Central Projector since the Central Projector and the Collimated Beam Projector will not be operating at the same time. 

.. note::

  Since the Central Projector and electronics will receive power from the CBP electronics cabinet, when the CBP electronics cabinet is down or under maintenance the power to the Central Projector will also be off. 

The maximum power, when all the components are operating at full capacity simultaneously, for the entire central projection system was calculated as approximately 730W. The standby power, when the system not in use, but still powered, was calculated as approximately 180W.

Design
======

.. figure:: /_static/ProjectorBlockDiagram.PNG
 :name: Projector Block Diagram
 :target: ../_images/ProjectorBlockDiagram.PNG
 :alt: Projector Block Diagram
 :scale: 50 %

Projector Enclosure
-------------------
There are 4 main components to the design:

1.	Optical Bench: Exit aperture must be in the center of the envelope

2.	Laser Projector: The optics for the laser projector are aligned with the exit aperture

3.	LED Projector: 2 Types of optics:

-	Collimating Optics: there are six LED subassemblies, each at a different wavelength. We need to pick off light from each of them using a linear stage. This section also includes the collimating optics.

- Converging Optics: This consists of the pick off mirror for the LEDs, a converging lens, a field lens, and then another mirror to send the light up to the exit aperture

4.	Pick Off Mirror: when this mirror is in place, the LED will be projected. When moved, the laser will be projected.

The projectors electronics include:

- Light Source Vertical Stage: `LRQ150P <https://www.zaber.com/products/linear-stages/X-LRQ-DE/specs?part=X-LRQ150AP-DE51>`__, Selects between the LED and Laser Projector
- Laser Goniometer: `OMG-T4A <https://www.zaber.com/products/optical-mounts/OMG/specs?part=OMG-T4A>`__, Gimbal for laser output. Adjusts the tip/tilt of the fiber. Two-axis control via Universal Controller, X-MCC4. 
- Laser Focus Stage: `LSM050A-PTB2 <https://www.zaber.com/products/linear-stages/X-LSM/specs?part=X-LSM050A>`__, Sets collimation distance as a function of wavelength. Moves collimated lenses relative to the output of the fiber. 
- LED Linear Stage: `LRQ300AL <https://www.zaber.com/products/linear-stages/X-LRQ-DE/specs?part=X-LRQ300AL-DE51>`__, Enables picking off light from different LED Projectors 
- Optical Components Stages: `LSA25-T4-MT10T3 <https://www.zaber.com/products/optical-mounts/OMG/specs>`__  
- LEDs: Uses multiple LEDs of varying wavelengths to create a “white light” projector. A dichroic will be used to combine the light from LEDs.

  More information on the Multi-LED Projector found `here <https://confluence.lsstcorp.org/pages/viewpage.action?spaceKey=LTS&title=Mulit-LED+Projector>`__. 

.. figure:: /_static/ProjectorElectronics.png
 :name: Projector Electronics
 :target: ../_images/ProjectorElectronics.png
 :alt: Projector Electronics
 :scale: 50 %

Electronics Cabinet
-------------------
The Electronics cabinet was designed to run on 220VAC, 50Hz, 1 Phase, 16A. The function of the electronics cabinet is to power and control the central projector electronics (Linear stages, LEDs, etc.) within the projector, and power and control the meters used to monitor the light coming from the projector.

The electronics cabinet must be powered down via a disconnect switch on the door to open the cabinet. Power will be shut down to all the electronics in the cabinet and the central projector when the cabinet is opened. 

The Electronics Cabinet includes a PDU, an Electrometer, two Fiber Spectrographs, a Network Switch, an Ethernet to Serial Server, an Embedded SBC, a LabJack, a 4-axis Drive Controller for the Projector stages, ten Solid State Relays, and ten LED Drivers. There are 5V, 12V, 15V, 24V, and 48V AC to DC power supplies that are all powered through the PDU.

.. figure:: /_static/Projector Panel 7.jpg
 :name: Projector Panel 7
 :target: ../_images/Projector Panel 7.jpg
 :alt: Projector Panel 7
 :scale: 50 %

Component Description
=====================

Fiber Spectrographs
-------------------
The fiber spectrographs used are an  `Avantes SenseLine AvaSpecULS2048x64TEC <https://www.einstinc.com/wpcproduct/avantes-senseline-avaspec-uls2048x64tec-fiber-optic-spectrometers/>`__, with a wavelength range of 200-1160 nm. An optical fiber runs from each of the two fiber spectrographs and monitors the light from the spectral output of the light sources, one monitors red light and the other monitors blue light.

The fiber spectrographs are controlled via USB that runs directly from the fiber spectrograph to an embedded SBC in the electronics cabinet. It can be commanded by the ts_fiberspectrograph CSC. More information can be found at https://ts-fiberspectrograph.lsst.io.

Electrometer 
------------
The electrometer used is the `Keithley 6517B <https://www.testequipmentdepot.com/media/akeneo_connector/asset_files/6/5/6517b_datasheet_5012.pdf>`__. It monitors the relative brightness of the light sources in the projector.  

The electrometer is controlled via a Serial Device Server, the MOXA Nport 5100. 

The electrometer can be run in charge or current mode. The Electrometer is commanded by the ts_electrometer CSC, which has its configuration stored in ts_config_ocs. See the `XML documentation <https://ts-xml.lsst.io/sal_interfaces/Electrometer.html>`__ for more information.

The electrometer sits in the electronics box and the cable from the photodiode is routed to the Projector enclosure.
Information on the electrometer and photodiode can be found on Docushare `here <https://docushare.lsst.org/docushare/dsweb/View/Collection-5176>`__

Ethernet Network Switch
-----------------------
Cisco Catalyst `IE-3100-4T2S-E <https://www.cisco.com/c/en/us/products/collateral/networking/industrial-switches/catalyst-ie3100-rugged-series/catalyst-ie3100-rugged-series-ds.html>`__. 4-Port Ethernet, one port for input Ethernet and 3 ports for output Ethernet. The Network Switch is powered at all times except when the disconnect switch on the door of the electronics cabinet is ‘OFF’ or power is otherwise lost to the electronics cabinet. Supplies Ethernet ports for the Ethernet-to-Serial server, PDU, and LabJack. 

.. note::

  The Network Switch does not have enough power for POE. 

Ethernet-to-Serial Server
-------------------------
`Moxa 5450I-T <https://cdn-cms.azureedge.net/getmedia/1bee66c9-d622-4f16-8024-f22a271a2bdf/moxa-nport-5400-series-datasheet-v2.1.pdf>`__, 4 port Eth to Serial server. Port 1 is RS232 for communications with the Zaber electronics and port 2 is RS485 communications to the Electrometer. Ports 3 and 4 are reserved for future expansion. Information on the Moxa setup can be found `here <https://ts-electrometer.lsst.io/developer-guide/developer-guide.html#moxa-serial-to-ethernet-converter>`__.

Embedded SBC
------------
The embedded SBCs are `ADL1500 Embedded Solutions <https://www.adl-usa.com/wp-content/uploads/2017/01/ADLEPC-1500-Datasheet-Final.pdf>`__.They are to be connected to the Ethernet via the Network switch. These devices received Ethernet from the Collimated Beam Projector cabinet. The SBC is used to communicate with and control the fiber Spectrographs via USB connections. 

Power Distribution Unit (PDU)
-----------------------------
Power distribution unit is the `Raritan PX3-5288R <https://cdn.raritan.com/product-selector/pdus/PX3-5288R/PX3-5288R-spec.pdf>`__. Port 2 is used for the Electrometer. Ports 3 and 4 are used for Fiber Spectrographs. Port 5 is for powering the Moxa, LED Drivers and LabJack. Port 6 is for powering the projector controller and stages. Only the Network Switch and the Embedded SBC are NOT powered through this device. 

LED Drivers
-----------
The LED drivers are the `Thorlab LEDD1B <https://www.thorlabs.com/newgrouppage9.cfm?objectgroup_id=2616&pn=LEDD1B>`__ T-Cube LED Drivers. These are used to drive power to the LEDs in the projector. The LED Drivers typically will function at max power to operate the LEDs in the projector. 

There are ten LED Drivers, each connected to a solid-state relay (SSR). Each SSR is connected to the LabJack, which is programmed to send a signal to the SSR that corresponds with the LED Driver(s)/LED(s) that are to be turned on. 

Each LED Driver will be funcitoning in modualtion mode, which allows for the LEDs that are selected to be adjusted in brightness. The LabJack is used to send a signal, via a BNC cable, to no more than two LED Drivers at a time (at most two LEDs will be on at a time in the projector). 

Arc Lamp
--------
The spectral Calibration source (arc lamp) is an `AVALight-Cal-Mini <https://www.avantes.com/content/uploads/2020/11/DS-LS-AvaLight-CAL-200702.pdf>`__. Attached to the Arc lamp is a DB15 board to connect the I/O pins to the LabJack, which turn on and off the arc lamp. 

LabJack
-------
This `LabJack T4 <https://files.labjack.com/datasheets/LabJack-T-Series-Datasheet.pdf>`__ is used to send signals to the SSRs to switch on and off the LEDs, and sends a signal to the Spectral Arc Lamp to switch it on and off. Connected to the LabJack is a DB15 Board, which allows for extra pins for the ten SSRs to connect to the LabJack. 

4-axis Universal Controller
---------------------------
This is a controller is an `X-MCC4 <https://www.zaber.com/products/controllers-joysticks/X-MCC/specs?part=X-MCC4>`__ Zaber controller. This controls the Zaber electronics stages in the projector. The stages are daisy chained together and are all powered through the X-MCC4. Zaber electronics include a Laser Goniometer, Optical Component Stage, LED Linear Stage, Laser Focus Stage, and a Vertical Stage.

Operation
=========

.. table:: The PDU outlet numbering

   +--------+------------------------------+
   | Outlet | Name                         |
   +--------+------------------------------+
   | 9      | Electrometer                 |
   +--------+------------------------------+
   | 10     | Moxa/LabJack/LED Drivers/    |
   |        | Projector Controller & Stages|
   +--------+------------------------------+ 
   | 11     | Blue Spectrograph            |
   +--------+------------------------------+   
   | 12     | Red Spectrograph             |
   +--------+------------------------------+    
     
   
.. table:: IP Addresses

   +----------------+-------------------+---------------+-------------------+-----------------+
   | Component      | MAC address       | DHCP name     | Static IP Address | TTS IP Adddress | 
   +----------------+-------------------+---------------+-------------------+-----------------+
   | PDU            |                   |               |                   |                 |
   +----------------+-------------------+---------------+-------------------+-----------------+
   | Moxa           |                   |               |                   |                 |
   +----------------+-------------------+---------------+-------------------+-----------------+
   | Network Switch |                   |               |                   |                 |
   +----------------+-------------------+---------------+-------------------+-----------------+
   | LabJack        |                   |               |                   |                 |
   +----------------+-------------------+---------------+-------------------+-----------------+
   | Embedded SBC   |                   |               |                   |                 |
   +----------------+-------------------+---------------+-------------------+-----------------+
   | Electrometer   |                   |               |                   |                 |
   +----------------+-------------------+---------------+-------------------+-----------------+
   | X-MCC4         |                   |               |                   |                 |
   +----------------+-------------------+---------------+-------------------+-----------------+

Additional Documentation
========================

Initial documentation for the Central Projector system was done in `Confluence <https://confluence.lsstcorp.org/pages/viewpage.action?spaceKey=LTS&title=Central+Projection+System+Electronics>`__, and further details on the design and specifications can be found `here <https://rubinobs.atlassian.net/wiki/spaces/LTS/pages/50084494/Central+Projection+System+Electronics>`__. 

Docushare: https://docushare.lsst.org/docushare/dsweb/View/Collection-10012 

Docushare for Projector Enclosure: https://docushare.lsst.org/docushare/dsweb/View/Collection-15446

Docushare for Electronics Cabinet: https://docushare.lsst.org/docushare/dsweb/View/Collection-15975


See the `reStructuredText Style Guide <https://developer.lsst.io/restructuredtext/style.html>`__ to learn how to create sections, links, images, tables, equations, and more.

.. Make in-text citations with: :cite:`bibkey`.
.. Uncomment to use citations
.. .. rubric:: References
.. 
.. .. bibliography:: local.bib lsstbib/books.bib lsstbib/lsst.bib lsstbib/lsst-dm.bib lsstbib/refs.bib lsstbib/refs_ads.bib
..    :style: lsst_aa

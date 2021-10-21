## What Does Device Under Test (DUT) Mean?

A device under test (DUT) is a device that is tested to determine performance and proficiency. A DUT also may be a component of a bigger module or unit known as a unit under test (UUT). A DUT is checked for defects to make sure the device is working. The testing is designed to prevent damaged devices from entering the market, which also may reduce manufacturing costs.

A DUT is usually tested by automatic or automated test equipment (ATE), which may be used to conduct simple or complex testing, depending on the device tested. ATEs may include testing performed on software, hardware, electronics, semiconductors or avionics.

## Drivers

三种类型：APO、HSA、EXT

APO: Audio Processing Object

rtk：Realtek

EXT: external 外部的

SWC: 

BT: Bluetooth

QC: QUALCOMM

| Abbreviations | Full Name                                   | More Explanation                                             |
| ------------- | ------------------------------------------- | ------------------------------------------------------------ |
| APO           | Audio Processing Object                     |                                                              |
| BT            | Bluetooth                                   |                                                              |
| EXT           | external                                    | used in the naming of Drivers                                |
| DUT           | device under test                           | a device that is tested to determine performance and proficiency |
| HSA           | **H**ardware **S**upported **A**pplications |                                                              |
| RTK           | Realtek                                     | a fabless semiconductor company which manufactures and sells a variety of microchips globally and its product lines broadly fall into three categories: communications network ICs, computer peripheral ICs, and multimedia ICs |
| **RPC**       |                                             |                                                              |
| QC            | QUALCOMM                                    | an American corporation which creates semiconductors, software, and services related to wireless technology |
| **SWC**       |                                             |                                                              |
| AO            | Audio Optimizer                             | Boost                                                        |
| AR            | Audio                                       | suppress                                                     |
| DTT           | Dolby Tuning Tool                           |                                                              |
| **HLK**       |                                             |                                                              |







## SKU标准

https://confluence.dolby.net/kb/display/CET/DAX3+SKU+definition



## DUT’s Unlock key

https://confluence.dolby.net/kb/display/CET/DAX+DUT+and+Activation+Keys



## USB需要在inf文件中添加设备信息

; Plantronics C3220
 %Device.ExtensionDesc% = DeviceExtension_Install_USB1,USB\VID_047F&PID_C056&REV_0210&MI_00
 ; Jabra EVOLVE LINK MS
 %Device.ExtensionDesc% = DeviceExtension_Install_USB1,USB\VID_0B0E&PID_0305&REV_0310&MI_00


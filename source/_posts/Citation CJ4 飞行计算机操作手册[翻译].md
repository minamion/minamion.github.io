---
layout: citation
title: 'Citation CJ4 飞行管理系统\飞行计算机(FMS -Flight management system)操作手册[翻译 WIP]'
date: 2020-08-31 23:25:32
tags:
---
>本文原文位于[此处](https://forums.flightsimulator.com/t/how-to-citation-cj4-fms-programming-guide/124457)

> 仅适用于 微软模拟飞行2020 是否适用于实际飞行请咨询塞斯纳公司

这是微软模拟飞行2020默认机CJ4的FMS使用手册，由于MSFS2020并非完全体，因此本手册将随时更新

注：波音787中的FMS也由柯林斯制造。即使它们看上去完全不同，也可以应用某些相同的操作逻辑
<!-- more -->
* * *
## FMS操作
### 输入数据

Here is a sample page. Note the area in light green. Anytime you see a blank square box like this, it means it is a required field. In this case, airport identifiers.

The yellow circles are called Line Select Keys. Sometimes abbreviated LSK. In this guide, I may mention LSK L6\. That would be the left side, 6th key down.

The red area is called the Scratchpad. This version of the Collins FMS works by typing into the scratchpad, and then “pasting” what you typed into the required field up above. You may also copy some fields from up above, down into the scratchpad using the line select keys.

To delete an item, first press the CLR DEL key in the lower right side. This puts “CLR” into your scratchpad. Then you paste CLR on top of what you want to delete using the line select keys (LSK). Note that there is a bug and you cannot delete your origin or destination in the sim.

![FPLN - Blank - Copy](https://forums.flightsimulator.com/uploads/default/original/3X/4/7/4754f0ab6f2d5eb42cc44e49ce78e7c3cdf1768a.jpeg)

### 主要按钮

The main buttons that you will use are circled in red. Normally you would use the IDX key to return to the Index page, but there is currently a bug that requires you to use the DISPL MENU key to go to the index. This can be confusing, so please report this to [ZenDesk]  
([https://flightsimulator.zendesk.com/hc/en-us <span class="badge badge-notification clicks" title="8 clicks">8</span>](https://flightsimulator.zendesk.com/hc/en-us)), as the more attention it gets the better.

![Page header](https://forums.flightsimulator.com/uploads/default/original/3X/7/b/7b132fb0016b061f2732251f7b7267afeaed75f3.jpeg)

Also, take note of the page header. Especially for indications that there are additional pages to be displayed. In this example, we are on the FPLN ROUTE page, and there are 4 total pages with data on them. Advance to the next page using the NEXT button on the far right side.

![FPLN - Blank buttons](https://forums.flightsimulator.com/uploads/default/original/3X/0/4/0461b28e436380b53680bf011787e51169fee83c.jpeg)



* * *

### FMS 设置和初始化

The first screen that you will see on startup is the STATUS page (incorrectly labeled IDENT). This page is where you will check the date of the Nav database (AIRAC cycle).

Pressing the R6 LSK (Right line select key next to POS INIT) will take you to the next step.

While the CJ does not have any IRS to align, it is still recommended to set the GNSS startup position using a copy and paste procedure listed below.

Push LSK R4 (Right side, 4th down) - labeled with a red 1 in the screenshot  
This copies the Lat/Long into the “scratchpad”  
Now push LSK R5 to paste the position into the empty boxes.

To move onto the next part, push the FPLN button below the screen (the R6 softkey next to Route does not work for some reason)

![POS INIT 12](https://forums.flightsimulator.com/uploads/default/original/3X/6/2/627dfc4d075a2147669ff1a93a59a8778afb65ac.jpeg "POS INIT 12")
###  输入飞行计划

The main flight plan is entered from the FPLN page (until Datalink gets modeled!). Type the 4 letter airport identifier into the scratchpad (circled in red) and then paste it into the Origin and Destination fields using the L1 and R1 line select keys. _Note:_ Currently a bug that won’t allow you to clr/delete these fields. So make sure you enter what you want .

![FPLN - TEB to PBI](https://forums.flightsimulator.com/uploads/default/original/3X/8/6/869fea0a60bc391e32e78aa257560f3aaf25b714.jpeg "FPLN - TEB to PBI")

###  加载离场程序 (SID)

Next go to the DEP / ARR page to load any applicable departure procedures (SID), if available for your airport. (Any missing procedures from the database should be reported to [ZenDesk ](https://flightsimulator.zendesk.com/hc/en-us))

After pressing DEP / ARR select the departure airport on the left using LSK 1\. If you do not see both the departure and arrival airport on this page, check the main flight plan origin and destination fields from the FPLN page.

![dep arr 1](https://forums.flightsimulator.com/uploads/default/original/3X/a/4/a4b16c1271ac791f00d9df960070a04b2789983c.jpeg)

Choose your Departure procedure (SID), transition, and runway. Note that once you select a SID it will hide the runways that do not apply to that departure procedure (and vice-versa)

![DEP ARR RUUDY6](https://forums.flightsimulator.com/uploads/default/original/3X/4/2/423dad8e2a3b6edc6384d8486b9d0d8a6d4c7031.jpeg "DEP ARR RUUDY6")

###  完成飞行计划

Now go back to the FPLN (Route) page. It will show the departure procedure on the left. Enter the remaining waypoints one at a time using the scratch pad, and paste them into the right side. (Example below shows ELVAE intersection entered)

![Route - first waypoint](https://forums.flightsimulator.com/uploads/default/original/3X/1/f/1f7abe638fb3d772100dc18da2f1746e9a1914ce.jpeg "Route - first waypoint")

Note the left column is labeled VIA and the right column is labeled TO. Normally airways can be entered in the left side, but the sim is picky about what entry and exit points you can use to enter an airway. Please report a bug using ZenDesk if you encounter one.

![Route - airway](https://forums.flightsimulator.com/uploads/default/original/3X/5/d/5d52d1bb5750132a0bba0c46429924bd47805def.jpeg "Route - airway")

###  重复航点

Sometimes when entering a waypoint you may see a box like this:

![Route - duplicate waypoint](https://forums.flightsimulator.com/uploads/default/original/3X/3/1/31136df9d3c53b09a75a89f9a7e45bd62cb7b5d4.jpeg "Route - duplicate waypoint")

This means there are multiple waypoints in the nav database that have the same identifier. Pick the correct one (normally this is the top one, which should be the closest)

###  路线回顾

Pressing the legs page will allow us to review what we entered in the flight plan page. For the most part, all modifications after takeoff will be done from the LEGS page, and not the FPLN page. This is also where you enter VNAV altitudes, once implemented. Due to a bug, occasionally the route page may look like this (not sure why):

![Legs Page - Review](https://forums.flightsimulator.com/uploads/default/original/3X/7/4/74e3acd85f7c42af8f54a071562d6f75310730b5.jpeg "Legs Page - Review")

###  起飞和着陆程序

The FMS has the ability to compute takeoff and landing speeds based on weight and weather conditions. Unfortunately this is not modeled in the sim. You can, however, use the PERF page to enter manually calculated V-speeds (the calculated speeds aren’t accurate). There are 2 caveats however. You can only enter takeoff speeds (not landing). And due to a bug they do not come up when pressing the PERF button. Instead you must hit DISPL MENU and then the L5 Line Select Key for Takeoff.

Form more info on takeoff or landing speeds, see the Performance Numbers section below.

![PERF - TO](https://forums.flightsimulator.com/uploads/default/original/3X/5/b/5b9d43b628eebb4995892e66181efc0f4d2dbb51.jpeg "PERF - TO")

### 加载进场程序 (STAR)

If the destination airport has an arrival procedure, it is loaded in the same way as the departure procedure (except using the right side after pushing the DEP ARR button)

![DEP ARR - STAR](https://forums.flightsimulator.com/uploads/default/original/3X/d/5/d5babf505c6141651b1f53a0bac19602b7d867c5.jpeg "DEP ARR - STAR")

### 直飞模式

To go direct to a new waypoint or one that is in your current route, use the DIR key on the left side. Then you can either type in a new waypoint in the scratchpad and paste it into L1\. Or, if the waypoint is already on your route you can select it to bring it into the scratchpad, and paste it into L1\. Note you may have to use the NEXT key to pick waypoints further down on your route.

![Direct To](https://forums.flightsimulator.com/uploads/default/original/3X/e/b/eb9d928d8998d15cce8899cc4fc499d04c4a82fc.jpeg "Direct To")



* * *
## 附录
### 调整无线电通信和导航频道

All radio tuning in the sim is done through the TUN page of the CDU (FMS). This includes radios for BOTH communications and navigation, such as an ILS. Press the TUN button to bring up the following page:

![FMS Tune](https://forums.flightsimulator.com/uploads/default/original/3X/e/8/e82ec62e43bab787a3daf0c1dac6d76298d17dfe.jpeg "FMS Tune")

In the sim, you must use a decimal point, example 121.5 will work, but 1215 will not. Also, after loading an approach in the FMS, the sim will not auto tune the ILS frequency and set the inbound course like the real airplane.

ADF Tuning is done on page 2 of the Radio Tuning page.

### 调整PFD / MFD显示和范围

This section is a work in progress, but to get the ball rolling, the left side primary flight display (PFD) is mostly controlled using the control panel above it. The button labeled PFD menu will allow you to change the format and range of the PFD. You can also change the altimeter units (Hpa, inches, meters). Note that changing the range also affects the center MFD as well.

To adjust the MFD map orientation, etc, use the LWR MENU button on the control panel under the MFD. The knobs in the screenshot (inner and outter) can be used within the menu on the PFD/MFD.

![Map Scale](https://forums.flightsimulator.com/uploads/default/original/3X/e/e/eea62a4b022951e1a7581b8ae1b84f72b3c8a6c9.jpeg "Map Scale")

### AP/自动驾驶仪

The Autopilot section is a major work in progress. A few quick notes however.

*   TO/GA mode is not included at this time.
*   Arming HDG and PIT is recommended for takeoff
*   Can climb in VS or PIT (or FLC).
*   FLC maintains selected vertical speed by adjusting the pitch.
*   The CJ does not have an Autothrottle (the speed bug is for reference and FLC adjustment)
*   VNAV is not implemented at this time

To Capture an ILS, you must change the NAV SRC from FMS 1 to VOR/LOC using the PFD menu button on the control panel above the PFD. Also, no autopilot will capture the glideslope from above (if you are too high). You must use VS to dive down and capture it in that scenario.

Do not press the ALT button! About the only exception is if you want to immediately stop your climb / descent at the current altitude. General order is to set the altitude preselector first, then pick a vertical mode (VS, PIT, FLC) and then adjust your rate (and engage the autopilot)

### 性能参数

这是一些在MSFS中应该起作用的参数，不是现实中的参数。

#### 起飞速度 

_17,100 lbs (Flaps 0°)_  
_Sea Level - 15° C temp_

V1 108  
VR 115  
V2 128  
Distance 3920’ takeoff roll

#### 起飞速度 - 17,100 lbs (襟翼 15°)

V1 99  
VR 104  
V2 117  
Distance: 3410’ takeoff roll
127kts 时收起襟翼

#### 爬升
Normal Climb: 240 kts transitioning to Mach 0.64  
Single Engine Climb: 140 kts (VENR)

#### 巡航:
FL410 (ISA Temp)  
99.0% N1  
Fuel Flow: 1154 lbs / hr total  
220 kts indicated / 431 true (Mach .75)  
Range: 37 nm / 100 lbs of fuel (no wind)

#### 下降: (no wind)  
21 min / 130 nm at 2,000 feet per minute VS.  
17 min / 100 nm at 3,000 feet per minute VS.

#### 进近 
进近速度 Ref + 10 kts  
进近设置: 55-60% N1 for 200 kts, configuring gear and flaps to slow to approach speeds  
盘旋进近: 最大襟翼

进近功率设置: (once fully configured inbound on glide slope)  
55% - 2 engine  
65% - 1 engine

#### 着陆速度- VREF (襟翼 35°):

113 kts at 15,660 lbs (最大着陆重量)  
98 kts at 12,000 lbs



* * *

# Validating self-adaptation across a sUAS System-of-Systems

<br>


<img align="right" width="220" src="https://github.com/SAREC-Lab/PuDZ/blob/main/images/drones.PNG">

<p align="justify">
The use of small autonomous Uncrewed Aerial Systems (sUAS) for Emergency Response requires rapid deployments into shared operational environments which we refer to as ``Pop-up Drone Zones'' (PuDZ). PuDZ represents a System of Systems (SoS), in which individual systems provide services such as air traffic control, environmental modeling, and support for sUAS autonomy. <br>
Each system needs the ability to configure itself dynamically at the start of the mission, and self-adapt throughout the mission in response to environmental changes, emergent problems, and changes in the overall mission status. Each system is self-managed, using its own local MAPE-K loop, and can, therefore, adapt independently; however, adaptations in one system can have a trickle-over effect to other systems. <br><br>
The tests reported on this page were conducted with four HX-10 drones (shown on the right) and were used to illustrate and validate various cross-system self-adaptation scenarios with physical and/or simulated sUAS. 
 </p> 
  
<br>

---

<br>


| Test         | Description     | Pattern | Triggering System | 
|:--------------:|-----------|:------------:|------------|
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; [T1](README.md#t1) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Mission state transition during normal operation   |&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; [A](pattern.md#pa)      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  |sUAS (Auton. Pilot) &nbsp;&nbsp;&nbsp;&nbsp; |
| [T2](README.md#t2) |sUAS-A detects and tracks a person | [A](pattern.md#pa)        |sUAS (Comp. Vision) |
| [T3](README.md#t3) | sUAS-A detects and sUAS-B tracks person  | [B](pattern.md#pb)         |sUAS (Comp. Vision)|
| [T4](README.md#t4) |sUAS misses heartbeat from GCS  | [A](pattern.md#pa)         |sUAS (Monitor) |
| [T5](README.md#t5) | EDS and Air-Leaser adapt due to high winds  | [C](pattern.md#pc)         |EDS (Weather) |
| [T6](README.md#t6) | Air-leaser adapts to grid layout   | [C](pattern.md#pc)        |Air-Leaser |
| [T7](README.md#t7) |Compass interference onboard sUAS   | [C](pattern.md#pc)       |sUAS (Analytics) |
| [T8](README.md#t8) |Human requests extended PuDZ Boundaries | [C](pattern.md#pc)       |EDS (boundaries)|
| [T9](README.md#t9) | Ill-formed mission detected. Mission aborted   | [C](pattern.md#pc)        |SoS Policy Manager  |
| [T10](README.md#t10) | FAA Part 107 flight regulation violation  |[C](pattern.md#pc)       |Runtime Monitor |


##### Note: For help in interpreting mission specifications please see [this](https://github.com/SAREC-Lab/PuDZ/blob/main/mission-specs/missions.md) link.

<br>

---

### :mag_right: T1: Mission state transition during normal operations
<a name="t1"></a>
<img align="right" width="200" src="https://github.com/SAREC-Lab/PuDZ/blob/main/images/PhasedCircle.PNG">
<p align="justify">
The test validates that the sUAS is able to transition effectively through a series of states. This is an example of internal system self-adaptation. The sUAS uses an internal MQTT system to coordinate transitions through the mission states. In particular, it demonstrates a 'phased circle', meaning that the drone flies around a specified part of a circle (as developed to support an image collection project at high altitude and distance). This test demonstrates transitions between many states including arming, takeoff, hover, fly-to-waypoints, phased-circle, land, and disarm. 
  </p>
  
- Video: [T1 Field test video](https://youtu.be/MmwdYf4_4zw)
- Flight Log: [T1 Field test flight log](https://logs.px4.io/plot_app?log=d5b39fa5-38e2-402b-87c5-f30f98087f2c)
- Mission Specification: [T1 JSON Specification](mission-specs/mission_spec_T1.json)

--- 

### :mag_right: T2: sUAS-A detects and tracks a person
<img align="right" width="200" src="https://github.com/SAREC-Lab/PuDZ/blob/main/images/T2-Picture.PNG">
<a name="t2"></a>
<p align="justify">
The test validates that the sUAS can transition states from 'search' to 'survey' when the onboard computer vision pipeline detects a person. One the person is detected, the sUAS computes the persons geolocation and circles around them. We are still working on accurate geolocation and have a solution ready to test once weather becomes warm.  In this video, the adaptations work as intended.
 </p>

- Video: [T2 Field test video](https://youtu.be/FCtVVyNWe7c)
- Flight Log: [T2 Field test flight log](https://logs.px4.io/plot_app?log=c10160a1-68fc-4d05-a122-413930471b41)
- Mission Specification: [T2 JSON Specification](mission-specs/mission_spec_T2.json)

--- 

### :mag_right: T3: sUAS-A detects and sUAS-B tracks person
<a name="t3"></a>
<img align="right" width="200" src="https://github.com/SAREC-Lab/PuDZ/blob/main/images/test1.PNG">
<p align="justify">
In this version of the test, we mimic sUAS-A detecting a person by publishing the coordinates of the found person to MQTT as:
(MESSAGE HERE). sUAS-B subscribes to this topic and self-adapts from `flying' state to 'circle' state around the coordinates.
</p>

- Video: [T3-Video](https://youtu.be/MmwdYf4_4zw)  
- Flight Log
- Mission Specification: [T3 Specification](mission-specs/mission_spec_t3.json)

--- 
<a name="t4"></a>
### :mag_right: T4: sUAS misses heartbeat from GCS
<p align="justify">
In this test, we added a new failsafe state (not shown in the JSON file as it is a default state for all states and therefore doesn't need to be specified by the user). When the heartbeat is lost then the drone transitions into heartbeat hover, and eventually if the heartbeat is not restored, it transitions into RTL.
 </p>
 

- Video: [T4-Video](https://youtu.be/JwX7aYFQkjA)
- Flight Log: (Test executed correctly, but in this version it introduced a strange character into the flight log making it unreadable. New version is lined up for testing in the Spring).
- Mission Specification: [T4 JSON Specification](mission-specs/mission_spec_t4.json)

--- 

### :mag_right: T5: EDS and Air-Leaser adapt due to high winds
<a name="t5"></a>
<p align="justify">
In this test we mimic the adaptation of the EDS due to high winds. We publish a high-wind alert, and the air-leaser adapts by increasing the separation distances between sUAS. 
 </p>


#### Air-leaser
- Video: [T5-Video](https://youtu.be/-BxXdtNNgw0) (Two sUAS flight, but no videos available of the air-leaser tests below.)

#### Air-Leaser Basic Test #1

<p align="justify">
Drones fly to opposite ends of the runway, hover for 20 seconds, and then request air-space to fly near to the current location of the other drone. The expected outcome is that drones should deadlock and be stuck in hover. Both drones should continue requesting an air lease from the ground service and continue to be denied indefinitely until pilot takes over.
 </p>
 
- Mission Specification: 
  - [Drone-A JSON Specification](https://github.com/SAREC-Lab/PuDZ/blob/main/mission-specs/mission_spec_T6a.json)
  - [Drone-B JSON Specification](https://github.com/SAREC-Lab/PuDZ/blob/main/mission-specs/mission_spec_T6b.json)

#### Air-Leaser Test #2.
<p align="justify">
Four drones are lined up South of the runway approximately 15-20 meters apart.  Each one is given a flight plan to take-off, fly south to a waypoint, hover for 20 seconds, and return home.  We expect to see all drones take off sequentially as they request leases, since they are positioned at spots greater than 21 meters.  If there is an airlease error, they will not all take off.  By progressively adapting the air-leaser's spacing plan, different outcomes are observed in terms of which sUAS take off in which order.
</p>
  
- Mission Specification: 
  - [Drone-RED](https://github.com/SAREC-Lab/PuDZ/blob/main/mission-specs/mission_spec_T6_RED.json)
  - [Drone-BLUE](https://github.com/SAREC-Lab/PuDZ/blob/main/mission-specs/mission_spec_T6_BLUE.json)
  - [Drone-GREEN](https://github.com/SAREC-Lab/PuDZ/blob/main/mission-specs/mission_spec_T6_GREEN.json)
  - [Drone-PURPLE](https://github.com/SAREC-Lab/PuDZ/blob/main/mission-specs/mission_spec_T6_PURPLE.json)

--- 

### :mag_right: T6: Air-leaser layout adaptation
The air-leaser adapts its layout due to high congestion. We have tested this in a low-fidelity simulator and not with the PX4 physics engine. 
<a name="t6"></a>

--- 

<img align="right" width="350" src ="https://github.com/SAREC-Lab/PuDZ/blob/main/images/realtime.png">
<a name="t7"></a>

### :mag_right: T7: Compass interference onboard sUAS

<p align="justify">

Onboard anomaly detection was tested for vibration with the high-fidelity Gazebo simulator. We demonstrated that it could be detected in real-time and lead to adaptations e.g., reduce throttle, LOITER, LAND. Currently being ported to physical sUAS. <BR> <BR> Onboard anomaly detection courtesy of Md Nafee Al Islam. 
  </p>
  
  <br>


--- 

### :mag_right: T8: Human requests extended PuDZ Boundaries
<img width="400" align="right" src="https://github.com/SAREC-Lab/PuDZ/blob/main/images/DR-GUI.png">
This tests whether a change in PuDZ boundaries causes routes to be adapted.  The image shows the GUI that is currently used to modify a search region which delimits regional searches. The fully self-adaptive solution is still under development as we currently have not implemented route reconfigurations during flight. The autonomous pilot has been designed to self-adapt routes, but some additional development and test is needed for full validation in the field.
<BR>
<BR>
<a name="t8"></a>
<BR>

--- 

### :mag_right: T9: Ill-formed mission detected
(To do: upload screen shot)
<a name="t9"></a>

--- 

<a name="t10"></a>
### :mag_right: T10: sUAS hits geofence and flies off course at high altitude
<img align="right" width="200" src="https://github.com/SAREC-Lab/PuDZ/blob/main/images/highflight.png">
<p align="justify">
This `test' was accidental. It was the result of several compounding errors and has been officially reported to the NASA sUAS incident service due to the high altitudes (over 400ft AGL). We had set up a geofence, but for some reason the geofence action was re-set to 'no action'. When the sUAS hit the geofence, it transitioned to STABILIZED mode and control was ceded from the onboard autopilot to the RPIC (human pilot). The throttle was very slightly above neutral. Therefore, the sUAS started ascending and flew in the direction of the prevailing wind. Retroactively we are developing a monitor to check for excessive altitude and adapt behavior to RTL.
</p>

- Video: 
- Flight Log: [T10-Flight Log](https://logs.px4.io/plot_app?log=7c381b16-a107-4268-9a9c-bfbb3b1575ae)
- Mission Specification: [T10 Specification](mission-specs/mission_spec_T10.json)

---


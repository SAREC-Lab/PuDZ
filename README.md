# PuDZ SoS  
## ![](https://placehold.co/15x15/f03c15/f03c15.png) Note: we are in process of uploading the correct files!!! 
We expect to have all files uploaded by Wednesday, February 8th. Please come back in a couple of days. 


| Test         | Description     | Pattern | Triggering System | 
|:--------------:|-----------|:------------:|------------|
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; [T1](README.md#t1) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Mission state transition during normal operation   |&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; [A](pattern.md#pa)      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  |sUAS (Auton. Pilot) &nbsp;&nbsp;&nbsp;&nbsp; |
| [T2](README.md#t2) |sUAS-A detects and tracks a person | [A](pattern.md#pa)        |sUAS (Comp. Vision) |
| [T3](README.md#t3) | sUAS-A detects and sUAS-B tracks person  | [B](pattern.md#pb)         |sUAS (Comp. Vision)|
| [T4](README.md#t4) |sUAS misses heartbeat from GCS  | [A](pattern.md#pa)         |sUAS (Monitor) |
| [T5](README.md#t5) | Bad weather triggers adaptation of EDS  | [C](pattern.md#pc)         |EDS (Weather) |
| [T6](README.md#t6) | Air-leaser adapts to grid layout   | [C](pattern.md#pc)        |Air-Leaser |
| [T7](README.md#t7) |Compass interference onboard sUAS   | [C](pattern.md#pc)       |sUAS (Analytics) |
| [T8](README.md#t8) |Human requests extended PuDZ Boundaries | [C](pattern.md#pc)       |EDS (boundaries)|
| [T9](README.md#t9) | Ill-formed mission detected. Mission aborted   | [C](pattern.md#pc)        |SoS Policy Manager  |
| [T10](README.md#t10) | FAA Part 107 flight regulation violation  |[C](pattern.md#pc)       |Runtime Monitor |

---

### :mag_right: T1: Mission state transition during normal operations
<a name="t1"></a>
The test validates that the sUAS is able to transition effectively through a series of states. This is an example of internal system self-adaptation. The sUAS uses an internal MQTT system to coordinate transitions through the mission states. In particular, it demonstrates a 'phased circle', meaning that the drone flies around a specified part of a circle (as developed to support an image collection project at high altitude and distance). This test demonstrates transitions between many states including arming, takeoff, hover, fly-to-waypoints, phased-circle, land, and disarm. 
- Video: [T1 Field test video](https://youtu.be/MmwdYf4_4zw)
- Flight Log: [T1 Field test flight log](https://logs.px4.io/plot_app?log=d5b39fa5-38e2-402b-87c5-f30f98087f2c)
- Mission Specification: [T1 JSON Specification](mission-specs/mission_spec_t1.json)

--- 

### :mag_right: T2: sUAS-A detects and tracks a person
The test 
<a name="t2"></a>
- Video: [T2 Field test video](https://youtu.be/FCtVVyNWe7c)
- Flight Log: [T2 Field test flight log](https://logs.px4.io/plot_app?log=c10160a1-68fc-4d05-a122-413930471b41)
- Mission Specification: [T2 Specification](mission-specs/mission_spec_t2.json)

<br>

--- 

<br>

### :mag_right: T3: sUAS-A detects and sUAS-B tracks person
<a name="t3"></a>
<img align="right" width="200" src="https://github.com/SAREC-Lab/PuDZ/blob/main/images/test1.PNG">
In this version of the test, we mimic sUAS-A detecting a person by publishing the coordinates of the found person to MQTT as:
(MESSAGE HERE). sUAS-B subscribes to this topic and self-adapts from `flying' state to 'circle' state around the coordinates.

- Video: [T3-Video](https://youtu.be/MmwdYf4_4zw)  (NOTE: Just a placeholder. I have to find all the right videos and upload!)
- Flight Log
- Mission Specification: [T3 Specification](mission-specs/mission_spec_t3.json)

<br>

--- 

<br>

### :mag_right: T4: sUAS misses heartbeat from GCS
<a name="t4"></a>
- Video
- Flight Log
- Mission Specification: [T4 Specification](mission-specs/mission_spec_t4.json)

<br>

--- 

<br>

### :mag_right: T5: Bad weather triggers adaptation of the Environmental Digital Shadow (EDS)
<a name="t5"></a>
- Video
- Flight Log
- Mission Specification: [T5 Specification](mission-specs/mission_spec_t5.json)


<br>

--- 

<br>

### :mag_right: T6: Air-leaser layout adaptation
The air-leaser adapts its layout in several different ways. First, it can adapt between direct routing and grid-based routing. So far we have tested that in a low-fidelity simulator and not with the PX4 physics engine.  We do not report it here.  Second, it can adapt the spacing between sUAS according to weather, satellite availability, and/or sUAS health. We report two different experiments with the air leaser at vary separation distances.  
<a name="t6"></a>
#### Air-leaser test #1.
- Video
- Flight Log
- Mission Specification: [T6 Specification - DroneA](mission-specs/mission_spec_t6A.json) &nbsp;&nbsp;&nbsp;&nbsp; [T6 Specification DroneB](mission-specs/mission_spec_t6B.json)


<br>

--- 

<br>

### :mag_right: T7: Compass interference onboard sUAS
<a name="t7"></a>
- Video
- Flight Log
- Mission Specification: [T7 Specification](mission-specs/mission_spec_t7.json)


<br>

--- 

<br>


### :mag_right: T8: Human requests extended PuDZ Boundaries
<a name="t8"></a>
- Video
- Flight Log
- Mission Specification: [T8 Specification](mission-specs/mission_spec_t8.json)


<br>

--- 

<br>


### :mag_right: T9: Ill-formed mission detected
<a name="t9"></a>
- Video
- Flight Log
- Mission Specification: [T9 Specification](mission-specs/mission_spec_t9.json)

<br>

--- 

<br>


### :mag_right: T10: FAA Part 107 flight regulation violation
<a name="t10"></a>
- Video
- Flight Log
- Mission Specification: [T10 Specification](mission-specs/mission_spec_t10.json)

---


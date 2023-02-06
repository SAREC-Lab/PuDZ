# PuDZ SoS  
## ![](https://placehold.co/15x15/f03c15/f03c15.png) Note: we are in process of uploading the correct files!!! 
We expect to have all files uploaded by Wednesday, February 8th. Please come back in a couple of days. 


| Test         | Description     | Pattern | Triggering System | 
|--------------|-----------|------------|------------|
| [T1](README.md#t1) | Mission state transition during normal oper.   | A       |sUAS (Auton. Pilot) |
| [T2](README.md#t2) | Mission state transition during normal oper.   | A       |sUAS (Comp. Vision) |
| [T3](README.md#t3) | Mission state transition during normal oper.   | B       |sUAS (Comp. Vision)|
| [T4](README.md#t4) | Mission state transition during normal oper.   | A       |sUAS (Monitor) |
| [T5](README.md#t5) | Mission state transition during normal oper.   | C       |EDS (Weather) |
| [T6](README.md#t6) | Mission state transition during normal oper.   | C       |Air-Leaser |
| [T7](README.md#t7) | Mission state transition during normal oper.   | C       |sUAS (Analytics) |
| [T8](README.md#t8) | Mission state transition during normal oper.   | C       |EDS (boundaries)|
| [T9](README.md#t9) | Mission state transition during normal oper.   | C       |SoS Policy Manager  |
| [T10](README.md#t10) | Mission state transition during normal oper.   |C       |Runtime Monitor |





### T1 Mission state transition during normal operations
<a name="t1"></a>
- Video
- Flight Log
- Mission Specification

### T2 sUAS-A detects and tracks a person
- Video
- Flight Log
- Mission Specification

---

### T3: sUAS-A detects and sUAS-B tracks person

<img align="right" width="200" src="https://github.com/SAREC-Lab/PuDZ/blob/main/images/test1.PNG">
In this version of the test, we mimic sUAS-A detecting a person by publishing the coordinates of the found person to MQTT as:
(MESSAGE HERE). sUAS-B subscribes to this topic and self-adapts from `flying' state to 'circle' state around the coordinates.

- Video [T3-Video][(https://youtu.be/MmwdYf4_4zw)]  (NOTE: Just a placeholder. I have to find all the right videos and upload!)
- Flight Log
- Mission Specification

---

### T4 sUAS misses heartbeat from GCS
- Video
- Flight Log
- Mission Specification

### T5 Bad weather triggers adaptation of the Environmental Digital Shadow (EDS)
- Video
- Flight Log
- Mission Specification

### T6 Air-leaser adapts to grid layout
- Video
- Flight Log
- Mission Specification

### T7 Compass interference onboard sUAS
- Video
- Flight Log
- Mission Specification

### T8 Human requests extended PuDZ Boundaries
- Video
- Flight Log
- Mission Specification

### T9 Ill-formed mission detected
- Video
- Flight Log
- Mission Specification

### T10 FAA Part 107 flight regulation violation
- Video
- Flight Log
- Mission Specification



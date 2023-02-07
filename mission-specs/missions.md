### Mission Specifications

All mission specifications are provided as JSON files. Additional failsafe states are added in addition to the states specified in the JSON file. 
The JSON file is sent to the sUAS which then instantiates its onboard state machine and monitors both local and regional inputs for events that would lead to state transitions.
Each JSON file can be visualized as a state transition diagram.  The following is an example of a search-and-detect mission. Notably, some states are relatively simple whereas others (e.g., search) are supported by onboard AI components.

<img width="460" src="https://github.com/SAREC-Lab/PuDZ/blob/main/images/SearchAndTrack.png">


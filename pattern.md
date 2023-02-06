MAPE-K managed systems within an SoS adapt in several different ways:
 
<a name="pa"></a>
### Pattern A

In the first scenario, ``System A`` receives data from its internal sensors, and after analysis and planning, it adapts accordingly.

<img align="center" width="600" src="/images/ptn-A.PNG">

<br>

---

<br>


<a name="pb"></a>
### Pattern B

In the second scenario ``System A`` does not adapt, however,it still publishes information to a regional data topic to which``System B`` is subscribed to.<br>
While no adaptations have been performed in ``System A``, the regional monitoring data received from ``System A``  ultimately leads to ``B``'s self-adaptation. 

<img align="center" width="600" src="/images/ptn-B.PNG">



<br>

---

<br>
<a name="pc"></a>

### Pattern C

 A similar example is Pattern C however, with the major difference that in this case, both ``System A`` and ``System B`` adapt.<br>
 ``System A``receives local sensor data and adapts in response. It then publishes regional data which causes ``System B`` to adapt.


<img align="center" width="600" src="/images/ptn-C.PNG">


<br>

---

<br>

<a name="pd"></a>
### Pattern D

<img align="center" width="600" src="/images/ptn-D.PNG">


inally, for the last case, a dependency cycle is introduced between two or more self-adaptive systems, meaning that adaptations in one system
trigger adaptions in another system, and vice versa, thereby forming a cycle.  
Cycles are broken when the execution plan of one system no longer publishes data that triggers adaptation.



<br>

---

<br>

# ICL
Intelligent Configurable Light
Documentation WIP

This Repository hosts a nodered flow, lovelace config and homeassistant yaml definitions to support an "Intelligent Configurable Light"

The Flow is HEAVILY inspired from https://www.reddit.com/r/homeassistant/comments/afk6cd/building_smarter_motion_lighting_nodered_finite/ 
I added some additional features.

It was born out of the frustration of Motion Sensor activated light Behaviour in some environments:
- light turning off while user still there (toilet , shower anybody?)
- no rolling window for sensor trigger
- No way to override motion sensor temporarily
- No way to inhibit sensor in special cases

So here a tentative solution

The flow is using
- aquara motion sensors via zigbee2mqtt but it should be stratitforward to adapt (it shall be easy to modify for other sensors)
- homeassistant
- nodered homeassistant contrib, finite state machine plus others

How it works:
Light-Sensor Combination has two automation modes: movement sensor automation, manual switch automation
Movement Sensor Automation:
- A light can be turned on by movement sensor.
- After a parametric timeout light will turn off.
- If another movement is detected during timeout the timer is reset (rolling window).
- This mode can be turned off alltogether
- this mode can be temporarely overriden (i.e. turned off based on some conditions, for example: tv is on so do not turn on/off lights)
- Working time can be parametrized in 3 ways
    - Sun: activate when dark outside
    - Always : do I have to explain?
    - Time Range : configurable start stop time
- Light Brightness configurable for a , separetely configurable, timerange

Manual Switch Automation:
- if a user interacts with the light's switch either the physical one or the UI one motion sensor automation stops
- light is driven by switch for a configurable duration of time 
- at expiration of this time the light is turned off or left on (configurable) and functioning returns to movement sensor mode
- This mode can be turned off alltogether
- this mode can be temporarely overriden (i.e. turned off based on some conditions)

Please be kind: this is the first major nodered flow I do. BUGS / Inefficiency ahead. Help making it better

I enclose a
1) a very rough interface having all parameters on one stackin card.
In my mind the final version would be much more slick hiding most of the parameters: again any suggestions are welcome
2) yaml files defining the ui resources used

Finally: replace in the files "Cucina" (italian for kitchen :-) with your rooms light/sensor name

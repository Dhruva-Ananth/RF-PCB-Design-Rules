## PCB Layout Design

Layout is the most critical aspect of any RF PCB.

PCB Layout design process shall involve an iterative process of placement, routing and assignments of planes.

**Steps to Follow**
1. Make sure you define the stack-up initial with a prior PCB designer, take experience into account, layout needs a lot. Material of the dielectric, vs cost, vs size, vs time to manufacture are the major factors. Including the type of finish, via types possible.
![image](https://user-images.githubusercontent.com/60318299/210174441-9f7d94e9-23ee-4d78-8fc4-755c5f5388ce.png)
2. Symmetric Layout stack-ups are preferred.
3. Some thumb rules for RF traces are, we can realize the RF trace as either a simple microstrip open to air (or) embedded in the sandwich of substrates. For both calculate the impedance needed and be ready with the trace widths needed for each routing.
![image](https://user-images.githubusercontent.com/60318299/210174560-a9adafd1-6a6b-40eb-b878-ee6330994f76.png)
4. Make sure you have a good component placement, and route an uncalibrated trace to just orient the various ICs, follow the same component placement as the schematic.
5. For both the above mentioned RF trace methods, we need a companion continuous ground plane to support the RF signal to travel through the substrate.

![image](https://user-images.githubusercontent.com/60318299/210174588-6bf366ab-f0c1-4469-9678-bb4e782020d7.png)

6. High speed lines and differential also need impedance control.
7. All through the RF trace it should be smooth and no sudden width changes are suggested.

![image](https://user-images.githubusercontent.com/60318299/210174606-eb3ef663-cdc8-400b-a3ea-a9da3a7d4378.png)

8. If there are breaks in the Ground Plane we need to carefully add a AC coupled capacitor to provide a short path for the RF signal to travel through. This arrives due to the presence of multiple grounds and isolation in GND planes.
9. Via stitching is a must, around the RF trace, and drop a big number to support the trace with a waveguide structure to propagate without any interference.
10. Via stiches are also important to avoid the GND from having high transient potential changes.

![image](https://user-images.githubusercontent.com/60318299/210174621-ffc12b17-49c7-4578-92c3-acfcc16987d7.png)

11. Once you are sure the RF traces and high speed traces are fine. Go ahead and place all the ICs needed for the interfaces and connect them in proper order with digital, analog and RF isolations in place.
12. Now the last part is of Power, which needs a separate attention along with test point placement.
13. RF traces need to have smooth bends, and are an essential part of the design.

**PCB Power Layout Finger Rules**

1. Try to choose the components with nearby power ranges, generally preferred to have around 3p3 to 10v at max.
2. Duly follow the converter's layout guidelines and make sure the caps are chosen as mentioned in the datasheets. Space grade caps/ COTS can be analyzed for the same.
3. Try to plan out your placement of components in such a fashion that we can establish PCB planes wherever needed.
4. Major findings of faults include the isolation aspects, make sure to take care of them, all in the end we will have a zero-ohm res connecting all the isolated planes.
5. After the planes, make sure you just  drop in the vias needed, and least routing as possible.
6. While choosing the power planes, for low voltage lanes choose the layers as near to the placement layer as possible, as DC drops can be significant across the Vias.
7. Make sure you route most of the power in a single plane, if not make sure you dedicate certain power planes for this sole purpose, and try to isolate with a power ground for the return paths.

![image](https://user-images.githubusercontent.com/60318299/210174733-bb81925d-4d5e-4dc5-be7e-bdd973b68a32.png)

8. Width vs the current flowing is available on the internet for various materials, [follow it extravagantly](https://www.candorind.com/pcb-trace-width-vs-current-table/) (feel free to multiply the trace widths with some incremental factors).
9. More development can be done to understand how very sensitive reference voltage lanes can be a nice thin trace as it will not sink much power, but thick enough to sustain some level of flexibility.

**Why do we do isolation in PCB?**
Simply we don’t want the spikes/ripples to propagate from one ICs power system to another directly, so we give it a long path hoping the spike/ripple is boiled down to a level that is very minute. Very similar to pipelining or maybe gratings in petroleum tankers.
	
## Design Verification

1. Learn to use software tools such as ADS for simulating the power profiles, RF trace impedance profiles and draw results for the simulated PCB.
2. Verify if the external interface pins are correctly matched and the peripheral parts are chosen according to spec.
3. More robust designs will need a much stringent check on the placement of the Test Points.
4. RF Baluns with proper ground via mechanisms is suggested.

![image](https://user-images.githubusercontent.com/60318299/210174823-6ac01fd9-6d38-4190-a223-dcff8c3e5f2a.png)
(Image source is [Altium](https://resources.altium.com/p/what-balun-and-does-your-rf-pcb-need-one))

5. RF test points with a 1:100 power divider will work in the transmit side, try to incorporate those features.
6. Sensor test points are not suggested for sensitive ones, and will be helpful after the instrumentation amplification.
7. Actuator systems need special care as they sink a ton of current, try to isolate that PCB from the main control and RF PCB to ensure no EMI/EMC issues.
8. Try to probe the board with an EMI/EMC probe to understand the leakages.
9. Overall PCB should also have a via stitch to provide good shielding and contain the EMI/EMC.
10. Length matching, and impedance control of the traces has to be verified once again in the end, ground planes running beneath the PCB need to be continuous to provide a good path for the return signal.

**High Throughput Interfaces such as,**
LVDS, SERDES, CMOS, JESD can all be treated as a RF line itself, clock is to be protected and length matching is to be done at every level.

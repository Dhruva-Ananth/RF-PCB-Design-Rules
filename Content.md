# RF PCB Design Rules
Hello all,

Let's get a good understanding of how to better design a RF PCB with onboard power conversion.

This is mainly concentrated around the design of CubeSat systems.

The complete PCB design methodology is divided into 3 parts, 
	1. Overall Architecture Design
	2. PCB Schematic Design
	3. PCB Layout Design

Verification and Repeated Cross references to the Data Sheets provided is inevitable and important all through the design processes.

## Overall Architecture Design
Specifications for the system are supposed to be clear and concise, but yes systems engineers are always the middle man, and often are forced to change a ton of things if they deal with all the subsystems.
Here are certain rules and thumb memories, and somethings not to do in the architecture design

1. **Don’t** go deep in the specifications, keep it superficial and integrated. Make sure various systems correlate with each other that is the only thing to do, all of this without diving too deep into the specs.
2. **Don’t** try to be rigid with the interfaces, always a good option to use generic and futuristic designs. You should never, in the future, feel some extra feature should have been added.

Choose the components wisely according to their availability, costing and lead times.
Smaller Footprints, lesser extra components needed, low power consumption and regular packages such as QFN, DIP are suggested, take inputs of special requirements from their eval board.
Much information will be available on the eval kits and they will serve as a potential mark on how the IC shall behave when operated.

## PCB Schematic Design
**Do's:**
1. Try to maintain a very similar design to the ones prescribed in the datasheet, and most often they are the best ones.
2. Always refer the evaluation board schematics before you begin, you will get an overview of the surrounding requirements for the specific IC that you have chosen.
3. Ensure the interfaces are specifically marked.
4. Ensure the power pins are specifically marked.
5. Ensure the grounding pins are marked as per requirements.

**Dont's:**
Never try to complete one single IC all at once, place all the major IC's first and then follow exactly the opposite order mentioned.
1. Place Test points, wherever needed.
2. Place the Power Components and then verify the connections across the sheets.
3. Clocking lanes are the next step.
4. Mention if differential.
5. Connect the Interfaces next, order from High speed ones to the low speed ones.
6.Connect the RF connections first and assign the required impedance control scheme.

**Last Steps:**
Perfectly reflect upon the designs, and make necessary changes if needed in components and make sure you cross verify the schematics with the ones specified in the data sheets. 

## PCB Layout Design

Layout is the most critical aspect of any RF PCB.

PCB Layout design process shall involve an iterative process of placement, routing and assignments of planes.

**The Steps in opposite order again ;)**
1. Make sure you define the stack-up initial with a prior PCB designer, take experience into account, layout needs a lot. Material of the dielectric, vs cost, vs size, vs time to manufacture are the major factors. Including the type of finish, via types possible.
2. Symmetric Layout stack-ups are preferred.
3. Some thumb rules for RF traces are, we can realize the RF trace as either a simple microstrip open to air (or) embedded in the sandwich of substrates. For both calculate the impedance needed and be ready with the trace widths needed for each routing.
4. Make sure you have a good component placement, and route an uncalibrated trace to just orient the various ICs, follow the same component placement as the schematic.
5. For both the above mentioned RF trace methods, we need a companion continuous ground plane to support the RF signal to travel through the substrate.
6. High speed lines and differential also need impedance control.
7. All through the RF trace it should be smooth and no sudden width changes are suggested.
8. If there are breaks in the Ground Plane we need to carefully add a AC coupled capacitor to provide a short path for the RF signal to travel through. This arrives due to the presence of multiple grounds and isolation in GND planes.
9. Via stitching is a must, around the RF trace, and drop a big number to support the trace with a waveguide structure to propagate without any interference.
10. Via stiches are also important to avoid the GND from having high transient potential changes.
11. Just read them in line, as they are in proper order.
12. Once you are sure the RF traces and high speed traces are fine. Go ahead and place all the ICs needed for the interfaces and connect them in proper order with digital, analog and RF isolations in place.
13. Now the last part is of Power, which needs a separate attention along with test point placement.
14. RF traces need to have smooth bends, and are an essential part of the design.

**PCB Power Layout Finger Rules**

1. Try to choose the components with nearby power ranges, generally preferred to have around 3p3 to 10v at max.
2. Duly follow the converter's layout guidelines and make sure the caps are chosen as mentioned in the datasheets. Space grade caps/ COTS can be analyzed for the same.
3. Try to plan out your placement of components in such a fashion that we can establish PCB planes wherever needed.
4. Major findings of faults include the isolation aspects, make sure to take care of them, all in the end we will have a zero-ohm res connecting all the isolated planes.
5. After the planes, make sure you just  drop in the vias needed, and least routing as possible.
6. While choosing the power planes, for low voltage lanes choose the layers as near to the placement layer as possible, as DC drops can be significant across the Vias.
7. Make sure you route most of the power in a single plane, if not make sure you dedicate certain power planes for this sole purpose, and try to isolate with a power ground for the return paths.
8. Width vs the current flowing is available on the internet for various materials, follow it extravagantly (feel free to multiply the trace widths with some incremental factors).
9. More development can be done to understand how very sensitive reference voltage lanes can be a nice thin trace as it will not sink much power, but thick enough to sustain some level of flexibility.

**Why do we do isolation in PCB?**
Simply we don’t want the spikes/ripples to propagate from one ICs power system to another directly, so we give it a long path hoping the spike/ripple is boiled down to a level that is very minute. Very similar to pipelining or maybe gratings in petroleum tankers.
	
## Design Verification

1. Learn to use software tools such as ADS for simulating the power profiles, RF trace impedance profiles and draw results for the simulated PCB.
2. Verify if the external interface pins are correctly matched and the peripheral parts are chosen according to spec.
3. More robust designs will need a much stringent check on the placement of the Test Points.
4. RF Baluns with proper ground via mechanisms is suggested.
5. RF test points with a 1:100 power divider will work in the transmit side, try to incorporate those features.
6. Sensor test points are not suggested for sensitive ones, and will be helpful after the instrumentation amplification.
7. Actuator systems need special care as they sink a ton of current, try to isolate that PCB from the main control and RF PCB to ensure no EMI/EMC issues.
8. Try to probe the board with an EMI/EMC probe to understand the leakages.
9. Overall PCB should also have a via stitch to provide good shielding and contain the EMI/EMC.
10. Length matching, and impedance control of the traces has to be verified once again in the end, ground planes running beneath the PCB need to be continuous to provide a good path for the return signal.

**High Throughput Interfaces such as,**
LVDS, SERDES, CMOS, JESD can all be treated as a RF line itself, clock is to be protected and length matching is to be done at every level.
	

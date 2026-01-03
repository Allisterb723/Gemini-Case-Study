# Case Study: Industrial Automation — Distributed Klipper Architecture & High-Voltage Systems

**Author:** [Your Name]
**Tools Used:** Klipper Firmware, Mainsail OS, Python (Macros), Crowsnest
**Hardware:** Ender 3 Pro (Heavily Modified), **External Raspberry Pi (Klipper Host)**
**Status:** Optimization Phase Complete // High-Voltage Assembly Pending

---

### The Challenge
I aimed to push a standard consumer 3D printer beyond its factory limits to approach industrial speeds. The stock microcontroller lacked the processing power to handle complex kinematic calculations at high velocity, and the 24V power system limited torque at high RPMs.

### Phase 1: Distributed Computing Architecture (Completed)
I re-architected the printer's control logic by implementing a **Distributed System**:
* **The Brain (External Host):** Deployed an **External Raspberry Pi** running Klipper Service and Mainsail OS. This offloads G-code parsing and trajectory planning from the printer's limited MCU to a robust Linux environment.
* **The MCU (Motion Controller):** Flashed the printer's mainboard to act strictly as a low-level signal executor, allowing the External Pi to feed step commands at a much higher frequency than stock firmware could generate.
* **Resonance Compensation:** Utilized the Pi's processing power to run **Input Shaping** (ADXL345) algorithms, analyzing and nullifying vibration frequencies in real-time.
* **Algorithmic Feature Set:** Enabled advanced Klipper modules including **Pressure Advance** (for cornering accuracy), **KAMP** (Adaptive Meshing), and **Exclude Object** (batch failure management).

### Phase 2: Automated Workflow Scripting (Completed)
I replaced the standard static "Start/End" scripts with conditional logic macros using the Jinja2 templating language within the Klipper configuration.
* **Quality Assurance (The Wipe):** Wrote a custom nozzle-wiping routine that executes a precise physical movement sequence (`G1` arc) to purge oozing filament away from the print zone before engagement.
* **Safety & Parking:** Developed a `PRINT_END` macro that calculates a safe Z-hop relative to the max build height (preventing gantry crashes) and parks the toolhead over a specific waste receptacle.
* **Computer Vision Integration:** Configured the External Pi to host the `crowsnest` webcam server. I resolved a pathing conflict by manually re-mapping the video device (`/dev/video0`) in the Linux backend to ensure low-latency monitoring via the Mainsail interface.

### Phase 3: The "End Game" 48V Architecture (Design & Procurement)
To break the physical limits of the stepper motors (Back EMF), I utilized Gemini 1.5 Pro to architect a future "High-Voltage" control system. I have successfully procured the components for this industrial overhaul:
* **Power Infrastructure:** **Mean Well LRS-600-48 Power Supply** to drive the motion system, isolated from the logic voltage.
* **Logic & Control:** **BigTreeTech Manta M8P V2 Mainboard** paired with a **Raspberry Pi CM4** for integrated, high-speed processing.
* **Motion Drivers:** **TMC5160T Pro High-Voltage Stepper Drivers**, capable of handling the 48V spike for massive torque retention.
* **Mechanical Rigidity:** **MGN12H Linear Rails** on all axes to eliminate v-wheel play.

### Current Status & Next Steps
The machine is currently operating at peak efficiency using the **External Pi + Klipper** architecture.
* **Next Action:** Physical assembly and wiring of the 48V rail and Manta M8P V2 mainboard.

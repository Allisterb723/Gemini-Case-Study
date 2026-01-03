# Case Study: Simulation Environment Engineering — Runtime Window Injection & Resolution Override

**Author:** Allister Barnes
**Tools Used:** SRWE (Simple Runtime Window Editor), Content Manager, Gemini 1.5 Pro
**Subject:** Assetto Corsa (Triple Screen Rendering @ 10320x1440)

---

### The Challenge
I needed to deploy a triple-screen simulation environment at a custom resolution of **10320x1440**. However, I required a "non-destructive" deployment: I could not use Nvidia Surround (which merges screens into one virtual monitor) because it breaks standard desktop productivity workflows.

Running the simulation in standard "Windowed Mode" across three screens caused the game engine to reject negative coordinate positioning (e.g., `X-3440`), forcing the window to snap back to the primary display.

### Phase 1: The "Ghost" Monitor Problem
I utilized the LLM to diagnose the conflict between Windows Display Scaling (125%) and the simulation's legacy rendering engine.
* **The Diagnosis:** The game checks for valid monitor coordinates only during the *initial boot sequence*. If the window is commanded to spawn on a "negative" coordinate (the left monitor), the engine flags it as "Out of Bounds" and resets it.
* **The Solution:** We needed to bypass the boot-check sequence entirely.

### Phase 2: Runtime Memory Injection (SRWE)
We implemented a **Runtime Injection Workflow** using SRWE.
* **The Bypass:** Instead of editing the configuration files (`video.ini`), which are read at startup, we launched the application in a safe "Center Screen" state.
* **The Injection:** Once the process (`acs.exe`) was running and the memory was allocated, we injected new window parameters directly into the OS window manager:
    * **Global Position:** Forced `X: -3440`, `Y: 0` (spanning the left monitor).
    * **Global Size:** Forced `Width: 10320`, `Height: 1440`.
* **Border Removal:** Stripped the standard Windows chrome (Title Bar/Borders) to emulate a "Fullscreen" environment without the OS-level "Exclusive Mode" handshake.

### Phase 3: Geometric Correction
With the resolution forced, the render perspective was initially distorted ("stretched").
* **The Fix:** We configured the internal **Triple Screen Projection Module**.
* **The Calculation:** We calculated the precise physical bezel width (in mm) and the angle of incidence between the side monitors. Inputting these values generated a corrected 3D perspective, rendering three distinct viewports (Left/Center/Right) rather than one stretched image.

### Outcome
I successfully achieved a **seamless 10320x1440 simulation environment** that functions visually as "Fullscreen" but technically runs as a "Bordered Window." This allows for instant switching between the Simulation and Productivity workflows without toggling Nvidia Surround or rebooting the GPU drivers.

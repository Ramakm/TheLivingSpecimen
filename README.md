# The Living Specimen

An interactive anatomy atlas where the 3D specimen is never static. Internal parts rotate, fluids flow, particles react and layers pulse. Pause at any moment to inspect the details.

Best for anatomy, biological systems and dynamic simulations.

![Human heart, dark theme](screenshots/heart-dark.png)

## Specimens

| ID | Specimen | What moves |
|---|---|---|
| LS-001 | **Human Heart** | Atria and ventricles contract at 72 bpm (real time). Blue and red blood flows through the chambers and great vessels. An electrical impulse travels from the SA node, pauses at the AV node and runs down to the apex. |
| LS-014 | **Animal Cell** | Live cutaway that follows the camera. The membrane ripples, mitochondria drift and flare, the cytoplasm streams, and vesicles bud from the Golgi, ride microtubules and fuse with the membrane. |
| LS-027 | **Motor Neuron** | Dendritic signals sum at the soma. An action potential jumps node to node along the myelin (saltatory conduction) and releases neurotransmitter at the terminals. |

## Inspecting

- **Pause / play:** button or <kbd>Space</kbd>. Pausing shows numbered labels on the model.
- **Scrub the cycle:** drag the phase timeline under the model. <kbd>←</kbd> <kbd>→</kbd> step 1% when paused.
- **Speed:** 0.1×, ¼×, ½×, 1×.
- **Layer toggle:** glass heart wall, cell cutaway or myelin sheath.
- **Click any structure** to open it in the close-up card. Hover shows its name.
- **Live readout:** an ECG, ATP turnover or membrane-potential trace plus live values. They are computed from simulation time, so they freeze on pause and follow the scrubber.
- A scale bar updates as you zoom. Light and dark themes are included.

## Run it

It is a single static file with no build step.

```bash
# any static server works
python3 -m http.server 8000
# then open http://localhost:8000
```

Opening `index.html` directly also works in most browsers. Three.js (r160) is loaded from jsDelivr through an import map, and the fonts come from Google Fonts, so the page needs an internet connection.

To host it, enable GitHub Pages on the `main` branch (root folder).

## How it's built

- **Three.js r160** with `OrbitControls`, `RoomEnvironment` lighting and `MeshPhysicalMaterial` (clearcoat + sheen) for wet tissue.
- **Procedural geometry only, with no model files.** Organs are noise-displaced spheres. Vessels, dendrites and the ER are tapered tubes. Coronary arteries are placed by raycasting onto the ventricle surface.
- **Deterministic animation.** Every motion is a function of simulation time `t` and cycle phase `f`, which is what makes pause and scrub exact. Blood flow uses a precomputed integral of the cardiac envelope so particles land in the same place whichever way you scrub.
- **Custom point shader** for blood, cytoplasm and neurotransmitter particles, with world-space clipping for the cell cutaway.
- The theme palette is drawn from H&E histology stain: hematoxylin violet, eosin pink and an amber "voltage" accent.

## Screenshots

| Animal cell | Light theme | Mobile |
|---|---|---|
| ![Cell](screenshots/cell-dark.png) | ![Light](screenshots/heart-light.png) | ![Mobile](screenshots/mobile.png) |

---

Built by [techwith.ram](https://techwithram.com).

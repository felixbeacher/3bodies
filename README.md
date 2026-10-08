# Threebody — Orbital Lab

An interactive, three-dimensional simulation of three celestial bodies moving under their mutual gravitational attraction. Explore chaotic orbits, follow their trails, and see how small changes to the starting conditions can produce very different journeys.

© 2026 Felix Beacher

## Getting started

Download `index.html` and open it in a modern web browser. Everything needed to run the simulation is contained in that one file.

No installation, build process, external libraries or internet connection is required. The simulation runs locally in your browser.

## Features

- Three-dimensional gravitational motion with perspective rendering.
- Colour-coded bodies, fading motion trails and gravitational force arrows.
- Smooth camera rotation, panning, zooming and automatic orbiting.
- Editable starting positions and velocity vectors for all three bodies.
- Sliders for gravity, individual masses, initial velocity multipliers and playback speed.
- Pause and resume, with camera controls available while paused.
- Three starting arrangements: a perturbed figure-eight, a figure-eight reference and a binary system with an approaching third body.
- Live energy, momentum and angular-momentum diagnostics.

## Camera controls

| Action | Control |
| --- | --- |
| Rotate the view | Drag with the mouse |
| Zoom | Scroll the mouse wheel |
| Pan | Shift-drag or right-drag |
| Bring all bodies into view | Double-click the scene or select **Frame bodies** |
| Restore an angled view | **Home view** |
| Look directly onto the XY plane | **XY view** |
| Rotate the camera automatically | **Auto orbit** |
| Touch rotation | Drag with one finger |
| Touch zoom and pan | Pinch or move two fingers |

With the scene focused, use the arrow keys to rotate, **+ / −** to zoom, **Space** to pause or resume, **F** to frame the bodies and **H** to restore the home view.

## Changing the experiment

1. Choose a starting arrangement, or expand each body's panel to enter your own values.
2. Set its **X, Y and Z** starting position and initial velocity components.
3. Adjust the mass, velocity multiplier and gravitational constant as desired.
4. Select **Apply & restart** to begin the new experiment.

Changes to the initial conditions are staged until you apply them. Applying resets simulation time, trails and the conservation baseline. **Restart** repeats the last applied experiment.

Playback speed and the trail, force-vector and grid switches take effect immediately.

All quantities use arbitrary, internally consistent units. Masses are relative to one mass unit. Position components accept values from −20 to 20; velocity components accept −10 to 10 before the velocity multiplier is applied.

## Reading the scene

**Trails** record the previous 12 units of simulated time and fade as they age.

**Bright arrows** show the direction of each body's net gravitational force. Arrow lengths use a logarithmic scale to keep large forces readable. Faint connecting lines identify the interacting pairs.

**Body sizes** are illustrative. The objects are simulated as softened point masses, not as solid spheres that collide when they touch on screen.

If a body moves outside the view, choose **Frame bodies**, or zoom out.

## Physics and numerical accuracy

The simulation uses softened Newtonian gravity in three dimensions. A softening length of **0.06** smooths the force during close encounters, avoiding the singularity of ideal point masses at zero separation. This also changes the physics of very close encounters; the program is an educational exploration rather than a precision astronomical prediction tool.

Motion is integrated with the **kick–drift–kick form of velocity Verlet**, using a fixed timestep of **1/8192** simulation unit. The force and energy calculations use the same softened gravitational model.

The physics timestep is independent of rendering speed. Work per frame is capped, so a heavily loaded browser slows the progression of simulated time rather than increasing the timestep. Trail history and display resolution are also bounded to help performance.

The numerical-health panel reports:

- **Total energy:** kinetic energy plus softened gravitational potential energy.
- **Energy drift:** the absolute change in energy divided by initial kinetic energy plus the magnitude of initial potential energy. This avoids dividing by nearly zero total energy.
- **Angular momentum drift:** the change relative to an initial characteristic scale.
- **Momentum drift:** the absolute magnitude of the change in total linear momentum.

An energy-drift warning appears above **0.1%**. The simulation pauses above **1%**, or if its energy calculation becomes non-finite. Try gentler initial conditions if a warning appears.

Chaotic trajectories amplify tiny differences in initial conditions and numerical calculations. Good energy conservation does not guarantee an exact long-term trajectory.

The figure-eight reference uses the classical Newtonian starting arrangement, but softening slightly perturbs its exact periodicity. The default arrangement changes the masses and introduces out-of-plane motion.

## How it is built

The single HTML file contains the layout, styles, physics and rendering code. The simulation maintains full 3D positions and velocities, then draws a perspective view using the browser's native Canvas 2D API. No external graphics engine, WebGL library or downloaded assets are required.

## Publish on GitHub Pages

You can host the project without editing any code:

1. Create a public GitHub repository, for example `three-body`.
2. Choose **Add file → Upload files** and upload `index.html` to the repository's top level. Commit the upload.
3. Open the repository's **Settings → Pages**.
4. Under **Build and deployment**, select **Deploy from a branch**.
5. Choose the **main** branch and **/ (root)** folder, then save.
6. When deployment finishes, open the website address shown by GitHub Pages.

The address for a project repository typically follows this pattern:

`https://YOUR-USERNAME.github.io/three-body/`

Only `index.html` is required to run the site. You can also upload this README to describe the project on GitHub. Updating the HTML file on the publishing branch updates the website after deployment.

See the [official GitHub Pages instructions](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site) for details.

## Copyright

© 2026 Felix Beacher.

No open-source licence is included with this project.

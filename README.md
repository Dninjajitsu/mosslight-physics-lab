# Mosslight: A Little Physics Lab

A no-build, no-dependency browser prototype for a cozy 2D science practical game. It starts with one experiment: timing a pendulum.

## Run it

1. Download and unzip the folder.
2. Open `index.html` in a modern desktop browser (Chrome, Edge, Firefox, or Safari).
3. Adjust the controls, then choose **Release & measure 10 periods**.

No account, API key, package installation, or internet connection is required after the file is downloaded.

## Controls

- **Left / Right arrow** or **A / D**: move the lab assistant.
- **E**: inspect / talk.
- **Space**: release the pendulum and run a trial.
- Use the sliders to change string length, release angle, bob mass, breeze, and lab disturbance.

## What the model does

- Uses the pendulum equation of motion with gravity, a small damping term, a changing lateral breeze, and a simplified vibration disturbance.
- Compares the measured period to the ideal small-angle estimate `T ≈ 2π√(L/g)` with `g = 9.81 m/s²`.
- Adds stopwatch reaction-time uncertainty to measured data. Noise is represented as a combined simplified model of bench vibration and observer distraction. Ordinary sound alone does not normally change a pendulum's period significantly.
- Keeps a short in-session experiment log. The log resets when the page is refreshed.

## What this is—and isn't

This is a playable visual prototype and a conversation starter for a larger educational game. It is not calibrated scientific equipment; the disturbance model is intentionally simplified for learning. The art is original and drawn procedurally in Canvas; it uses a cozy hand-drawn animation mood rather than copying a particular studio's characters or assets.

## Recommended next milestones

1. Add a proper pause, reset-to-defaults, keyboard focus, and mobile controls.
2. Add a projectile-motion practical using measured launch angle, initial speed, gravity, and wind resistance.
3. Add data export (CSV), graphing, units checks, and teacher mode.
4. Separate the physics simulation from presentation code and add automated tests against known cases.
5. Replace procedural scenery with commissioned/original illustrated backgrounds and sprite sheets, keeping art files editable.
6. Add save files and lesson progression only after the experiment loop is stable.

## Codex task prompt

> Inspect this small no-build HTML5 Canvas game before editing it. Keep the game browser-based and 2D. First list current features and bugs, then make one focused change at a time. Preserve the educational physics: the ideal simple-pendulum period is approximately `2π√(L/g)` for small angles, mass should not affect the ideal period, and sound should not be claimed to directly alter gravity. Keep rendering, physics, controls, and experiment-log code clearly separated. Test the page in a browser after every meaningful change and report exactly what you tested. Do not add accounts, servers, multiplayer, paid APIs, or a framework unless I approve it.

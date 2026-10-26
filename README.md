# Mosslight: A Little Physics Lab

A no-build, no-dependency browser simulator for a cozy 2D science practical game. It simulates a physics practical in a quiet greenhouse laboratory: timing a pendulum and investigating how real-world conditions affect experimental outcomes.

## Run It

1. Download or clone this repository.
2. Open `index.html` (or `mosslight ver 1.html`) directly in any modern desktop browser (Chrome, Edge, Firefox, Safari).
3. No build tools, package managers, accounts, servers, or external internet connections are required.

To run via a local static web server (optional):
```bash
# Using Node.js
npx serve .
# or
node -e "const http=require('http'),fs=require('fs'),path=require('path');http.createServer((req,res)=>{const p=path.join(__dirname,req.url==='/'?'index.html':req.url);fs.readFile(p,(err,d)=>{if(err){res.writeHead(404);res.end('Not found');}else{res.writeHead(200);res.end(d);}});}).listen(8080,()=>console.log('Server running on http://localhost:8080'));"
```

## Controls

- **Left / Right Arrow** or **A / D**: Walk the student assistant around the greenhouse.
- **E**: Inspect apparatus or talk with the assistant.
- **Space**: Release the pendulum and begin timing 10 complete periods.
- **Number Fields & Sliders**: Type exact values or drag sliders to modify experiment parameters.
- **🎨 Customize Character**: Open the character studio wardrobe to customize appearance, clothes, and science props.
- **▶ Audio Player**: Toggle relaxing procedural lo-fi chords and ambient greenhouse sounds.

## What the Model Does

- **Pendulum Equation of Motion**:
  $$\frac{d^2\theta}{dt^2} = -\frac{g}{L}\sin\theta - \gamma \frac{d\theta}{dt} + \frac{a_{\text{wind}} + a_{\text{vibration}}}{L}\cos\theta$$
- **Theoretical Small-Angle Period**:
  $$T \approx 2\pi\sqrt{\frac{L}{g}}$$
- **Finite-Amplitude Second-Order Correction**:
  $$T \approx T_0 \left(1 + \frac{1}{16}\theta_0^2\right)$$
  (Highlights the small-angle assumption when $\theta_0 > 15^\circ$).
- **Fixed 10-Period Timing Protocol**:
  Times 10 complete periods from release peak $t_0$ to $t_{10}$, adding realistic human stopwatch reaction uncertainty ($\pm 0.04\text{s}$ to $0.24\text{s}$ scaled by disturbance), then computes $T_{\text{measured}} = (t_{10} - t_0 + \text{reactionError}) / 10$.
- **Mass Independence in Ideal Gravity**:
  Bob mass cancels out in the gravitational restoring term ($\alpha = -(g/L)\sin\theta$). In the presence of air drag and cross-breeze, heavier bobs display greater aerodynamic inertia ($a = F_{\text{drag}} / m$).
- **Planetary Gravity Presets**:
  Quick-switch between Earth ($9.81\text{ m/s}^2$), Moon ($1.62\text{ m/s}^2$), Mars ($3.72\text{ m/s}^2$), and Jupiter ($24.79\text{ m/s}^2$).

## Key Features

1. **Dual Numerical Controls**:
   - Every physical parameter has a linked editable number input and slider with bidirectional synchronization.
   - User typing is never interrupted mid-input; values are validated and clamped on `Enter` or `blur`.
   - Clear physical units: metres (`m`), degrees (`°`), grams/kilograms (`g`/`kg`), gravitational acceleration (`m/s²`), damping rate (`s⁻¹`), and wind/disturbance (`%`).
   - Dedicated "↺ Reset Experiment" and "↺ Reset to Defaults" controls.
2. **Modular Chibi Character & Wardrobe Studio**:
   - Expressive 2D storybook chibi aesthetic with stepped, handmade animation.
   - Layered modular rendering: skin tones, hairstyles, hair colours, eye colours & expressions, sweaters, bottoms, lab coats/aprons, footwear, spectacles, goggles, and handheld tools.
   - Dynamic animation states: `idle` (breathing, blinking), `walking` (stepped 4-frame cycle), `observing` (leaning forward, taking notes), `celebrating` (raising arms with sparkle emotes when error $< 3\%$), and `reacting` (head tilt with sweat drop when error/disturbance is high).
   - Saved locally via browser `localStorage` (`mosslight_chibi_character_v1`).
3. **Procedural Lo-Fi Music & Ambience**:
   - Synthesized using the native Web Audio API — zero external files or copyright issues.
   - Warm Rhodes-style electric piano chords ($F^{\text{maj7}} \to E^{\text{m7}} \to D^{\text{m9}} \to C^{\text{maj7}}$ at 68 BPM), kalimba arpeggio plucks, and mellow sub bass.
   - Dynamic environmental audio: greenhouse wind/breeze (scales with the wind setting), organic birdsong chirps, gentle rain, and physical interaction sound effects.
   - Full browser autoplay compliance with tab-visibility auto-pause.
4. **Field Notebook & Data Export**:
   - Compares theoretical small-angle period against measured period and percentage error.
   - Generates contextual scientific takeaways based on parameter choices.
   - Complete trial history log with "📥 Export CSV" and "🗑️ Clear Log" options.

## Automated Testing

Run the test suites with Node.js:

```bash
# Run unit tests (physics formulas, parameter bounds, validation, character sanitization)
node tests/unit_tests.js

# Run Chrome DevTools Protocol integration test (headless browser DOM, audio, simulation, screenshot)
node tests/browser_test.js
```

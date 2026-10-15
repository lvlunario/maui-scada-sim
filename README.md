# Island Grid Simulator

**An educational browser-based simulator for exploring island power systems, renewable generation, battery storage, and simplified dispatch.**

This personal project connects my electric-utility engineering background with an interactive way to explore how supply and demand change throughout the day. It brings simulated grid indicators, generation assets, and operator controls into a single dashboard.

**Status:** early prototype. The application is implemented in [`index.html`](index.html); this repository is more than a project outline.

> This is an independent educational model, not a Maui Electric / Hawaiian Electric system. Place names, equipment labels, capacities, and operating assumptions in the prototype are illustrative and are not a verified representation of the actual Maui grid. No utility telemetry or equipment connections are used.

## Run the simulator

There is no build step, package installation, account, or API key required.

1. Select **Code → Download ZIP** on this repository.
2. Extract the ZIP.
3. Open `index.html` in a modern browser.
4. Keep an internet connection available for the externally hosted styles and charts.
5. Select **START** to begin. The simulator initially opens paused with zero readings.

For a local HTTP server, use:

```bash
git clone https://github.com/lvlunario/maui-scada-sim.git
cd maui-scada-sim
python -m http.server 8000
```

Then open **http://localhost:8000**. On Windows, `py -m http.server 8000` is an alternative.

GitHub's file viewer displays source code; clicking `index.html` on GitHub does not launch the application.

## What you can explore

| Area | Implemented behavior |
| --- | --- |
| **Grid overview** | Simulated demand, generation, supply balance, and an illustrative frequency indicator. |
| **Renewable generation** | Solar and wind output driven by simplified weather and generation curves. |
| **Battery storage** | State of charge, charging during selected surplus hours, and discharge during selected evening conditions. |
| **Firm generation / AGC** | Simplified automatic dispatch, unit selection, manual start/stop, and return to automatic control. |
| **Charts** | Demand versus net demand, generation mix, and selected-unit output history. |
| **Reports** | Energy totals, load extrema, unit running hours, and illustrative maintenance counters. |
| **Weather mode** | Internal synthetic weather by default; an optional Open-Meteo cloud-cover forecast mode. |

**AGC** means automatic generation control. **EMS** means energy management system. In this project, both refer to simplified teaching logic rather than a utility-grade implementation.

## Suggested walkthrough

1. **Start in Simulation mode.** Observe demand, renewable output, and the firm generators responding.
2. **Adjust the speed slider.** Let several simulated hours pass to see the daily demand and solar patterns. Charts collect samples every ten simulated minutes.
3. **Compare total and net demand.** Net demand is demand minus solar and wind generation.
4. **Watch battery behavior.** Look for charging during midday surplus and discharging during high evening net demand. Storage does not necessarily operate every day.
5. **Open AGC: Firm Generation.** Select a unit, try **Force Stop**, and observe how automatic units respond. Select **Return to Auto** to release the override.
6. **Open Reports & Analytics.** Review running hours and the maintenance counters. **Log Maintenance** resets the selected unit's running-hours counter.
7. **Pause or reset.** Reset clears the in-memory simulation. Reloading the page also starts a new session.

## Model and architecture

The current application is contained in one HTML file:

```text
index.html
├── Dashboard markup and styling
├── Asset configuration and hourly demand profile
├── Simulation state and one-minute time steps
├── Synthetic weather and renewable-output calculations
├── Battery scheduling and simplified firm dispatch
├── Chart.js visualization
└── Browser controls and optional weather request
```

- **Interface:** HTML, JavaScript, CSS, and Tailwind CSS loaded from a CDN.
- **Charts:** Chart.js loaded from a CDN.
- **Weather:** synthetic conditions; optional external Open-Meteo forecast request.
- **Storage:** browser memory only; no database, account system, or saved sessions.
- **Units:** power in MW; energy and battery state of charge in MWh.

The optional forecast only supplies cloud-cover inputs. Demand and generation remain simulated; wind remains synthetic. The interface's “Real-Time Forecast” label does not mean live grid data.

## Engineering limitations and known issues

This prototype is useful for exploring relationships and interface ideas, but its outputs are not validated for engineering decisions.

- No AC power flow, network topology, voltage/reactive-power model, protection coordination, or transient-stability solution.
- The displayed frequency is a simple function of supply imbalance, not a physical frequency-response model.
- Dispatch uses fixed priority and simplified ramping. Configured startup times and minimum output constraints are not fully enforced.
- Battery charging is not included correctly in the displayed supply-balance accounting; this needs correction before interpreting that KPI quantitatively.
- The **START** timer and speed-slider timer use inconsistent scaling. The speed label should not yet be treated as an accurate time multiplier.
- Daily statistics do not reset at midnight yet.
- Weather varies between runs, and forecast handling does not yet align timestamps across simulation dates.
- Manual-start behavior, status labels, and selected-unit details need further validation.
- External CDN or forecast failures can affect startup, appearance, or chart rendering. The application is not fully offline-ready.

## Next development priorities

- [ ] Correct power-balance accounting, timer scaling, and daily-statistic rollover.
- [ ] Add deterministic scenarios and automated checks for energy balance and battery limits.
- [ ] Validate unit start/stop behavior and define startup/ramp constraints explicitly.
- [ ] Improve forecast error handling and timestamp alignment.
- [ ] Separate the simulation model from the interface.
- [ ] Add scenario export, documented validation results, and a hosted demo.

These are planned improvements, not completed capabilities.

## Project context

Created as an independent portfolio and learning project by **Leonardo Lunario**, drawing on experience in utility engineering, systems integration, and test. Personal development may include AI assistance; the repository is separate from employer work and proprietary systems.

[Engineering portfolio](https://leonardolunario.vercel.app/) · [GitHub profile](https://github.com/lvlunario) · [LinkedIn](https://www.linkedin.com/in/leonardolunario)

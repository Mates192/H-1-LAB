# Tail Rotor Thrust Simulator — Product and Technical Specification

## 1. Document Status

- **Product:** Tail Rotor Thrust Simulator
- **Version:** 4.0 MSA-altitude and temperature OGE specification
- **Application type:** Single-page educational visualization and simulation
- **Distribution format:** One self-contained, executable HTML file
- **Language of the user interface:** English

## 2. Product Summary

The application is an educational, top-down visualization of a 9,000–13,000 kg helicopter in out-of-ground-effect hover. It demonstrates how main-rotor torque, shared engine power, helicopter weight, MSA altitude, air temperature, tail-rotor blade pitch, and wind interact to produce rotor thrust and helicopter yaw.

The user sets:

- tail-rotor blade pitch at \(r/R=0.7\), subject to the SPUU-52 altitude-dependent maximum;
- combined engine power as a percentage of the altitude-limited 4,000 metric-horsepower rating;
- helicopter weight from 9.0 to 13.0 metric tonnes;
- `Angular Momentum`, implemented as the adjustable yaw moment of inertia for equipment and load distribution;
- MSA altitude above mean sea level from 0 to 6,000 m;
- outside air temperature from −50°C to +50°C;
- wind speed;
- wind direction.

The application then continuously calculates and displays:

- helicopter yaw direction and yaw rate;
- actual tail-rotor thrust under the current wind and yaw-rate conditions;
- representative tail-rotor blade angle of attack and its range over one rotor revolution;
- main-rotor lift after the density and available-power corrections;
- current air density and maximum engine power at the selected MSA altitude and temperature;
- tail-rotor thrust required for zero yaw;
- wind direction and magnitude;
- the resulting yawing moments.

The helicopter must rotate visibly around its vertical axis when the moments are not balanced.

Version 4 uses a main rotor that turns **clockwise when viewed from above**. Its reaction torque therefore acts **counterclockwise on the fuselage**.

## 3. Purpose

The primary purpose is to help a learner understand that:

1. a rotating main rotor produces an opposing torque on the fuselage;
2. the tail rotor produces a lateral force at a distance from the center of gravity and therefore creates an opposing yawing moment;
3. wind can create an aerodynamic yawing moment on the fuselage;
4. pitch input changes geometric tail-rotor blade pitch, while wind changes relative airflow and therefore changes blade angle of attack and thrust even when pitch is held steady;
5. helicopter yaw rate gives the tail rotor a local translational velocity around the center of gravity, which also changes relative airflow, blade angle of attack, and thrust;
6. an imbalance of yawing moments causes angular acceleration and rotation;
7. the tail-rotor thrust actually produced is not necessarily the same as the thrust required to maintain a constant heading.

The application is a qualitative and educational model. It is not intended for aircraft design, flight planning, pilot certification, accident analysis, or prediction of a specific helicopter's behavior.

## 4. Scope

### 4.1 Included in Version 4

- A symbolic, generic single-main-rotor helicopter.
- Top-down view in hover.
- Clockwise main-rotor rotation when viewed from above.
- Counterclockwise main-rotor reaction torque on the fuselage.
- User-controlled tail-rotor geometric pitch from −6° to the current SPUU-52 limit at \(r/R=0.7\).
- Simplified blade-element calculation of tail-rotor angle of attack and thrust.
- Relative airflow at the tail rotor caused by both wind and helicopter yaw rate.
- A configurable critical tail-rotor blade angle of attack.
- A simplified post-stall thrust collapse used as an educational LTE approximation.
- A live chart of tail-rotor thrust against blade angle of attack, including the critical angle and current operating point.
- User-controlled combined engine-power percentage.
- User-controlled helicopter weight from 9.0 to 13.0 metric tonnes.
- User-controlled yaw moment of inertia, labeled `Angular Momentum`, with weight-dependent realistic limits.
- User-controlled MSA altitude from 0 to 6,000 m.
- User-controlled outside air temperature from −50°C to +50°C.
- Automatic MSA/ISA standard-temperature selection when altitude changes.
- Air-density calculation from standard pressure at MSA altitude and the selected temperature.
- TV3-117VM-inspired flat-rated combined power to 3,600 m, followed by a density-ratio power lapse.
- Altitude-and-temperature density correction of main-rotor lift, tail-rotor blade-element forces, induced velocity, and wind force.
- User-controlled wind speed and direction.
- Wind-induced fuselage yawing moment.
- Simplified wind effect on tail-rotor thrust.
- Continuous yaw dynamics.
- Graphical and numerical display of yaw rate.
- Graphical and numerical display of actual tail-rotor thrust.
- Numerical display of tail-rotor thrust required for zero yaw.
- Graphical wind vector.
- Pause, resume, and reset controls.
- A short explanation of the active forces and model limitations.

### 4.2 Explicitly Excluded from Version 4

- Full aircraft-specific LTE modeling, including main-rotor vortex interference, tail-rotor vortex-ring-state dynamics, and detailed weathercock-stability regions.
- Vortex ring state or settling with power.
- Translational lift.
- Main-rotor flapping, coning, or gyroscopic effects.
- Ground effect.
- Vertical, longitudinal, or lateral helicopter movement.
- Roll and pitch dynamics.
- Mechanical drivetrain losses, engine/drivetrain transients, governor dynamics, fuel, and rotor-speed droop. Version 4 keeps both rotor speeds fixed and reports when the selected power cannot sustain that fixed-RPM operating point.
- High-fidelity three-dimensional blade aerodynamics, dynamic stall, blade flapping, and computational-fluid-dynamics modeling.
- Terrain, obstacles, gust turbulence, and wind shear.
- A model of any real helicopter type.

## 5. Terminology

- **Combined engine-power input:** User-selected percentage of the altitude-limited shared 4,000 metric-horsepower rating.
- **MSA altitude:** Height above mean sea level; the model derives standard atmospheric pressure from this value.
- **Outside air temperature:** Independently adjustable air temperature. Changing MSA altitude resets it to the corresponding standard-atmosphere temperature, while changing temperature does not alter altitude.
- **Maximum engine power at altitude:** The flat-rated or lapsed combined TV3-117VM-inspired power before the user-selected power percentage is applied.
- **Main-rotor torque:** Reaction torque applied to the fuselage by the clockwise main rotor.
- **Geometric blade pitch:** The directly commanded blade angle at \(r/R=0.7\).
- **SPUU-52 pitch limit:** The maximum commanded tail-rotor pitch calculated from standard pressure at the selected MSA altitude and the selected air temperature.
- **Blade angle of attack:** The angle between a blade element's chord line and its local relative airflow. It may change even while geometric blade pitch is held steady.
- **Actual tail-rotor thrust:** Thrust produced at the commanded pitch after calculating local relative airflow and blade-element forces.
- **Required tail-rotor thrust:** The tail-rotor thrust that would be needed at the current instant to produce zero net aerodynamic and rotor yawing moment.
- **Yaw rate:** Helicopter angular velocity around its vertical axis.
- **Wind direction:** The compass direction **from which** the wind originates.
- **Heading:** Direction in which the helicopter nose points.

## 6. Coordinate and Sign Conventions

The application must use the following conventions consistently in calculation, labels, and graphics:

- The initial helicopter heading is north/up.
- Compass direction is measured clockwise:
  - 0° = north;
  - 90° = east;
  - 180° = south;
  - 270° = west.
- Wind direction follows the meteorological “from” convention. A wind direction of 90° means wind from the east and air movement toward the west.
- Positive yaw is counterclockwise when viewed from above.
- Negative yaw is clockwise when viewed from above.
- The helicopter body axes are \(x\) forward, \(y\) left, and \(z\) up.
- The tail-rotor hub is located aft of the center of gravity at \(\vec{r}_{tr} = [-L_{tr}, 0, 0]\).
- The numerical yaw-rate display must always include a plain-language direction:
  - `12.4 °/s CCW`;
  - `8.1 °/s CW`;
  - `0.0 °/s Stable`.
- The main rotor rotates clockwise when viewed from above.
- The clockwise main rotor applies a positive, counterclockwise reaction torque to the fuselage.
- At the initial north-facing heading, the tail rotor's compensating force vector points to the helicopter's left and produces a clockwise yawing moment.

## 7. User Experience

### 7.1 Page Layout

The single page should contain four functional regions:

1. **Header**
   - Application name.
   - One-sentence educational description.
   - Pause/resume and reset controls aligned to the upper-right corner.

2. **Input panel**
   - Combined engine-power control.
   - Wind-speed control.
   - Wind-direction control.

3. **Simulation canvas**
   - Top-down helicopter.
   - Rotating main rotor.
   - Helicopter heading/yaw motion.
   - Actual and required tail-rotor thrust vectors anchored at the tail-rotor location.
   - Wind vector.
   - Optional moment arcs around the center of gravity.
   - No tail-rotor propeller or blade graphic; in the top-down view, the tail-rotor location is represented only by its thrust vectors.

4. **Output and explanation panel**
   - Yaw rate and current heading grouped in the hero readout.
   - Actual tail-rotor thrust.
   - Mean tail-rotor blade angle of attack.
   - Minimum-to-maximum blade angle-of-attack range.
   - Relative axial airflow at the tail rotor.
   - Simplified LTE state and percentage of blade elements beyond the critical angle.
   - Required tail-rotor thrust.
   - Main-rotor reaction torque.
   - Wind yawing moment.
   - Net yawing moment.
   - Short dynamic explanation of why the helicopter is rotating or stable.

5. **Live LTE chart**
   - Horizontal axis: peak local tail-rotor blade angle of attack in degrees.
   - Vertical axis: calculated tail-rotor thrust on a constant 0–35,000 N scale.
   - Critical-angle marker.
   - Post-stall/LTE region.
   - Fixed reference thrust curve generated from the trimmed no-wind condition.
   - Continuously updated current operating point.

On wide screens, the input panel, simulation canvas, and output panel should be visible simultaneously. On narrow screens, they may stack vertically with the simulation canvas first or second, but all controls must remain usable without horizontal page scrolling.

### 7.2 Input Controls

The controls panel is divided into three sections:

- `Flight Controls`: `Yaw Pedals` and `Power`.
- `Environment`: `Wind speed`, `Wind direction`, `MSA altitude`, and `Temperature`.
- `Helicopter Configuration`: `Weight` and `Angular Momentum`.

#### Tail-Rotor Pitch

- This must be the first control in the `Flight Controls` section.
- Control type: range slider plus synchronized numeric field.
- Label: `Yaw Pedals`.
- Unit: degrees.
- Default: the numerically solved no-wind trim value (approximately 11.2°).
- Minimum: `−6°`.
- Neutral: `0°`.
- Maximum: the current SPUU-52 limit, approximately `20.6°` at 0 m and `23.2°` from approximately 3,000 m upward.
- Step: `0.1°`.
- Invalid typed values must be clamped to the valid range.
- The scale must show `−6°` and the current SPUU-52 maximum.
- Changing MSA altitude or temperature must update both pitch-control maxima immediately and clamp the current command if it exceeds the new limit.
- When focus is not inside an editable control, `ArrowLeft` and `ArrowRight` must change pitch by 0.1°.
- Holding Shift with either arrow key must use a 1° step.
- Global pedal shortcuts must not override native arrow-key behavior while the user is editing a numeric field, select, textarea, or focused range slider.
- No auxiliary trim-status or keyboard-shortcut caption is shown below the pedal control.

The default pitch must balance the main-rotor reaction moment at 100% combined engine power in no wind at zero yaw rate.

#### Combined Engine Power

- Control type: range slider plus synchronized numeric field.
- Label: `Power`.
- Unit: `% of the maximum engine power available at the selected atmospheric conditions`.
- Initial value: automatically calculated for steady hover at the selected
  helicopter weight, MSA altitude, and temperature.
- Minimum: `0%`.
- Maximum: `100%`.
- Step: `0.1%`.
- Invalid typed values must be clamped to the valid range.
- When focus is not inside an editable control, `ArrowDown` must decrease engine power by 1% and `ArrowUp` must increase it by 1%.
- Holding Shift with either vertical arrow key must use a 5% step.
- Global thrust shortcuts must not override native arrow-key behavior inside editable controls or focused range sliders.
- No auxiliary keyboard-shortcut caption is shown below the engine-power control.

At 100%, no wind, zero yaw rate, and the calibrated default pitch, the model
must produce approximately 14,000 kg of main-rotor lift while the main-rotor and tail-rotor
moments balance. The 13,000 kg maximum helicopter weight is a structural
operating limit, not the full-power sea-level hover-thrust calibration point.

#### Helicopter Weight

- Control type: range slider plus synchronized numeric field.
- Position: first control in the `Helicopter Configuration` section.
- Label: `Weight`.
- Unit: `t`.
- Initial value on application load: `13.0 t`.
- Minimum: `9.0 t`.
- Maximum: `13.0 t`.
- Step: `0.1 t`.
- The control and telemetry value must display one decimal place using a decimal comma (for example `12,4 t`).
- The typed input must accept both a decimal comma and a decimal point.
- Invalid typed values must be clamped to the valid range.
- Changing Weight scales the current `Angular Momentum` value proportionally.
- Changing `Angular Momentum` must not change Weight.
- Reset must preserve the currently selected helicopter weight.

#### MSA Altitude

- Control type: range slider plus synchronized numeric field.
- Position: immediately before the Temperature control in the `Environment` section.
- Label: `MSA altitude`.
- Unit: `m`.
- Initial value on application load: `0 m`.
- Minimum: `0 m`.
- Maximum: `6,000 m`.
- Step: `100 m`.
- Invalid typed values must be rounded to the nearest 100 m and clamped to the valid range.
- Changing altitude must automatically set Temperature to the standard MSA value \(15-0.0065h\) in degrees Celsius.
- The control must update pressure, air density, available engine power, main-rotor lift, tail-rotor blade-element forces, induced velocity, wind force, and the SPUU-52 limit.
- Reset must preserve the currently selected MSA altitude and temperature, consistently with helicopter weight.

#### Temperature

- Position: last control in the `Environment` section.
- Control type: range slider plus synchronized numeric field.
- Label: `Temperature`.
- Unit: `°C`.
- Initial value on application load: `15.0°C`.
- Minimum: `−50°C`.
- Maximum: `+50°C`.
- Step: `0.1°C`.
- Changing Temperature must not change MSA altitude.
- Changing Temperature must update air density, rotor performance, wind force, available engine power above the flat-rating altitude, and the SPUU-52 limit.

#### Angular Momentum

- Position: last item in the `Helicopter Configuration` section.
- Control type: range slider plus synchronized numeric field.
- Label: `Angular Momentum`.
- Physical quantity used by the model: simplified yaw moment of inertia.
- Display unit: `t·m²`.
- Internal calculation unit: `kg·m²`.
- Initial value: `120 t·m²` at `13.0 t`.
- Range at `13.0 t`: `80–160 t·m²`.
- Step: `0.1 t·m²`.
- The minimum and maximum scale linearly with Weight, preserving an equivalent yaw radius of gyration of approximately `2.5–3.5 m`.
- When Weight changes, the current value changes in the same proportion so the selected load-distribution factor is preserved.
- When this control changes, Weight remains unchanged.
- The selected value is used directly as \(I_z\) in the yaw-acceleration calculation.
- Reset preserves the selected value.

#### Wind Speed

- Control type: range slider plus synchronized numeric field.
- Label: `Wind speed`.
- Unit: `m/s`.
- Default: `0 m/s`.
- Minimum: `0 m/s`.
- Maximum: `25 m/s`.
- Step: `0.5 m/s`.
- Invalid typed values must be clamped to the valid range.

#### Wind Direction

- Control type: compass dial plus synchronized numeric field.
- Label: `Wind from`.
- Unit: degrees.
- Default: `0°`.
- Valid range: `0°` to less than `360°`.
- Numeric values must wrap into the range `[0, 360)`.
- The cardinal direction should also be shown, for example `045° NE`.
- The compass arrow must originate on the selected meteorological source side and point inward in the direction the air moves.
- The direction control remains enabled at zero wind so the user can prepare the next case.
- No explanatory caption about the meteorological convention or cyan vector is shown below the wind-direction control.

#### Simulation Controls

- `Pause`/`Resume` and `Reset` must appear together in the upper-right corner of the application header.
- `Pause` freezes the physics state and animation.
- `Resume` continues from the frozen state.
- `Reset` restores all default inputs and the initial simulation state:
  - combined engine power: automatically calculated for steady hover at the
    currently selected helicopter weight, MSA altitude, and temperature, capped at 100%;
  - tail-rotor pitch: subsequently solved to balance the main-rotor reaction
    moment at the calculated power;
  - wind speed: 0 m/s;
  - wind direction: 0°;
  - heading: 0°;
  - yaw rate: 0°/s;
  - elapsed simulation time: 0 s;
  - running state: active.

### 7.3 Graphical Conventions

The central graphic must remain legible without relying on labels alone.

- **Helicopter:** neutral gray body with a clearly identifiable nose and tail.
- **Center of gravity:** small visible marker.
- **Main rotor:** translucent disk or blades with a clockwise rotation indicator.
- **Main-rotor reaction torque:** amber counterclockwise arc.
- **Actual tail-rotor thrust:** blue vector anchored at the tail rotor.
- **Tail-rotor blade angle of attack:** numerical mean and sampled range in the telemetry output.
- **Required tail-rotor thrust:** optional blue dashed vector or a clearly labeled value in the output panel.
- **Wind:** cyan vector placed outside the helicopter and pointing in the direction the air is moving. A nearby label must state the meteorological source direction, for example `Wind from E — 10.0 m/s`.
- **Net yaw direction:** red or magenta curved arrow around the center of gravity when the net moment is materially non-zero.
- **Balanced state:** green `Yaw moments balanced` indication.

Vector length must be proportional to magnitude but visually clamped so that very small vectors remain visible and maximum vectors remain inside the canvas. Numerical values are authoritative when graphical vectors are clamped.

The main-rotor reaction-moment arc and net-moment arc must also encode moment magnitude geometrically. Increasing absolute moment must increase arc span, radius, line thickness, and arrowhead size within safe visual limits. The main-rotor arc disappears at zero main-rotor torque. The net-moment arc disappears inside the balance threshold and changes direction between positive/CCW and negative/CW moment.

The helicopter body and all body-fixed elements must rotate together. The wind vector is world-fixed and must not rotate with the helicopter.

### 7.4 Numerical Output

Values should update at least 10 times per second while the simulation is running.

| Output | Unit | Suggested precision |
|---|---:|---:|
| Heading | degrees | 1 decimal |
| Yaw rate | °/s | 1 decimal |
| Actual tail-rotor thrust | N | whole number |
| Mean tail-rotor blade angle of attack | degrees | 1 decimal |
| Tail-rotor angle-of-attack range | degrees | 1 decimal |
| Relative axial airflow at tail rotor | m/s | 1 decimal |
| Blade elements beyond critical angle | % | whole number |
| Simplified LTE state | text | Normal / Onset / LTE |
| Required tail-rotor thrust | N | whole number |
| Main-rotor reaction torque | N·m | whole number |
| Tail-rotor moment | N·m | whole number |
| Wind yawing moment | N·m | whole number |
| Net yawing moment | N·m | whole number |
| Main-/tail-rotor hover figure of merit | dimensionless | 2 decimals |
| Main-/tail-rotor aerodynamic loss power | kW | whole number |

If a value is close enough to zero for display purposes, it should be displayed as zero rather than as a small alternating positive/negative value.

### 7.5 Dynamic Explanation

The application must generate a short explanation based on the current state. Examples:

- `The yaw moments are balanced. Heading is stable.`
- `Main-rotor reaction torque is greater than the opposing tail-rotor and wind moments, so the helicopter is accelerating counterclockwise.`
- `At the current pedal setting, the tail rotor produces more thrust in this relative airflow, reducing counterclockwise yaw.`
- `Counterclockwise yaw moves the tail through the air and increases the tail-rotor blade angle of attack in this configuration.`
- `The helicopter is rotating clockwise, but the current net moment is slowing that rotation.`

The explanation must distinguish angular velocity from angular acceleration. It must not say that a helicopter is accelerating in a direction merely because it is already rotating in that direction.

## 8. Simulation Model

### 8.1 Modeling Approach

Version 4 uses a deterministic, configurable, low-order yaw model calibrated to the supplied aircraft geometry and power.

All physical constants must be collected in a single clearly named JavaScript configuration object so that the model can be calibrated without rewriting the simulation logic.

Suggested default constants:

| Symbol | Meaning | Suggested value |
|---|---|---:|
| \(P_{max}\) | Combined engine power | 4,000 metric hp (2.942 MW) |
| \(h_{MSA}\) | User-selected MSA altitude | 0–6,000 m |
| \(T_C\) | User-selected outside air temperature | −50°C to +50°C |
| \(h_{flat}\) | End of TV3-117VM-inspired flat rating | 3,600 m |
| \(T_{mr,ref}\) | OGE main-rotor lift at sea-level takeoff power | 14,000 kg |
| \(m_{ref}\) | Reference helicopter mass for yaw inertia | 13,000 kg |
| \(R_{mr}\) | Main-rotor radius | 10.65 m |
| \(n_{mr}\) | Main-rotor speed | 192 rpm |
| \(B_{mr}\) | Number of main-rotor blades | 5 |
| \(c_{mr}\) | Main-rotor blade chord | 0.521 m |
| \(\sigma_{mr}\) | Main-rotor solidity | 0.0777 |
| \(\Delta\theta_{mr}\) | Main-rotor blade twist | -6° |
| \(\kappa_{mr}\) | Main-rotor induced-power factor | 1.20 |
| \(B_{tip,mr}\) | Main-rotor effective tip-loss radius factor | 0.97 |
| \(\bar C_{d,mr}\) | Main-rotor mean profile-drag coefficient | 0.011 |
| \(L_{tr}\) | Tail-rotor moment arm from main hub/CG | \(25.352-10.65-1.954=12.748\) m |
| \(I_z\) | Adjustable yaw moment of inertia (`Angular Momentum` control) | 80,000–160,000 kg·m² at 13,000 kg; default 120,000 kg·m² |
| \(c_1\) | Linear yaw damping coefficient | 1,200 N·m·s/rad |
| \(c_2\) | Quadratic yaw damping coefficient | 1,000 N·m·s²/rad² |
| \(\rho_0\) | Standard sea-level air density | 1.225 kg/m³ |
| \(C_{d,y}\) | Effective lateral drag coefficient | 1.0 |
| \(A_y\) | Effective lateral area | 25 m² |
| \(x_{cp}\) | Longitudinal center-of-pressure offset from CG | -1.2 m |
| \(R_{tr}\) | Tail-rotor radius | 1.954 m |
| \(S_{tr}\) | Combined working tail-blade planform area | 1.430 m² |
| \(r_{root}\) | Aerodynamic blade root cutout | \(0.20R_{tr}\) |
| \(B_{tr}\) | Number of tail-rotor blades | 3 |
| \(c_{tr}\) | Tail-rotor blade chord | 0.305 m |
| \(\sigma_{tr}\) | Nominal tail-rotor solidity \(Bc/(\pi R)\) | 0.149 |
| \(n_{tr}\) | Fixed tail-rotor speed | 1,120 rpm |
| \(P_{tr,gear,max}\) | Published maximum tail-gearbox power, retained as reference rather than a hard simulation limit | 442 kW |
| \(\theta_{tr,0.7}\) | Geometric pitch specified at \(r/R=0.7\) | −6° to the SPUU-52 limit |
| \(a\) | Linear lift-curve slope | 5.7 rad⁻¹ |
| \(C_{l,min}\) | Minimum section lift coefficient | -1.2 |
| \(C_{l,max}\) | Maximum section lift coefficient | 1.5 |
| \(\alpha_{0L}\) | Provisional NACA 230-family zero-lift angle | -1.2° |
| \(\alpha_{crit}\) | Critical positive blade angle of attack | 12° |
| \(\alpha_{collapse}\) | Angle at which the modeled thrust collapse is fully developed | 19° |
| \(f_{post}\) | Remaining lift fraction after collapse | 0.18 |
| \(C_{d,0}\) | Profile drag coefficient at zero lift | 0.0069 |
| \(k_d\) | Induced/profile drag polar coefficient | 0.015 |
| \(\kappa_{tr}\) | Tail-rotor induced-power factor | 1.20 |
| \(B_{tip,tr}\) | Tail-rotor effective tip-loss radius factor | 0.97 |
| \(FM_{tr,max}\) | Empirical maximum tail-rotor hover figure of merit | 0.52 |
| \(N_r\) | Radial blade-element samples | 12 |
| \(N_\beta\) | Azimuth samples over one revolution | 24 |

The tail-blade working area is derived from the documented three-blade
geometry, \(3 \times 0.305 \times 1.954 \times (1-0.20)\), rather than from
the previously supplied 2.0 m² value. The latter matches the documented
horizontal-stabilizer area and is not used as tail-blade planform area.

Published operational limits such as 12°/s maximum hover-turn rate, at least
three seconds for a full pedal reversal, and at least five seconds for a full
collective movement are not used as aerodynamic calibration targets. They are
operational safety limits and would artificially suppress the unconstrained
response explored by this simulator.

The combined-power calibration condition is:

\[
T_{tr}(\theta_{trim})L_{tr}
= \frac{P_{max}-P_{tr}(\theta_{trim})}{\Omega_{mr}}
\]

This produces a trimmed state at 100% engine power with no wind. The
blade-element model calculates tail-rotor shaft power as well as thrust, so
both rotors share the 4,000 metric-horsepower limit. At sea level, this point
is calibrated to a 14,000 kgf full-power OGE equivalent. The 13,000 kg maximum
takeoff mass therefore retains about 7.7% thrust margin for vertical climb.

At initialization, the application must numerically solve for \(\theta_{trim}\)
within −6° to the current SPUU-52 limit. On application load and Reset, power is solved first for the
selected weight, MSA altitude, and temperature, then tail-rotor pitch is solved for yaw
balance at that power. While the simulation is paused, each user change to the
power input automatically re-trims tail-rotor pitch to minimize the net yawing
moment. This coupling is one-way: a user change to tail-rotor pitch never changes
power. While the simulation is running, user changes to either input remain
independent.

#### 8.1.1 MSA Altitude, Temperature, Air Density, and Available Power

Within the modeled 0–6,000 m range, standard MSA/ISA temperature and pressure
are:

\[
T_{MSA}(h)=T_0-Lh
\]

\[
P(h)=P_0
\left(1-\frac{Lh}{T_0}\right)^{\frac{g}{RL}}
\]

where \(T_0=288.15\ \mathrm{K}\), \(L=0.0065\ \mathrm{K/m}\),
\(g=9.80665\ \mathrm{m/s^2}\), and \(R=287.05287\ \mathrm{J/(kg\,K)}\).
Changing MSA altitude sets the temperature input to \(T_{MSA}(h)\). A
subsequent manual temperature change leaves \(h\) unchanged.

Air density uses standard pressure at the selected altitude and the selected
temperature:

\[
\rho(h,T_C)=\frac{P(h)}{R(T_C+273.15)}
\]

The simplified TV3-117VM-inspired power factor is flat-rated to 3,600 m:

\[
f_{eng}(h,T_C)=
\begin{cases}
1, & h\leq h_{flat}\\
\frac{\rho(h,T_C)}{\rho(h_{flat},T_{MSA}(h_{flat}))}, & h>h_{flat}
\end{cases}
\]

The user power input \(u\) is applied to that altitude-limited rating:

\[
P_{available}=uP_{max}f_{eng}(h,T_C)
\]

For the pitch limiter, the application uses standard pressure \(P(h)\) at the
selected MSA altitude and the selected temperature \(T_C\), then applies the
published SPUU-52 nominal calibration:

\[
s=\operatorname{clamp}_{0}^{100}
\left(50+1.05(T_C-10)+0.28(760-P_{mmHg})\right)
\]

\[
\theta_{max}=17^\circ20'
+\frac{s}{100}\left(23^\circ15'-17^\circ20'\right)
\]

The result is rounded downward to the nearest 0.1° command step so the UI never
offers a value above the calculated physical limit.

### 8.2 Main-Rotor Power, Efficiency, and Reaction Torque

The power and reaction torque available to the main rotor are:

\[
P_{mr}=\max(0,P_{available}-P_{tr}),\qquad
Q_{mr}=\frac{P_{mr}}{\Omega_{mr}}
\]

The main rotor uses an explicit fixed-RPM aerodynamic power balance. The ideal
hover power, induced power with nonuniform-inflow and tip-loss corrections, and
profile power are:

\[
P_{ideal,mr} =
\frac{T_{mr}^{3/2}}{\sqrt{2\rho A_{mr}}}
\]

\[
A_{eff,mr}=\pi(B_{tip,mr}R_{mr})^2,\qquad
P_{i,mr}=\kappa_{mr}
\frac{T_{mr}^{3/2}}{\sqrt{2\rho A_{eff,mr}}}
\]

\[
P_{0,mr}=
\rho A_{mr}(\Omega_{mr}R_{mr})^3
\frac{\sigma_{mr}\bar C_{d,mr}}{8}
\]

The nominal sea-level calibration supplies an empirical upper bound on hover
figure of merit:

\[
FM_{mr,ref}=\frac{P_{ideal,mr,ref}}{P_{mr,ref}}
\]

\[
P_{req,mr}(T)=
\max\left(P_{i,mr}+P_{0,mr},
\frac{P_{ideal,mr}}{FM_{mr,ref}}\right)
\]

At every update, \(T_{mr}\) is found by bounded numerical inversion of
\(P_{req,mr}(T)=P_{mr}\). This prevents the main rotor from producing the
calibrated thrust without paying both induced and profile power.

For the version 4 clockwise main rotor, \(Q_{mr}\) acts counterclockwise on the fuselage and is therefore positive under the sign convention in Section 6.

### 8.3 Wind Vector

For wind speed \(V_w\) and meteorological source direction \(\theta_w\), the world-space air-velocity vector points 180° away from the selected source direction.

With world \(x\) pointing east and world \(y\) pointing north:

\[
\vec{V}_{air,world} =
-V_w
\begin{bmatrix}
\sin(\theta_w) \\
\cos(\theta_w)
\end{bmatrix}
\]

The vector must be transformed into helicopter body coordinates using the current heading before calculating fuselage moment and tail-rotor inflow.

#### 8.3.1 Mi-8MTV / Mi-17 OGE Wind Correction

The model applies the digitized limiting-weight correction from the Russian
Mi-8MTV-5-1 Flight Manual, Section 1, Figure 1.2, for helicopter takeoff and
landing without ground effect at a 20 m hover height. The source graph expresses
the correction as a change in limiting weight, \(\Delta G\), in kgf.

| Wind speed, m/s | Front, kg | Left/right crosswind, kg | Rear, kg |
| ---: | ---: | ---: | ---: |
| 0 | 0 | 0 | 0 |
| 1 | +60 | −150 | −260 |
| 2 | +120 | −220 | −500 |
| 3 | +180 | −170 | −650 |
| 4 | +250 | 0 | −750 |
| 5 | +370 | +150 | −800 |
| 6 | +490 | +310 | −775 |
| 7 | +625 | +475 | −700 |
| 8 | +770 | +650 | −600 |
| 9 | +930 | +820 | −475 |
| 10 | +1,100 | +1,000 | −325 |

The digitized source scale is used through 10 m/s. Linear interpolation is used
between speed points. The Flight Manual has one common curve for left and right
crosswind, so their limiting-weight corrections are identical.

The [Russian Mi-8MTV2 aerodynamic manual](https://www.digitalcombatsimulator.ru/upload/iblock/458/DCS-Mi-8MTV2_FlightManual_RU.pdf)
describes the change from axial to oblique main-rotor flow over approximately
20-40 km/h. For wind speeds above the 10 m/s nomogram
scale, the implementation continues the final 9-10 m/s slope of each directional
curve up to the upper transition boundary of 40 km/h (11.11 m/s). This makes
required main-rotor power continue to decrease with increasing wind for every
direction until oblique flow is established. Above 11.11 m/s the transition value
is held because forward-flight main-rotor aerodynamics are outside this hover
model's scope.

Wind direction is evaluated relative to the helicopter's current heading. The
front, side, and rear curves are blended smoothly between the four cardinal
directions. The full correction is used to change required OGE hover power, so
tail-rotor power demand remains a separate consumer of the shared engine-power
budget. For the current main-rotor lift-capability readout only, the correction
is multiplied by the ratio of actual main-rotor power to still-air hover power,
clamped from 0 to 1; this prevents a nonzero indicated lift at zero power.

For the vertical-performance calculation, a positive correction reduces the
equivalent weight for which hover power is evaluated:

\[
G_{equiv} = G - \Delta G
\]

The interface shows only the correction applied at the current relative wind
direction. The four cardinal-direction audit table and explanatory source note
are intentionally omitted from the simulator panel.

### 8.4 Wind-Induced Fuselage Yawing Moment

The model uses the lateral component of wind in body coordinates, \(V_y\), where positive is toward the helicopter's left, consistently with the body axes in Section 6.

The effective lateral aerodynamic force is:

\[
F_{wind,y} =
\frac{1}{2} \rho C_{d,y} A_y V_y |V_y|
\]

The yawing moment is calculated from the configured center-of-pressure location:

\[
Q_{wind} = x_{cp} \cdot F_{wind,y}
\]

The sign follows directly from the body-axis geometry. The implementation must be covered by directional tests so that reversing the crosswind reverses the wind yawing moment.

This is a deliberately simplified weathervane model. It does not model separate aerodynamic forces on every fuselage component.

### 8.5 Relative Airflow at the Tail Rotor

The pitch input sets geometric tail-rotor blade pitch at \(r/R=0.7\). Blade angle of attack is still derived from local relative airflow and is not equal to geometric pitch.

The useful tail-rotor thrust direction is the body-left direction:

\[
\hat{n}_{T} = [0, 1, 0]
\]

The positive through-disk inflow direction is opposite to useful thrust:

\[
\hat{n}_{inflow} = -\hat{n}_{T}
\]

The tail-rotor hub moves because the fuselage yaws. Its body-axis velocity is:

\[
\vec{V}_{hub,yaw} =
\vec{\omega}_{body} \times \vec{r}_{tr}
\]

where:

\[
\vec{\omega}_{body} = [0, 0, \omega]
\]

The external air velocity relative to the tail-rotor hub is:

\[
\vec{V}_{ext,tr} =
\vec{V}_{air,body} - \vec{V}_{hub,yaw}
\]

This equation is mandatory: it is the mechanism by which both wind and helicopter yaw rate affect tail-rotor blade angle of attack.

The external axial flow through the disk is:

\[
V_{ax,ext} =
\vec{V}_{ext,tr} \cdot \hat{n}_{inflow}
\]

The in-plane airflow is:

\[
\vec{V}_{plane} =
\vec{V}_{ext,tr}
- V_{ax,ext}\hat{n}_{inflow}
\]

The implementation must show the signed \(V_{ax,ext}\) value or an equivalent clearly labeled relative-flow value in the output panel.

### 8.6 Tail-Rotor Blade Angle of Attack

The tail rotor is evaluated using a low-order blade-element calculation across radius and rotor azimuth. The result is averaged over one complete rotor revolution so that the displayed thrust does not flicker at blade-passage frequency.

For each radial station \(r\) from \(r_{root}\) to \(R_{tr}\), each sampled rotor azimuth \(\beta\), and blade index \(b\), define the blade azimuth:

\[
\beta_b =
\beta + \frac{2\pi b}{B_{tr}}
\]

Then define:

- \(\hat{e}_t(\beta_b)\): local blade tangential-direction unit vector in the rotor disk;
- \(v_i\): induced velocity through the tail-rotor disk;
- \(V_{plane,t} = \vec{V}_{plane} \cdot \hat{e}_t(\beta_b)\): local in-plane wind component parallel to blade motion.

The local tangential relative-airflow speed is:

\[
U_t(r,\beta_b) =
\Omega_{tr}r - V_{plane,t}
\]

The local perpendicular/axial airflow speed is:

\[
U_p =
v_i + V_{ax,ext}
\]

The local inflow angle is:

\[
\phi(r,\beta_b) =
\operatorname{atan2}(U_p, U_t)
\]

The local blade angle of attack is:

\[
\alpha(r,\beta_b) =
\theta_{tr} - \phi(r,\beta_b)
\]

The calculation must retain the sign of \(\alpha\). Angles must be calculated internally in radians and converted to degrees only for display.

This formulation accounts for:

- disk-normal wind changing \(U_p\);
- wind within the rotor plane changing \(U_t\) differently around blade azimuth;
- yaw rate changing the tail-hub velocity and therefore \(V_{ax,ext}\);
- fixed geometric pitch producing a variable angle of attack.

The application must calculate and expose:

- area-weighted mean angle of attack over the modeled blade span and full revolution;
- minimum and maximum angle of attack over the sampled elements;
- optionally, mean inflow angle.

Root-cutout elements are excluded from the displayed minimum and maximum. This prevents non-lifting blade-root geometry from dominating the educational result.

### 8.7 Blade-Element Tail-Rotor Thrust

For each blade element of width \(dr\):

\[
W(r,\beta_b) =
\sqrt{U_t^2 + U_p^2}
\]

\[
C_{l,linear}(r,\beta_b) =
\operatorname{clamp}
\left(
a(\alpha-\alpha_{0L}),
C_{l,min},
C_{l,max}
\right)
\]

For positive angle of attack up to the critical angle:

\[
C_l = C_{l,linear}
\quad \text{for } \alpha \leq \alpha_{crit}
\]

Between the critical and collapse angles, the positive lift coefficient must decrease smoothly and monotonically:

\[
s =
\operatorname{smoothstep}
\left(
0,
1,
\frac{\alpha-\alpha_{crit}}
{\alpha_{collapse}-\alpha_{crit}}
\right)
\]

\[
C_l =
C_l(\alpha_{crit})
\left[
1-s(1-f_{post})
\right]
\quad \text{for } \alpha > \alpha_{crit}
\]

At and above \(\alpha_{collapse}\), the remaining positive lift coefficient is \(f_{post}C_{l,max}\). Negative-angle behavior may continue to use the bounded linear model in version 3.

\[
C_d(r,\beta_b) =
C_{d,0} + k_d C_l^2
\]

\[
dL =
\frac{1}{2}\rho W^2 c_{tr} C_l\,dr
\]

\[
dD =
\frac{1}{2}\rho W^2 c_{tr} C_d\,dr
\]

The element's useful axial thrust contribution is:

\[
dT =
dL\cos(\phi) - dD\sin(\phi)
\]

Actual tail-rotor thrust is the sum across the modeled blades and radial stations, averaged across the \(N_\beta\) azimuth samples:

\[
T_{tr,actual} =
\frac{1}{N_\beta}
\sum_{\beta}
\sum_{b=1}^{B_{tr}}
\sum_r dT
\]

Induced velocity is solved quasi-steadily using disk momentum theory:

\[
A_{tr} = \pi R_{tr}^2
\]

\[
v_i =
\sqrt{
\frac{\max(T_{tr,actual},0)}
{2\rho A_{tr}}
}
\]

Because thrust depends on induced velocity and induced velocity depends on thrust, the implementation must use a bounded numerical iteration. Four to eight relaxed iterations per calculation are sufficient. The last finite solution must be retained if an iteration fails to converge. Dynamic inflow lag is not modeled in version 3.

The tail-rotor blade-element torque is separated into lift-induced and
profile-drag components. Aerodynamic shaft power is corrected for nonuniform
inflow and tip losses:

\[
P_{i,tr}=
\max\left(
\frac{\kappa_{tr}}{B_{tip,tr}}P_{i,BEM},
\kappa_{tr}
\frac{T_{tr}^{3/2}}{\sqrt{2\rho A_{eff,tr}}}
\right)
\]

\[
P_{req,tr}=P_{i,tr}+P_{0,tr}+P_{cal,tr}
\]

where \(P_{cal,tr}\geq0\) is the residual aerodynamic calibration loss needed
to enforce:

\[
FM_{tr}=
\frac{P_{ideal,tr}}{P_{req,tr}}
\leq FM_{tr,max}=0.52
\]

This calibration represents unresolved three-dimensional wake and blade
interaction losses without treating them as mechanical drivetrain losses.
Both rotors remain at their nominal fixed speeds. If the selected engine power
is below the aerodynamic power required to sustain those speeds, the
application must show an unsustainable fixed-RPM operating-point warning; it
must not silently reduce either rotor RPM.

The tail-rotor yawing moment opposes the main-rotor reaction torque:

\[
Q_{tr} = -T_{tr,actual} \cdot L_{tr}
\]

An element is considered beyond the critical angle when \(\alpha > \alpha_{crit}\). The application must expose the percentage of sampled elements in this state. The UI state is:

- `Normal` when no sampled element is beyond the critical angle;
- `LTE onset` when at least one but less than 20% of sampled elements are beyond it;
- `LTE — thrust loss` when 20% or more are beyond it.

The post-stall curve is a deliberately simplified educational LTE approximation. Real LTE is an aerodynamic control-margin condition with multiple possible aerodynamic interactions; it is not defined solely by a universal blade stall angle.

### 8.8 Required Tail-Rotor Thrust

The tail-rotor thrust required to balance the main-rotor and wind moments at the current instant, excluding rotational damping, is:

\[
T_{tr,required} =
\frac{Q_{mr} + Q_{wind}}{L_{tr}}
\]

If this value is negative, the numerical output may show the signed value, but the explanation must state that balancing requires thrust in the opposite direction and an appropriate left-pedal command.

The difference between required and actual tail-rotor thrust is:

\[
\Delta T_{tr} =
T_{tr,required} - T_{tr,actual}
\]

This difference is useful for the educational explanation and balance indication.

### 8.9 Yaw Dynamics

The total yawing moment before damping is:

\[
Q_{rotors+wind} = Q_{mr} + Q_{tr} + Q_{wind}
\]

Yaw damping is:

\[
Q_{damping} =
-c_1\omega - c_2\omega|\omega|
\]

This damping term represents residual fuselage and stabilizing-surface damping only. The separate change in tail-rotor thrust caused by yaw-rate-induced relative airflow must remain active and must not be replaced by this generic damping term.

The net moment is:

\[
Q_{net} =
Q_{mr} + Q_{tr} + Q_{wind} + Q_{damping}
\]

Angular acceleration is:

\[
\alpha = \frac{Q_{net}}{I_z}
\]

The `Angular Momentum` control represents the simplified yaw moment of inertia
\(I_z\). When Weight changes from \(m_0\) to \(m_1\), the application preserves
the selected load-distribution factor by scaling:

\[
I_{z,1} = I_{z,0}\frac{m_1}{m_0}
\]

Directly changing \(I_z\) does not modify \(m\).

The state is integrated over time:

\[
\omega_{t+\Delta t} = \omega_t + \alpha \Delta t
\]

\[
\psi_{t+\Delta t} = \psi_t + \omega_{t+\Delta t}\Delta t
\]

where:

- \(\omega\) is yaw rate in radians per second;
- \(\psi\) is heading/yaw angle;
- \(\Delta t\) is the simulation time step.

The internal calculation must use radians. Degrees are used only for user input and display.

### 8.10 Numerical Integration

- Rendering must use `requestAnimationFrame`.
- Physics must use a fixed or capped time step to remain stable when the browser stalls or the tab becomes inactive.
- Recommended physics step: `1/120 s`.
- Maximum accepted elapsed frame time: `0.05 s`.
- A frame may run multiple fixed physics steps to catch up, up to a safe limit.
- Simulation time must not advance while paused.
- The result must be broadly independent of display refresh rate.

### 8.11 Stability Thresholds

Suggested display thresholds:

- Balanced moment: \(|Q_{rotors+wind}| < 10\ \text{N·m}\).
- Stable yaw rate: \(|\omega| < 0.05^\circ/s\).
- Zero-display threshold for yaw rate: \(0.05^\circ/s\).
- Zero-display threshold for moment: `1 N·m`.

These thresholds affect labels and display rounding only. They must not introduce discontinuities into the physics model.

## 9. Visual Animation

- The main-rotor graphic must visibly rotate clockwise at a constant symbolic
  animation speed relative to the screen, independent of engine-power input
  and helicopter yaw. Because the rotor graphic is nested inside the rotating
  helicopter group, its local transform must compensate for the helicopter
  heading transform.
- Main-rotor animation speed represents rotor direction, not physical rotor RPM.
- The helicopter body must rotate according to the calculated heading.
- The helicopter's center of gravity remains fixed at the center of the simulation canvas.
- The tail-rotor propeller and blades must not be drawn in the top-down view.
- The tail-rotor thrust vectors must remain anchored to the tail and rotate with the body.
- The wind vector remains aligned to the world/compass direction.
- The visual yaw motion must use the simulated heading without cosmetic exaggeration.
- If `prefers-reduced-motion` is enabled:
  - decorative rotor blur/rotation should be reduced or replaced by a static clockwise arrow;
  - the calculated helicopter heading must still update because it carries essential information;
  - numerical values must remain fully functional.

## 10. Functional Requirements

### FR-01 — Self-Contained Delivery

The complete application must run from one HTML file opened directly in a modern browser. HTML, CSS, JavaScript, SVG, fonts, icons, and explanatory content must be embedded in that file. No web server is required.

### FR-02 — Offline Operation

After the file is downloaded, all functionality must work without an internet connection. The file must not request external scripts, styles, fonts, images, analytics, or APIs.

### FR-03 — Immediate Feedback

Changing any input must affect the calculated forces, moments, and vector graphics immediately without page reload.

### FR-04 — Continuous Simulation

While running, the application must continuously integrate yaw rate and heading.

### FR-05 — Directional Pedals

The application must provide a tail-rotor pitch control from −6° to the current SPUU-52 limit at \(r/R=0.7\) as the first `Flight Controls` control. Input changes must immediately change commanded geometric blade pitch, tail-rotor thrust, power split, yawing moment, LTE state, and live operating point.

The pedal control must also support global left/right arrow-key input as specified in Section 7.2.

### FR-06 — Tail-Rotor Outputs

The application must show actual pedal-commanded tail-rotor thrust and required zero-yaw tail-rotor thrust as distinct values. It must also show representative blade angle of attack and the angle-of-attack range calculated from local relative airflow.

### FR-07 — Direction Clarity

Yaw and wind values must show both magnitude and direction in words or standard abbreviations. Color alone is insufficient.

### FR-08 — Reset

Reset must reproduce the trimmed, no-wind default state deterministically.

### FR-09 — Pause

Pause must freeze heading, yaw rate, animation time, and all state integration. Input changes made while paused may update static force and moment calculations, but integration must resume only when the user selects Resume.

### FR-10 — Explanation

The application must explain whether the helicopter is:

- stable;
- rotating clockwise;
- rotating counterclockwise;
- accelerating in the current rotation direction;
- slowing down despite still rotating.

### FR-11 — Limitation Notice

The page must visibly state:

`Simplified educational LTE approximation. Real LTE also depends on aircraft-specific aerodynamic interactions that are not modeled here.`

### FR-12 — Live LTE Chart

The application must plot calculated tail-rotor thrust against peak local blade angle of attack. The chart must label both axes, mark \(\alpha_{crit}\), distinguish the post-stall region, and show the current operating point without requiring user interaction.

The vertical axis must remain fixed from 0 to 35,000 N and must never auto-scale. The reference curve must be generated once from the trimmed 100%, no-wind, zero-yaw condition and remain visually unchanged while inputs and dynamic state change. Only the live operating point and guide lines move. The operating point must continue to use the fully iterated blade-element solution.

Changes to the current operating point, guide lines, and displayed chart values must be interpolated between live samples rather than replaced in one frame. A transition from `Normal` directly into a fully developed LTE display must pass through a short `LTE onset` presentation state. This visual smoothing must not alter or delay the underlying physics calculation.

## 11. Non-Functional Requirements

### 11.1 Browser Support

The application should support current stable desktop and mobile versions of:

- Google Chrome;
- Microsoft Edge;
- Mozilla Firefox;
- Apple Safari.

No browser extension, installation, or local server may be required.

### 11.2 Performance

- Target rendering rate: 60 frames per second on a typical modern laptop.
- The main animation loop should avoid unnecessary DOM allocation.
- Numerical output may be throttled to 10–20 updates per second while graphics continue at the display refresh rate.
- The application should become interactive within one second after opening on a typical modern laptop.

### 11.3 Accessibility

- All controls must be keyboard accessible.
- Every input must have a programmatically associated label.
- Range and numeric inputs must expose units and current values.
- Focus indicators must be clearly visible.
- Text and critical graphic elements must meet WCAG 2.1 AA contrast targets where applicable.
- Direction and state must not be communicated by color alone.
- The simulation canvas must have a concise accessible description.
- Live numerical values should not be announced on every animation frame. An accessible summary may update at a slower rate or on input changes.

### 11.4 Responsive Design

- Minimum supported viewport width: 320 CSS pixels.
- No horizontal page scrolling at supported widths.
- The simulation must retain a square or near-square usable drawing area.
- Touch targets should be at least 44 by 44 CSS pixels where practical.

### 11.5 Privacy and Security

- No personal data is collected.
- No network requests are made.
- No cookies, local storage, telemetry, or analytics are required.
- User-entered numeric values must be parsed and validated before use.
- The application must not use `eval`, dynamic remote imports, or runtime HTML injection from user input.

## 12. Technical Architecture

The delivered HTML file should use:

- semantic HTML for controls and output;
- embedded CSS in a `<style>` element;
- embedded JavaScript in a `<script>` element;
- inline SVG or HTML Canvas for the top-down visualization.

SVG is preferred for version 3 because it provides:

- crisp scaling;
- accessible structure;
- easy vector rotation and anchoring;
- straightforward arrow markers and labels.

Suggested internal modules or logical sections within the one script:

1. `MODEL_CONFIG` — physical and display constants.
2. `state` — inputs, heading, yaw rate, pause state, and elapsed time.
3. input validation and event handling.
4. coordinate and vector utilities.
5. force and moment calculation.
6. fixed-step physics integration.
7. SVG rendering.
8. numerical output rendering.
9. explanation generation.
10. reset and pause/resume behavior.

The code may remain in one file while using JavaScript classes, closures, or module-style objects for separation of concerns. No build step or package dependency may be required for the final artifact.

## 13. Data and State

Minimum runtime state:

```text
tailRotorPitchDegrees
enginePowerPercent
helicopterWeightKg
yawInertiaKgM2
msaAltitudeM
airTemperatureC
windSpeedMps
windFromDegrees
headingRadians
yawRateRadiansPerSecond
nominalTrim
tailRotorInducedVelocityMps
simulationTimeSeconds
isPaused
lastFrameTimestamp
physicsAccumulator
```

All derived values, including forces, moments, vector directions, and explanation text, should be recalculated from the current input and dynamic state rather than stored independently.

No state persistence is required between page loads.

## 14. Validation and Error Handling

- Empty or non-numeric typed input must not propagate `NaN` into the simulation.
- During invalid text editing, the last valid value may remain active.
- On blur or Enter, values must be normalized to the allowed range.
- Wind direction must wrap rather than clamp:
  - `360°` becomes `0°`;
  - `-10°` becomes `350°`.
- If an unexpected non-finite calculated value occurs:
  - pause the simulation;
  - restore the last finite dynamic state;
  - show a concise error message;
  - allow Reset to recover.

## 15. Test Requirements

### 15.1 Calculation Tests

The implementation must verify at minimum:

1. At 100% engine power, calibrated trim pitch, zero wind, and zero yaw rate:
   - main-rotor lift is approximately 14,000 kg within display rounding;
   - main-rotor torque equals the magnitude of tail-rotor moment;
   - net moment is zero within floating-point tolerance;
   - yaw acceleration is zero.
2. At nominal trim, main-rotor and tail-rotor shaft power sum to 4,000 metric horsepower within display rounding.
   - tail-rotor hover figure of merit does not exceed 0.52;
   - main-rotor hover figure of merit matches its calibrated reference value;
   - both rotors retain their nominal displayed RPM.
3. At zero wind, decreasing engine power below 100% produces clockwise net moment when pitch is held at the nominal trim value.
4. Opposite crosswind directions produce opposite wind yawing-moment signs.
5. With geometric pitch held constant, opposite disk-normal wind directions produce opposite changes in mean blade angle of attack.
6. A change in mean blade angle of attack produces a corresponding change in calculated tail-rotor thrust.
7. At zero wind, non-zero yaw rate changes relative axial airflow at the tail-rotor hub.
8. Opposite yaw rates produce opposite changes in tail-rotor mean angle of attack and thrust.
9. Wind within the tail-rotor disk plane produces an azimuthal angle-of-attack variation.
10. At the trimmed default state, startup calibration balances tail thrust against the power-derived main-rotor torque within 0.5%.
11. The blade-element and induced-velocity iteration remains finite over the full valid input range.
12. Induced, profile, calibration-loss, ideal, and total shaft powers are finite and non-negative at the nominal operating point.
13. At a deliberately underpowered setting, the application reports that fixed RPM is unsustainable and does not silently reduce tail-rotor RPM.
14. Lift coefficient and integrated thrust decrease substantially between \(\alpha_{crit}\) and \(\alpha_{collapse}\).
15. A tested post-stall operating point produces less than 50% of the peak pre-stall tail-rotor thrust.
16. The LTE chart contains the critical-angle marker and current operating point.
17. The LTE chart current point matches the numerical maximum local angle of attack and actual thrust within display rounding.
18. The damping moment always opposes non-zero yaw rate.
19. Wind direction conversion is correct for 0°, 90°, 180°, and 270°.
20. Heading wraps cleanly through 0°/360°.
21. Pause prevents all dynamic-state integration.
22. Reset returns the exact default dynamic state, preserves the selected
    helicopter weight, yaw moment of inertia, MSA altitude, and temperature, recalculates the combined engine
    power required for steady hover, and subsequently trims tail-rotor pitch
    for yaw balance at that power.
23. No displayed calculated value becomes `NaN` or infinite for any valid input.
24. At the default trim pitch and 100% engine power, the no-wind zero-yaw state remains finite and balanced.
25. A change from a normal operating point to a modeled LTE operating point moves the graph marker and guide lines continuously over multiple animation frames and exposes `LTE onset` before `LTE — thrust loss`.
26. Changing wind, yaw rate, or engine-power input does not change the vertical-axis range or reference-curve path; the vertical tick labels remain 0, 8.75k, 17.5k, 26.25k, and 35k N.
27. Left and right arrow keys change tail-rotor pitch by 0.1°, Shift modifies the step to 1°, limits remain enforced, and editable controls retain their native keyboard behavior.
28. Increasing main-rotor torque increases the amber moment arc's span, radius, stroke width, and arrowhead size; zero main-rotor torque hides it.
29. Increasing absolute net yaw moment increases the magenta moment arc's span, radius, stroke width, and arrowhead size; balanced moment hides it and reversing moment reverses the visible arrow direction.
30. Up and down arrow keys change engine power by 1%, Shift modifies the step to 5%, the 0–100% limits remain enforced, and editable controls retain their native keyboard behavior.
31. The helicopter-weight slider and numeric field stay synchronized, enforce the 9.0–13.0 t range in 0.1 t steps, display one decimal place with a decimal comma, accept either comma or point as typed input, initialize to 13.0 t, and preserve the selected value through Reset.
32. Changing helicopter weight scales the current `Angular Momentum` value in the same proportion.
33. Changing `Angular Momentum` does not change helicopter weight, and a lower selected value produces a proportionally larger yaw acceleration at equal non-zero net yaw moment.
34. The MSA-altitude slider and numeric field stay synchronized, enforce the 0–6,000 m range in 100 m steps, initialize to 0 m, and preserve the selected value through Reset.
35. Changing MSA altitude sets Temperature to the corresponding standard-atmosphere value, from 15.0°C at 0 m to −24.0°C at 6,000 m.
36. Changing Temperature leaves MSA altitude unchanged and the temperature control enforces the −50°C to +50°C range.
37. At unchanged altitude, increasing Temperature decreases air density.
38. Maximum engine power remains 4,000 metric horsepower through 3,600 m and decreases with density above 3,600 m.
39. At unchanged engine-power input and standard MSA temperature, increasing altitude decreases main-rotor lift.
40. At 3,600 m and 100% power, the main rotor produces less lift than at sea level even though the engine remains flat-rated.
41. Tail-rotor blade-element forces and induced-velocity solution use the selected altitude-and-temperature air density and remain finite across the full range.
42. On initial application load and after Reset, combined engine power is the
    nearest 0.1 percentage point that makes calculated main-rotor lift equal the
    selected helicopter weight. If the required value exceeds the
    altitude-limited available power, the control is capped at 100%.
43. After automatic hover power is selected, tail-rotor pitch is solved to
    minimize the no-wind yaw-moment imbalance at that power and density
    altitude and is displayed in 0.1° increments.
44. While paused, changing engine power automatically re-trims tail-rotor pitch
    to minimize net yawing moment; changing tail-rotor pitch does not alter
    engine power, and no automatic re-trim occurs while the simulation is running.
45. At standard MSA temperature, the SPUU-52 limit is 20.6° at 0 m and reaches
    the 23.2° UI maximum by approximately 3,000 m. Altitude or temperature
    changes update the pitch inputs immediately and clamp an out-of-range
    current pitch.
46. At 4 m/s, the OGE nomogram returns +250 kg for front wind, 0 kg for
    left and right crosswind, and −750 kg for rear wind.
47. At every speed, left and right crosswind return identical OGE corrections;
    arbitrary relative directions interpolate continuously between the front,
    side, and rear curves.
48. A positive OGE correction lowers equivalent hover-power demand, a negative
    correction raises it, and this required-power correction does not depend on
    how much of the shared engine power the tail rotor currently consumes.
49. From 10 m/s to 11.11 m/s, every directional OGE correction continues with
    its final nomogram slope, so required main-rotor power decreases as wind
    speed rises. Above 11.11 m/s the result remains finite and holds the
    oblique-flow-transition value.
50. Wind above the OGE nomogram range continues to change tail-rotor blade angle
    of attack and thrust through the blade-element model; the main-rotor
    transition cap must not clamp tail-rotor relative airflow.

### 15.2 Interaction Tests

- Sliders and numeric fields remain synchronized.
- Click-and-drag with a mouse updates every range control continuously without
  starting the browser's native drag-and-drop operation.
- The Yaw Pedals slider retains pointer capture while dragging so that the
  control continues to respond if the pointer briefly leaves the thumb.
- The compass dial and degree field remain synchronized.
- Keyboard operation works for every control.
- Rapid input changes do not destabilize the simulation.
- Reset works while running and while paused.
- Inputs changed while paused are reflected correctly when resumed.

### 15.3 Visual Tests

- Main rotor visibly turns clockwise.
- The fuselage initially reacts counterclockwise when main-rotor torque exceeds compensation.
- No rotating tail-rotor propeller or blade graphic is visible in the top-down view.
- Tail-rotor thrust vectors remain attached to the tail while the helicopter rotates.
- Displayed tail-rotor angle of attack responds to both wind changes and yaw-rate changes.
- Wind vector does not rotate with the helicopter.
- Wind-vector arrow direction matches air movement, while its label correctly states wind source direction.
- No vector or label is unintentionally clipped at minimum supported viewport size.
- CW, CCW, and stable states are distinguishable without color.

## 16. Acceptance Criteria

Version 4 is accepted when all of the following are true:

1. The product is delivered as one HTML file and operates by opening that file directly.
2. It makes no external network request and remains fully functional offline.
3. A top-down generic helicopter is clearly visible and its main rotor is shown rotating clockwise.
4. The user can set tail-rotor pitch, combined engine-power percentage, helicopter weight, yaw moment of inertia through `Angular Momentum`, MSA altitude, temperature, wind speed, and wind source direction.
5. The helicopter heading changes continuously in response to calculated net yaw moment.
6. Yaw rate is shown graphically and numerically with CW/CCW direction.
7. Actual pedal-commanded tail-rotor thrust is shown graphically and numerically.
8. Mean tail-rotor blade angle of attack and its sampled range are shown numerically.
9. Wind changes the calculated relative airflow, blade angle of attack, and actual tail-rotor thrust.
10. Helicopter yaw rate changes the tail-hub relative airflow, blade angle of attack, and actual tail-rotor thrust.
11. Required zero-yaw tail-rotor thrust is shown separately from actual thrust.
12. The wind vector is shown graphically and is consistent with the entered speed and source direction.
13. The no-wind default state at 100% engine power and calibrated trim pitch remains stationary because the yaw moments are balanced.
14. Pause, resume, and reset work as specified.
15. The pitch control is first in `Flight Controls`, ranges from −6° to the current SPUU-52 altitude-dependent limit, defaults to the calibrated trim pitch, and changes geometric blade pitch while blade angle of attack remains airflow-dependent.
16. A visible LTE state appears when the configured critical angle is exceeded by enough sampled blade elements.
17. Tail-rotor thrust decreases drastically in the modeled post-stall region.
18. The live chart plots tail-rotor thrust vertically against blade angle of attack horizontally.
19. The chart marks the critical angle, post-stall region, and current operating point.
20. The application clearly states that its critical-angle LTE behavior is simplified and is not a full aircraft-specific LTE model.
21. The numerical and directional tests in Section 15 pass.
22. The interface is usable with mouse, touch, and keyboard at widths down to 320 CSS pixels.
23. At the no-wind 100% calibration state, displayed main-rotor lift is
    approximately 14,000 kg and the displayed power split totals 4,000 k.s.
24. Tail-rotor pitch can be operated with left/right arrow keys, including the Shift-modified 1° step, without interfering with typed numeric input.
25. Main-rotor and net-moment arrows visibly scale with their respective moment magnitudes while retaining correct CCW/CW direction.
26. Combined engine power can be operated with up/down arrow keys, including the Shift-modified 5% step, without interfering with typed numeric input.

27. MSA altitude and temperature visibly change air density and main-rotor lift, while maximum engine power remains flat-rated through 3,600 m and lapses above it.
28. Changing altitude automatically selects standard MSA temperature, while changing temperature leaves altitude unchanged.
29. The tail-rotor blade-element model and wind-force calculation use the same altitude-and-temperature-dependent air density.
30. Wind changes OGE lift capability according to the digitized Mi-8MTV-5-1
    Figure 1.2 curves, and the interface lists the front, left, right, and rear
    limiting-weight and equivalent-power changes for verification.

## 17. Future Extensions

Potential later versions may add:

- pedal commands required to hold heading;
- aircraft-specific LTE azimuth regions and unsteady vortex-interference models;
- main-rotor direction selection;
- counterclockwise main-rotor configurations;
- gusts and turbulence;
- selectable helicopter size or configuration;
- separate vertical-fin and fuselage wind moments;
- lateral helicopter motion and relative airflow;
- time-history charts for yaw rate, moments, and tail-rotor thrust;
- guided learning scenarios and quizzes;
- SI/imperial unit selection;
- import/export of simulation cases.

These extensions are not part of version 4 and must not complicate the single-file educational experience.

# Open-source CNC machining center

![Finished machine](images/01-machine.jpg)

<!-- DOPLNIT: fotka hotového stroje, ideálně při práci. Pokud máš video z chodu,
     dej pod fotku odkaz. Renders z Crea jsou v práci — ale fotka reálného
     stroje je cennější. -->

A three-axis CNC router I designed as my bachelor's thesis in 2022 and then built,
wired and commissioned over the following two years. Frame concept, FEA sizing,
component selection, procurement, assembly and GRBL setup are all my own work,
done in free time on a hobby budget.

The goal was not the cheapest possible router. It was to go through the entire
loop once — concept, calculation, drawings, procurement, build, control, and the
long tail of tuning nobody writes about — and end up with a machine that holds
tolerance.

## Specification

| | |
|---|---|
| Working envelope | 750 × 830 × 400 mm |
| Overall dimensions | 1710 × 1150 × 1200 mm |
| Frame | Aluminium extrusion 3030, Al6060 T5, T-nut assembly |
| Linear guides | HIWIN HGR20 rails, HGH20CA blocks (all axes), ZA preload |
| Drive | HIWIN ballscrews, 5 mm pitch — R1605 (X, Y), R1205 (Z) |
| Motors | NEMA 23 stepper, 1.4 Nm up to ~70 rpm |
| Resolution | 320 steps/mm at 1/8 microstepping |
| Max feed rate | 1000 mm/min (at 200 rpm, torque preserved) |
| Spindle | Makita RT0700C, 710 W, up to 30 000 rpm, manual speed control |
| Max cutting force | 1397 N (calculated) |
| Control | Arduino Mega (ATmega2560), TB6600 drivers, GRBL |
| Table | Hardwood plywood |
| Target materials | Wood, aluminium |

## Design notes

**Aluminium extrusion over a welded steel frame.** Steel is cheaper per metre, but
a welded frame distorts as it cools and the weight itself contributes to
deflection. Extrusion is lighter, stays square, and — the reason that mattered
most for a first machine — lets any element be swapped for a better one later
without cutting anything apart.

**Sizing the frame by simulation, not by feel.** The gantry load was taken as
400 N (~40 kg split across two rails) and the beam simulated in Creo Simulate.
Supported only at its ends, the profile deflected about 1 mm — far too much. Adding
a single vertical strut at mid-span cut that to 0.14 mm, roughly a factor of ten
for one extra profile. Simulating the profile together with the steel linear rail,
which carries load as a structural member rather than just riding on top, brought
it to 0.027 mm. The lesson worth taking from this: the cheapest stiffness on the
whole machine came from one strut in the right place.

**Where 3D printing belongs and where it doesn't.** Printed PET-G is fine for
motor mounts, endstop brackets and covers. It is not fine for anything holding
geometry under dynamic load — plastic is too elastic, and once the motors run,
the accelerating masses turn that compliance into position error. Those parts are
waterjet-cut from 3 mm aluminium plate instead. Printed parts also fail between
layers when loaded perpendicular to them, so print orientation was part of the
design, not an afterthought (PET-G, 0.2 mm layers, 30 % infill, Prusa i3 MK2.5S).

**Ballscrews over belts.** More expensive, but they give backlash under 0.05 mm
and a high enough lead that the required motor torque drops — 0.018 Nm to move
the Y axis, well inside what a NEMA 23 delivers.

**Modular Z head.** The spindle mount attaches with six bolts to an aluminium
plate, so the router can be swapped for a laser or a 3D printing extruder without
touching the rest of the axis.

**What I'd change.** The structure is overbuilt relative to the motors — it was
sized for masses well above the actual ones to leave room for later upgrades, and
the result is a machine whose speed is limited by the drives rather than by
stiffness. The Z-axis support deflects 0.115 mm at 100 N, the largest number on
the machine and the first thing I'd stiffen. Positioning accuracy was never
measured properly against a reference, which is the honest gap in this project.

## Repository contents

```
cad/          3D models — STEP and STL
drawings/     Manufacturing drawings
firmware/     GRBL configuration
docs/         Bill of materials, datasheet, calculations
images/       Build photos
```

<!-- DOPLNIT: smaž řádky, které nakonec nenahraješ. STL export sestavy stojí
     za to — GitHub ho renderuje přímo v prohlížeči. -->

## Thesis

Návrh konstrukce open-source CNC frézky (2022), Technical University of Liberec,
Faculty of Mechanical Engineering. Supervisor: Ing. Andrii Shynkarenko, Ph.D.

---

[← zpět na přehled projektů](../README.md)

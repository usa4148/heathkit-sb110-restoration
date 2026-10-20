---
title: "Heathkit SB-110 / SB-110A 6 m Transceiver — Restoration Plan"
subtitle: "Rev. 2 — checked against the original Heath SB-110A manual"
date: "October 2026"
geometry: margin=0.9in
fontsize: 10pt
colorlinks: true
toc: true
---

<!-- Build: pandoc sb110-restoration-plan.md -o sb110-restoration-plan.pdf --pdf-engine=xelatex -V mainfont="DejaVu Serif" -->

> **Safety (manual p. 88).** "Lethal voltages are present both above and below the chassis." The finals run at about +700 V DC (the HP-23A's HV pin is marked +820 V unloaded). Heath says to connect a lead from a good earth ground to the ground bolt on the rear of the chassis, and to all test equipment. Use well-insulated tools. Short the hot end of every supply filter capacitor to chassis before working inside (p. 110). Transmit only into a **50 Ω non-reactive dummy load rated for 100 W; Heath says do not use light bulbs** (p. 89). **Never operate without an 8 Ω speaker or headphones connected** (p. 88).

> **About the sources.** Rev. 2 is checked against **Heath manual 595-1145-01, *Assembly Manual, 6-Meter SSB Transceiver Model SB-110A*** (©1966, printed 4-17-70). Page numbers are the manual's **printed** page numbers. Items still marked **[family]** are SB-line practice the manual does not cover.

# 1. Source documents

| Document | Use |
|---|---|
| **Heath SB-110A Assembly Manual 595-1145-01** (archive.org K6KJN; ManualsLib #895692; Dan's scan) | Primary reference: parts lists (pp. 3–4, 18–21), preliminary checks and resistance chart (pp. 81–84), power supply connections (pp. 86–87), initial test (p. 88), alignment (pp. 89–94), special crystals (pp. 95–96), operation (pp. 105–109), troubleshooting (pp. 110–120), specifications (pp. 121–125), circuit description (pp. 127–146), voltage and resistance charts (Figs. 1-13, 1-14), replacement parts list (p. 151+). |
| SB-110 service bulletin **SB-110-1** (Nov 1969), Heath list (Mar 1998) | The only SB-110 bulletin on record. |
| Heath list SB-110/110A threads (1997–2012) | Model identification, field symptoms. |
| SB-100/101/102 and HW-101 bulletins; W5RKL SB-10x guide | **[family]** practice where the manual is silent. |

# 2. Transceiver at a glance

## 2.1 Specifications (manual pp. 121–125)

| Item | Value |
|---|---|
| Coverage | **49.5–54.0 MHz in 500 kHz segments; 50.0–52.0 MHz with the supplied crystals** |
| Sensitivity | **0.1 µV for 10 dB (S+N)/N** |
| Selectivity | 2.1 kHz at −6 dB, 5 kHz max at −60 dB |
| Image / IF rejection | 50 dB or better |
| Spurious | All below 0.1 µV equivalent, except 51.250 MHz (below 0.3 µV) |
| AGC | Audio varies < 12 dB for 50 dB input change (0.5–150 µV) |
| Audio | 1 W; 8 Ω speaker; 600 Ω+ headphones |
| Input power | 180 W PEP SSB; 150 W CW |
| Output power | **100 W PEP SSB; 90 W CW** (into 50 Ω non-reactive) |
| Carrier / unwanted sideband suppression | 55 dB / 55 dB (at 1000 Hz and above) |
| Distortion products | 30 dB below rated PEP |
| ALC | 10 dB or better at 30 µA of final grid current |
| CW sidetone | About 800 Hz, internally switched to the speaker |
| Keying | Grid-block; VOX operated from the keyed tone |
| Stability | < 100 Hz/hr after 20 min warm-up; < 100 Hz for ±10% supply change |
| Dial accuracy | **Within 400 Hz on all segments after calibrating at the nearest 100 kHz point**; visual within 200 Hz; backlash ≤ 50 Hz |
| IFs | 8.395–8.895 MHz (receiver 1st IF / transmitter 2nd IF); 3.395 MHz (receiver 2nd IF / transmitter 1st IF) |
| Size / weight | 14-7/8 × 6-5/8 × 13-3/8 in.; 17 lb |

*Rev. 1 quoted "0.1 µV for 15 dB" and "noise figure ≤ 3 dB" from secondary sources. Neither appears in the manual.*

## 2.2 Power requirements and the supply (pp. 86–87, 109, 123)

| Rail | Requirement | 11-pin power plug CC |
|---|---|---|
| HV | **+700 V DC @ 250 mA**, 1% max ripple | Pin 4 (HP-23A marked +820 V; HP-13A +800 V) |
| LV B+ | **+250 V DC @ 100 mA**, 0.05% max ripple | Pin 3 |
| Bias | **−115 V DC @ 10 mA**, 0.5% max ripple | Pin 1 (supply delivers about −130 V) |
| Filaments | **12.6 V AC/DC @ 4.355 A** | Pins 6 (hot), 2 (ground) |
| Ground | — | Pin 7 (B−, C+) |
| Power switch | Function switch AC loop | Pins 9–10 |
| Linear amp relay | N.O. contacts | Pins 5 and 11 |

> **Answer to the Rev. 1 open question.** The manual says the HP-23A's low-voltage circuit must be wired with its **alternate connection for the +250 V output** (p. 87; the same caution appears for the HP-13A on p. 86). **Do not use the 300 V setting the HW-101 and SB-102 need.** With the SB-110A's power cable, the HP-23A's own BIAS control is inoperative; bias is set by the transceiver's **BIAS ADJ** (Section K). With the **HP-13A** (mobile), turn the supply's Bias control **fully clockwise** (maximum bias) first (p. 86), then set 50 mA with the transceiver (p. 109).

**Mobile warnings (p. 109).** Vehicle charging voltage must not exceed **14.5 V**. LV B+ from the supply must not exceed **290 V**. Exceeding either shortens component life and causes inoperative VOX and instability. Troubleshooting items 15E and 35E both point here.

There is **no fuse in the transceiver.** Fusing is in the supply (HP-23A) or the HP-13A's in-line fuse holder (Fig. 1-3).

## 2.3 Tube and semiconductor complement (pp. 124–125, circuit description)

| V | Tube | Function |
|----|--------|------------------------------------------------|
| V1 | 6DS4 nuvistor | Receiver RF amplifier |
| V2 | 6DS4 nuvistor | Receiver 1st mixer |
| V3 | 6EA8 | A: receiver 2nd mixer · B: crystal oscillator (Y6, AUX T / XTAL modes) |
| V4 | 6AZ8 | A: 1st IF amp (receive **and** transmit) · B: VOX amplifier |
| V5 | 6AZ8 **(painted tip, 411-218; must go in V5)** | A: 2nd IF amp · B: VOX relay amplifier |
| V6 | 6EB8 | A: 2nd audio preamp · B: audio output |
| V7 | 6EA8 | A: heterodyne crystal oscillator · B: heterodyne oscillator amplifier |
| V8 | 12AT7 | A: USB carrier generator (Y7) · B: LSB carrier generator (Y8) |
| V9 | 6AZ8 | A: CW carrier generator (Y9) · B: transmitter isolation amplifier |
| V10 | 6EA8 | A: microphone amp / 800 Hz CW tone oscillator · B: cathode follower |
| V11 | 6EA8 | A: 100 kHz crystal calibrator (Y10) · B: transmitter 1st mixer |
| V12 | 6CB6 | Transmitter 2nd mixer |
| V13 | 12BY7 | Driver |
| V14, V15 | **6146** | Finals (parallel, class AB1) |
| V16 | 0A2 | +150 V regulator (must glow violet/orange at turn-on) |
| V17 | **6BZ6** | LMO (inside the LMO; replace only with the same brand) |
| Q1 | 2N2712 | Receiver 1st audio preamplifier |

**Diodes (p. 125).**

| Qty | Type (Heath p/n) | Use |
|---|---|---|
| 6 | 1N2079 silicon rectifier (57-29, 750 mA 100 PIV) | VOX (SR52), anti-trip (SR50/SR51), ALC (SR150/SR151), DC blocking |
| 3 | GE S187 silicon (56-28) | Noise limiter (SD50/SD51), AGC (SD52) |
| 10 | 1N191 germanium (56-26) | Balanced modulator (GD220–GD223), product detector (GD200–GD203), AGC (GD50), RF sampling (GD140) |
| 1 | 1N4166A 15 V zener (56-25) | Cathode reference for relay amp V5B |

## 2.4 Frequency scheme (p. 127, Figs. 2-11, 2-18)

- **LMO** tunes 5.0–5.5 MHz. It is shifted 2.8 kHz between USB and LSB by an internal shifter, so the dial reads the suppressed-carrier frequency in both modes.
- **Heterodyne crystals** (Y1–Y4, chassis, 2 × 2 under a retaining plate):

| Segment | Crystal | Position |
|---|---|---|
| 50.0 | 41.605 MHz | Y1 |
| 50.5 | 42.105 MHz | Y2 |
| 51.0 | 42.605 MHz | Y3 |
| 51.5 | 43.105 MHz | Y4 |

- **Carrier crystals:** **Y7 3393.6 kHz = USB**, **Y8 3396.4 kHz = LSB**, **Y9 3394.4 kHz = CW**. The CW carrier sits 800 Hz above the USB carrier, which allows cross-mode USB/CW contacts.
- **Y10** is the 100 kHz calibrator. **Y6** (receiver RF board, "XTAL FREQ ADJ" trimmer) is the optional fixed-frequency crystal for AUX T/XTAL operation.
- The heterodyne amplifier V7B feeds a stock **half-wave harmonic filter** (C77 22 pF / C78 150 pF, labelled "Harmonic filter" in Fig. 3-8). This is factory, not a mod.

## 2.5 SB-110 vs. SB-110A

The manual confirms the SB-110A layout:

- **V7** (heterodyne oscillator) is on the **chassis** with its own shield (p. 88).
- **Y1–Y4** sit in **sockets on the chassis under a crystal retaining plate** with a knurled nut (p. 85).
- The **Carrier Generator board 85-152** holds V6, V8, V9 and V10 (Fig. 1-5).

On the earlier **SB-110**, V7 was on the carrier generator board and the four crystals sat in a single row (Heath list, 2003). The SB-110 manual and its numbering may differ from what follows; this plan follows the SB-110A.

# 3. What fails, ranked

## 3.1 Service bulletin SB-110-1 (Nov 3, 1969)

| Item | Detail |
|---|---|
| Symptom (SB-110) | Audio oscillation on CW with sidetone fully up; hand-capacitance effects; audio output tube overheats; a 20 µF electrolytic seems intermittent. |
| Cause | DC from the VOX amp plate reaches the audio output grid through a **3.3 MΩ resistor (R49)**, the sidetone control and a second 3.3 MΩ, putting about +3 V on the grid. |
| Fix | Replace R49 with a **500 pF ceramic disc** (21-13). |
| **SB-110A status (manual-verified)** | **Already incorporated.** In the SB-110A the sidetone feed from the V4B plate is **capacitor-coupled through C48, 500 pF** (Fig. 2-2), and the SB-110A manual uses different part numbers (there is no R49/C658 in this circuit). **An SB-110A needs no change.** On an early **SB-110**, check for the bulletin fix. |

A **hot 6EB8 (V6) or audio oscillation** on an SB-110A therefore points elsewhere. The troubleshooting chart (item 9, p. 112) lists R68 (22 kΩ 2 W) open or wrong, **C67 shorted or installed backwards**, V6, Q1, and relay DE contacts 2–3. Also check that the tube shields are fitted: the manual warns the IF and audio sections **may oscillate without tube shields** (p. 88).

## 3.2 Capacitors

**Electrolytics.** The kit has only **five**, all on circuit boards (pp. 4, 151). The chassis list has none.

| Ref (from schematic figures) | Value | Where / role | Replace with |
|---|---|---|---|
| C68 | **20 µF** (25-135) | Audio output B+ decoupling, with R68 22 kΩ 2 W | 22 µF **≥ 350 V** |
| C63 | **100 µF** (25-117) | V6A cathode bypass (with R62 5.6 kΩ) | 100 µF ≥ 25 V |
| C67 | 10 µF | V6B (audio output) cathode bypass (R67 100 Ω) | 10 µF ≥ 50 V; **check polarity** (chart 9D) |
| C102 | 10 µF | V10A mic amp cathode bypass (R102 1 kΩ) | 10 µF ≥ 50 V |
| C210 | 10 µF | Q1 emitter bypass (R215 5.6 kΩ) | 10 µF ≥ 25 V |

The manual's parts lists give **no voltage ratings**, and they couldn't be read on the scanned schematic. The ratings above are chosen by circuit position; confirm on the board before ordering. *Rev. 1 also told you to replace a "bias-filter electrolytic on the −115 V line." There isn't one in the transceiver; bias filtering is in the supply.*

**Other capacitors worth testing:**

| Part | Why |
|---|---|
| .1 µF and **.2 µF resin** caps (27-47, 27-34): e.g. C59 VOX delay, C230/C157/C158 AGC and ALC time constants, C106/C108/C109 audio | Leakage or drift changes VOX hold, AGC decay and ALC. Chart items 37 and 40 name C155–C158. |
| 1 pF and 2.2 pF **phenolic** caps (28-2, 28-1) | Same failure mode as in the SB-301 (open, or drifted). |
| C47, C66 (anti-trip) | Chart item 39D. |
| C80–C86, C90–C92 (carrier oscillators) | Chart items 28–29: wrong value → no carrier. |
| C70/C73/C77/C78 (heterodyne oscillator) | Chart item 32F. |
| .005 µF 1.4 kV discs (21-72) | Line/HV bypass; replace with modern HV-rated parts. |

## 3.3 Resistors

Survey all resistors with one lead lifted; replace any more than 10% out of tolerance. Manual-named suspects:

| Ref | Value | Symptom if wrong (chart item) |
|---|---|---|
| R160 | (+150 V regulator feed) | No, high or low regulated B+ (5–7) |
| **R68** | 22 kΩ 2 W | No audio (9C) |
| R42, R43, R44, R52, R53, R54, R230, R231 | S-meter bridge | S-meter backwards, inoperative or won't zero (17F) |
| R40, R41, R42, R43, R230 | 1st IF | No first-IF output (24F) |
| **R125, R127** | 10 k / 15 kΩ (bias divider with BIAS ADJ) | Bias won't shift to operating level (19F) |
| R95–R98, R223, R224 | Isolation amp | No output from V9B (25C) |
| R81–R83 / R91, R92 | Carrier oscillators | No carrier injection (28C, 29E) |
| R190–R192 | LMO shift | LMO won't shift with mode (31C) |
| R51, R232, R233 | AGC (5.6 MΩ decay) | Slow recovery after transmit (37B) |
| R56, R57, R65 | Anti-trip | ATG has no effect (39C) |
| **R132** 6800 Ω 1 W, **R151** 100 Ω 1 W | Driver and final screen feeds at AU | No driver or final output (21C, 20C) |
| R140 10 kΩ 2 W; 33 kΩ 2 W (RF board); 22 kΩ 2 W; 2000 Ω 10 W | Power resistors | Heat-stressed; check value and discoloration |

## 3.4 Tubes, by risk

1. **6EB8 (V6):** hot running; audio faults (§3.1).
2. **6146 pair (V14/V15):**
   - The manual specifies the **6146** (411-75) and **does not mention the 6146B**.
   - After replacing the finals, **repeat the neutralizing procedure** (p. 85).
   - **[family]** HW-101 bulletins -18/-49 report RF-choke heating and high-band neutralizing trouble with some 6146Bs. If you fit Bs, neutralize carefully and watch RFC6.
3. **6DS4 nuvistors (V1, V2):** scarce. Install with the heat sinks, wide locating tab into the wide socket opening (p. 85).
4. **6AZ8 (V4, V5, V9):**
   - **V5 must be the painted-tip 6AZ8** (411-218) (p. 85).
   - Replacing V4 or V5 means rechecking S-meter zero and T2/T3 (p. 85).
   - If the T5 null or 50 mA reading can't be obtained, **swap V9 and V4** (p. 92).
5. **6BZ6 LMO tube (V17):** "replace with tube from the same manufacturer" (pp. 110, 117).
6. **0A2 (V16):** must glow at turn-on; if not, switch off (p. 88).

**Do not pull tubes or pilot lamps with power applied.** With a 12 V supply the filaments are series-parallel, and removing one can destroy others (p. 110).

## 3.5 LMO

- **Manual:** "At no time should the LMO be opened or the warranty will be voided" (p. 110). If the LMO is proven faulty after the chart 30 checks, Heath said to return the complete unit for replacement (p. 117).
- **[family], restorer practice:** for a jumpy dial or stiff tuning, the TRW-style service applies (rotor-to-frame braid; regrease the worm and anti-backlash gear; open one side only; never rotate the capacitor shaft with the stops loose). Do this only if needed, and expect to recalibrate.
- **Shift problems:** LMO frequency not shifting with mode → R190/R191/R192, MODE wafer MS1R, 30-lug strip segments (chart 31).

## 3.6 Relays: the manual differs from family practice

> **Manual (p. 110):** clean relay contacts **with a burnishing tool only**. "**DO NOT TRY TO USE PAPER, FINGER NAIL BOARDS OR LIQUID CONTACT CLEANERS.**" Compressed air often removes foreign matter.

This overrides the paper-strip method used on the SB-10x/HW-101. Relay-related chart items:

- 8, 18 (DE contacts 16–18), 9H (2–3), 19B (1–2), 24C (4–5), 40C (4–5).
- 20D (antenna relay contacts 1–2).
- 42 (a short between DE 17–18 makes the plate meter read backwards).

## 3.7 Mechanical and grounding

- **Instability** (receive item 15, transmit item 36): circuit-board mounting screws loose or **lockwashers missing between board and chassis** (lockwashers go against the foil side; p. 110); preselector or driver tuning-cap hardware loose; neutralization off; supply voltage too high; defective feedthroughs AP–AU.
- Switch wafers: many chart items are reversed leads at MS1R, MS2F, FS1R and BS1R–BS3R. Photograph before any rework.
- **Dial drive** (100-450 assembly): spiral follower, zero-set pulley, drive-shaft bushing. Check that the nylon spiral follower is engaged before calibrating (p. 94).
- Preset positions for every internal control are on p. 82. Use them if a previous owner has "tweaked" the rig.

# 4. Restoration plan

## 4.1 Phase 0: Assess cold

- Identify SB-110 vs. SB-110A (§2.5) and note the blue/white ID label (production series, p. 98).
- Photograph everything. Note mods and non-stock tubes. **Check that V5 is the painted-tip 6AZ8.**
- Pull and label tubes (nuvistors with their heat sinks). Test them.
- Check heterodyne crystals Y1–Y4 against §2.4, and any Y6 crystal.
- **Run the manual's resistance checks (pp. 82–84)** with both 6146s removed, at the 11-pin plug CC, using the switch and relay states in the chart. Key readings, ±20%:

| Pin | Condition | Expected |
|---|---|---|
| 1 (bias) | OFF/USB, relay NE | 32 kΩ (12–34 kΩ across switch states) |
| 3 (LV) | Relay NE / E | 65 kΩ / 18 kΩ |
| 4 (HV) | — | ∞ (≈ 6 Ω with a 6146 anode lead shorted to chassis) |
| 6 (FIL) | Pilot lamp socket out / in | ~20 Ω / ~10 Ω (meter dependent) |
| 2, 7 | — | 0 |
| 5, 8, 11 | — | ∞ |
| 9–10 | OFF / PTT | ∞ / 0 |

- Fig. 1-14 (fold-out) gives the full tube-socket resistance chart.

## 4.2 Phase 1: Supply

- Recap and test the HP-23A/HP-23 or HP-13A. **[family]** HP-23: C1–C4 → 150 µF 500 V; C5 → 47 µF 450 V; bias C6/C7 → 47 µF 160 V+; bleeders 100 kΩ 2 W; diodes 1N4007; grounded cord.
- **Wire the low-voltage section for +250 V** (p. 87).
- Bring it up on a variac with resistive loads.
- Make up the 8-conductor power cable exactly per Fig. 1-4 (HP-23A) or Fig. 1-3 (HP-13A).

## 4.3 Phase 2: Clean

- Vacuum and brush; use cleaner on swabs.
- DeoxIT the rotary switches and pots (not the relays; §3.6).
- Keep solvents off the dial and meter plastics and the panel lettering.

## 4.4 Phase 3: Recap and resistor survey

1. Replace the five electrolytics (§3.2), observing polarity.
2. Test or replace the resin caps in the VOX, AGC, ALC and audio circuits; replace the phenolic caps.
3. Resistor survey (§3.3).
4. Burnish relay contacts if dirty (§3.6).
5. Check every board's mounting screws and lockwashers.

## 4.5 Phase 4: Initial test (p. 88)

1. Set the controls per p. 81 (FUNCTION OFF, MODE USB, OSC MODE LMO, MIC/CW fully CCW, METER PLATE, etc.).
2. Connect the supply, an 8 Ω speaker and an earth ground.
3. FUNCTION → PTT: the pilot lamps light at once and the tubes glow in a few seconds. **V16 (0A2) must glow violet/orange.** Switch off immediately if a relay pulls in or anything overheats.
4. With an 11 MΩ VTVM, check feedthrough **AT ≈ −125 V DC** and **AU ≈ +250 V DC** (Fig. 1-6).
5. Install all tube shields (p. 88; V16 has none).
6. Compare with the **voltage chart, Fig. 1-13** (11 MΩ VTVM, ±10–20%).

## 4.6 Phase 5: Alignment (manual pp. 89–94)

Equipment: an **11 MΩ VTVM**, a **50 Ω non-reactive 100 W dummy load**, and a receiver that can hear **WWV** (2.5/5/10/15 MHz) or a broadcast station on a multiple of 100 kHz. Lay the chassis on its right side. Put a tape flag on the alignment tool. Fit the **47 Ω load plug** in ANT RF OUT for the receiver steps. **Do not transmit until told to** (p. 89).

**Receiver: heterodyne oscillator (Section G).**

1. VTVM negative lead to **TP** (the free lead of the 100 kΩ resistor in Section H); range for −1.5 to −3 V. FUNCTION PTT; warm up 1–2 min.
2. Band 50.0: peak **L6**, then turn its slug ¼ turn CCW. Peak **L10** (about **−2 V**).
3. Repeat for 50.5 (**L7** then ¼ CCW; **L11**), 51.0 (**L8**; **L12**) and 51.5 (**L9**; **L13**).
4. The −2 V reading varies slightly with PRESELECTOR. Unusually high or low readings mean trouble (see chart 32).

**Receiver: IF and RF (Sections G, H).**

1. Band 50.0; VTVM on AC across the speaker. Peak **T3**, then **T2**. Where there are two slug peaks, **use the one nearest the circuit board** (p. 90).
2. Temporarily jumper **4–5** on the foil side of the RF board (85-114-1). This removes B+ from the RF stage for the L2 step.
3. FUNCTION CAL. Set the dial to 50.10 (BAND 50.0, upper dial at 1, circular dial at 0). Rock the dial ±20 kHz: you'll find two signals about 10 kHz apart. Set the dial midway and adjust **CAL ADJ** (Section M) until a signal is heard there.
4. PRESELECTOR at 10 o'clock: peak **L4**, **L3**, **L1**.
5. **L2 (RF neutralizing coil):** adjust for a **minimum** (null) of signal leak-through. Re-peak L4, L3, L1.
6. FUNCTION OFF. Tape over L2's hole. Remove the jumper and install the **33 kΩ 2 W** resistor on the RF board.
7. FUNCTION CAL: re-peak T3, T2, L4, L3, L1.
8. **Do not readjust L2 later.** It can only be set with B+ removed from the RF stage (p. 90).

**S-meter (p. 90).** FUNCTION PTT.

1. METER PLATE: adjust **S-METER "0" ADJ** (Section M) for zero.
2. METER ALC: adjust **ALC METER ADJ** (Section G) for zero.
3. Repeat until neither position deflects.

**Transmitter alignment (pp. 91–93).** In the factory sequence the driver and final screen feeds (the **6800 Ω 1 W** and **100 Ω 1 W** resistors at AU) are left unsoldered until neutralizing is done. **To re-neutralize a built unit, temporarily lift those leads exactly as described.**

1. **Driver and mixer coils:**
   - Tack the 6800 Ω lead from AL8 to AU (temporary).
   - VTVM at **AL2**, ≥ −150 V range. PTT: about **−125 V**. TUNE: both relays energize and the reading drops to about 0 V.
   - DRIVER at 10 o'clock; MIC/CW fully CW. Peak **L14, L15, L16**; repeat until no further increase.
   - Peak **T5** (Section J; preset, ≤ ½ turn).
2. **Bias preset:**
   - Move the VTVM to **AT**, MODE LSB, PTT: about **−125 V**. TUNE (BIAS ADJ fully CCW): about **−45 V**.
   - With MIC/CW fully CW, peak L16, L15, L14 again: about **−60 to −70 V**.
   - **OSC MODE → AUX T: the reading must drop to about −45 V.** If it doesn't, L14–L16 are tuned to the heterodyne oscillator output instead of the mixer product. Turn all three slugs at least **5 full turns CCW**, return to LMO, and repeat from the start of this group (p. 91).
3. **Final neutralizing (cold):**
   - Remove the 47 Ω load. METER REL PWR; FINAL LOAD fully CW; REL PWR ADJ fully CW.
   - Peak **FINAL** tune (about half scale).
   - Adjust **FINAL NEUT** (Section A, underside; use the trimmer tool made per Fig. 1-6) for a **minimum** meter reading.
   - MIC/CW fully CCW. Adjust **BIAS ADJ** (Section K) for **−50 V** on the VTVM.
4. **Driver neutralizing:**
   - MODE LSB, OFF; disconnect the VTVM.
   - Remove the 6800 Ω lead from AU. Solder the 100 Ω 1 W lead from AF3 to AU **permanently**.
   - PTT, METER PLATE, TUNE: the meter should read **50 mA static plate current**; adjust BIAS ADJ if not.
   - METER REL PWR, MIC/CW fully CW, FINAL LOAD at 50 Ω. Peak FINAL (about 1–2 S-units).
   - Adjust **DRIVER NEUT** (Section L) for a **minimum** meter indication.
   - MIC/CW CCW, MODE LSB, OFF. **Reconnect the 6800 Ω to AU permanently.**
5. **Carrier isolation null (T5):**
   - Connect the 50 Ω, 100 W dummy load to RF OUT.
   - PTT, MIC/CW fully CCW, TUNE. Adjust **T5** for a **null** (≤ ½ turn), then turn the slug **clockwise to the second null and leave it there**.
   - METER PLATE should read **50 mA**. If you can't get the null or 50 mA, **swap V9 and V4**. A tube change means rechecking T2/T3 and the S-meter zero.
6. **Tune-up into the load:**
   - REL PWR METER ADJ mid-range. MIC/CW at 11 o'clock: plate current rises slightly.
   - Peak with **DRIVER** for maximum plate current, keeping it **< 250 mA** with MIC/CW. Dip with **FINAL**.
   - Advance MIC/CW while re-peaking DRIVER and re-dipping until the plate current reads **250 mA**.
   - With a true 50 Ω load, LOADING can stay at its preset. Otherwise: METER REL PWR, set REL PWR ADJ for half scale, then adjust FINAL tune and load for maximum, **never exceeding 250 mA**.
   - MIC/CW fully CCW; MODE USB; REL PWR METER ADJ fully CW.
7. **Carrier null (p. 93):**
   - Ground MIC connector NF lug 2 to energize the relays. METER REL PWR: about 1–2 S-units.
   - Alternate **CARRIER NULL ADJ** and **CARRIER BAL ADJ** (Section J) to a null, until the meter reads 0.
   - For better suppression, listen on an external receiver at **50.1 or 8.5 MHz** with its BFO on. Null in USB, then switch to LSB and compromise with CARRIER NULL ADJ so the carrier is equal on both sidebands.
   - If CARRIER BAL ADJ ends at **minimum capacity**, move it from **position A to B** on the carrier generator board.
   - If CARRIER NULL ADJ ends at an **extreme**, **interchange R220 and R222**.
   - Afterwards recheck the **50 mA** static plate current. Remove the NF lug 2 jumper.
8. **Crystal calibrator (pp. 93–94):**
   - Wrap the external receiver's antenna wire one or two turns around the **orange shielded cable at point 5 on the receiver RF board**.
   - Transceiver AF GAIN fully CCW, FUNCTION CAL. Tune the external receiver to **WWV** (or a broadcast station on a multiple of 100 kHz).
   - Adjust **CAL ADJ** (Section M) for zero beat, best during WWV's unmodulated periods. Use S-meter pulsation if the receiver has one.
   - Toggle FUNCTION VOX ↔ CAL: the S-meter should stay steady.
   - Precision matters: the 6 m dial uses the **500th harmonic**, so **a 20 Hz error at 100 kHz becomes a 10 kHz dial error at 50 MHz** (p. 94).
   - Spurious 100 kHz signals can appear. Find the real one by its strength, or by the heterodyne-crystal "chirp" when you switch BAND away and back.
9. **LMO shifter (p. 94):**
   - Dial at 50.10, CAL, **LSB**: zero-beat the calibrator and peak PRESELECTOR.
   - Switch to **USB without touching the dial**. Adjust the **LMO FREQUENCY SHIFTER** (top of the LMO) for exact zero beat. Recheck LSB and repeat as needed.
10. **Dial calibration (p. 94):**
    - Zero-beat at 50.10 and center the zero-set line in the window.
    - Remove the tuning knob. Hold the LMO drive shaft with a screwdriver through the escutcheon hole. Loosen the circular-dial setscrew, set **0** under the zero-set line and retighten.
    - Confirm the nylon spiral follower is engaged. Refit the knob.

## 4.7 Phase 6: Operating setup (pp. 105–108)

- **Every time you tune up** (steps 1–13, p. 106):
  - TUNE should read **50 mA**.
  - MIC/CW to 100–150 mA, dip FINAL; peak DRIVER (≤ 250 mA); advance to **250 mA** loaded; peak REL PWR with LOAD and FINAL.
  - Set MIC/CW **just below saturation**. Going beyond saturation causes a time lag on transmit-to-receive changeover.
  - Re-tune DRIVER, FINAL and LOAD after any big frequency change.
- **SSB:** METER ALC; MIC/CW so voice peaks reach about **S3**, never beyond the top of the ALC (S8) region.
- **VOX / ATG / DELAY** are on the front of the final shield, under the cover. Set VOX just high enough, ATG just high enough to stop the speaker tripping the relays, and DELAY to hold between words.
- **CW:** the transmitted signal is **800 Hz above the dial reading**. Set VOX so the relays close on key-down, DELAY to hold between characters, and SIDETONE LEVEL to taste.
- Most 6 m SSB was USB when the manual was written (p. 105).
- The manual warns not to run voice on 50.0–50.1 MHz, reflecting band rules at the time (p. 106).

# 5. Troubleshooting quick reference (chart pp. 111–120)

| Symptom | First checks (chart item) |
|---|---|
| No regulated +150 V | V16 0A2, R160, V16 socket wiring (5–7) |
| No audio | R68, C67, V6, Q1, T4, relay DE 2–3 (9) |
| Hum only, no signal or noise | RFC1, product detector GD200–203, carrier injection, T3, V5A, noise limiter SD50/51 (12) |
| Noise but no signal | T2, filter Y5, LMO injection at V3A, V4A, V3A, T1, heterodyne injection at V2, V1/V2 6DS4s, RL2 contacts (13) |
| Receiver oscillates or birdies | **L2 misaligned**, loose preselector/board hardware, missing lockwashers, bad antenna SWR, supply too high (15) |
| Sidebands reversed | **Y7/Y8 swapped**, Y9 swapped (16) |
| S-meter backwards or won't zero | Meter leads, DE 14–15, S/ALC zero, R42–R44, R52–R54, R230/231, V4A/V5A (17) |
| Bias won't shift on transmit | DE 1–2, R125, R127, BIAS ADJ (19) |
| No final output | HV missing, RFC6, R151, RL2/AE, bias, V14/V15 (20) |
| No driver output | RFC4, R132, bias, L14–L16, V13 (21) |
| No output in USB/LSB only | Balanced modulator GD220–223, RFC2/3, CARRIER BAL/NULL, MIC cabling, V10 (26) |
| No output in TUNE/CW only | Y9, C90–C92, R91/R92, V9A (28) |
| LMO won't shift with mode | R190–R192, MS1R, 30-lug strip (31) |
| No heterodyne injection | Y1–Y4, oscillator board orientation, BS1R–BS3R, C70/C73/C77/C78, V7 (32) |
| VOX won't trip / always tripped | V4B, SR52, zener, ATG; SR50/51, B+ too high (34, 35) |
| Transmitter unstable | Neutralization, driver-cap hardware, board lockwashers, feedthroughs AP–AU, L14–L16 (36) |
| Slow receive recovery | MIC/CW too high; R51, R232, R233; RF GAIN/AGC wiring (37) |
| ALC ineffective | SR150/151, C155–C158, DE 4–5, MS2F, neutralization, L16 (40) |
| Plate meter backwards, ALC pinned, audio oscillation | **Short between relay DE contacts 17–18** (42) |

# 6. Special crystals (pp. 95–96)

- **Extra 500 kHz segments:**

| Segment | Crystal |
|---|---|
| 49.5–50.0 MHz (MARS) | 41.105 MHz |
| 52.0–52.5 | 43.605 MHz |
| 52.5–53.0 | 44.105 MHz |
| 53.0–53.5 | 44.605 MHz |
| 53.5–54.0 | 45.105 MHz |

  After changing a crystal, realign its heterodyne oscillator and amplifier coils.
- **Heterodyne crystal spec:** 3rd overtone, ±0.003%, HC-6/U, 0.050 in. pins on 0.486 in. spacing, CL 23.2 pF, C0 ≤ 5 pF, Rs ≤ 30 Ω, 10 mW drive.
- **Fixed-frequency Y6 (AUX T: transmit on Y6, receive on the LMO; XTAL: both on Y6):** fundamental, ±0.01%, HC-6/U, CL 15 pF, C0 ≤ 7 pF, Rs ≤ 25 Ω, 2 mW.
  - USB: f = (f_MARS − f_het) − 3.3936 MHz. LSB: f = (f_MARS − f_het) − 3.3964 MHz.
  - Example for 49.980 MHz on the 41.605 crystal: 4.9814 MHz (USB), 4.9786 MHz (LSB).
  - Trim with XTAL FREQ ADJ. Below 50.0 MHz, Y6 operation is limited to about 25 kHz by the T1/T6 couplers; beyond that, use the 41.105 MHz heterodyne crystal.

# 7. Tips and tricks

- Spares: 6DS4 ×2 (hardest to find), a 6146 pair, 6EB8, 6EA8, 6AZ8 (plus a painted-tip one for V5), 12BY7, 6BZ6 of the original LMO brand, 0A2, #47 ×2, #53 ×1.
- Never pull tubes or lamps hot (§3.4).
- Keep the internal controls' preset positions (p. 82) on file.
- Mobile antennas: keep SWR low. Loading is more critical on 6 m mobile antennas (p. 109).

# 8. Maintenance schedule

| Interval | Task |
|---|---|
| Each session | 20–30 min warm-up; calibrator zero-set at the nearest 100 kHz point. |
| 6 months | Exercise switches and pots; S-meter and ALC zero (p. 90). |
| Yearly | Static plate current (50 mA); carrier null; receive check on the calibrator; inspect relays (burnish only if needed). |
| 2–3 years | Neutralization check (cold method, §4.6); board screws and lockwashers; calibrator vs. WWV. |
| 5 years | Tube test (nuvistors, finals, 6EB8 first); supply voltages (+250 / +700 / −115). |
| ~15–20 years | Re-check the five electrolytics and the supply capacitors. |

# 9. Parts sources

- Mouser / Digi-Key: electrolytics, film caps, resistors.
- HP-23 rebuild kits.
- Nuvistors: specialty tube dealers; test before buying.
- Heathkit-Radios and heathkit (groups.io): SB-110 parts units, crystals, dial parts.

# 10. Sources

- Heath, *Assembly Manual, 6-Meter SSB Transceiver Model SB-110A*, 595-1145-01 (1966; printed 4-17-70).
- Heath list (puck.nether.net): SB-110 service bulletins (Mar 1998); "SB110 Question to Owners" (Jun 2003); "SB-110 VFO's" (Apr 2012); "SB-110A Question – 6146Bs" (Feb 2003); SB-110A oscillation (Oct 1997); low drive (Feb 1999).
- **[family]** HW-101/SB-10x service bulletins; W5RKL SB-10x guide; Latta HP-23 restoration.

# 11. Rev. 2 change log (manual review)

| Item | Rev. 1 | Rev. 2 (per manual) |
|---|---|---|
| **HP-23 B+** | Open question: 250 vs. 300 V | **+250 V**: wire the HP-23A low-voltage section for +250 V (p. 87); HP-23A bias control inoperative, BIAS ADJ in the transceiver |
| Sensitivity / NF | 0.1 µV for 15 dB; NF ≤ 3 dB | **0.1 µV for 10 dB (S+N)/N**; no NF spec (p. 121) |
| Heterodyne crystals | 42.105, 42.605, 43.105 and one more MHz | **41.605 / 42.105 / 42.605 / 43.105 MHz** = Y1–Y4 for 50.0–51.5 (Fig. 2-11) |
| Carrier crystals | Listed without sideband | **Y7 3393.6 = USB, Y8 3396.4 = LSB, Y9 3394.4 = CW** |
| Tube table | Partial, "verify" | Full V1–V17 + Q1 with functions; LMO tube is a **6BZ6 (V17)**; V5 must be the painted-tip 6AZ8 |
| SB-110-1 | "Check whether present; replace C658" | **Built into the SB-110A** (C48 500 pF coupling); bulletin applies to early SB-110s only |
| Electrolytics | "Several 10, 20, 100 µF + bias filter" | **Exactly five** (C63 100, C68 20, C67/C102/C210 10 µF); **no bias-filter electrolytic** in the transceiver; ratings not printed in the manual |
| Pilot lamps / fuse | #47 and #53 | #47 ×2, #53 ×1; **no fuse in the transceiver** (in the supply) |
| Relay cleaning | Paper strip **[family]** | **Burnishing tool only; no paper or liquid cleaners** (p. 110) |
| Bias | "About 50 mA idle **[family]**" | **50 mA static plate current** in TUNE (pp. 92, 106, 136); −50 V at the VTVM during alignment |
| Neutralizing | SB-100-2 alternate method **[family]** | Manual's cold method: finals and driver neutralized with their screen feeds (100 Ω / 6800 Ω at AU) lifted; repeat after any 6146 change |
| Alignment | Pending | Full sequence with TP ≈ −2 V, L1–L16, T2/T3/T5, **L2 null with RF B+ removed**, AUX T −45 V check, carrier BAL A/B and R220/R222 swap |
| Calibrator on 6 m | "Use counter or HF zero beat" | Zero-beat against WWV on an external receiver; 20 Hz error = 10 kHz on the dial |
| LMO shifter | "Zero beat USB, adjust in LSB" | **Zero beat in LSB, adjust the shifter in USB** (p. 94) |
| Heterodyne "harmonic filtering" | Possible owner mod | **Stock** half-wave harmonic filter (C77/C78) |
| Max plate current | — | **250 mA** tune-up limit; MIC/CW just below saturation |
| Mobile | — | HP-13A bias fully CW; alternator ≤ 14.5 V; LV B+ ≤ 290 V |
| 6146B | List question | Manual specifies 6146 only; no 6146B guidance |

**Not readable or not in the manual:** electrolytic voltage ratings (not in the parts lists, and illegible on the scanned schematic); which socket takes the #53 lamp vs. the #47s; the value of R160.

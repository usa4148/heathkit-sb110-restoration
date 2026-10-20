---
title: "Heathkit SB-110 / SB-110A 6 m Transceiver — Restoration Plan"
subtitle: "Rev. 1 — Heath service bulletin, partial manual OCR, Heath list and SB-family field sources (manual cross-check pending)"
date: "October 2026"
geometry: margin=0.9in
fontsize: 10pt
colorlinks: true
toc: true
---

<!-- Build: pandoc sb110-restoration-plan.md -o sb110-restoration-plan.pdf --pdf-engine=xelatex -V mainfont="DejaVu Serif" -->

> **Safety.** The SB-110 runs its finals at **+700 V DC** from an external supply, and that voltage stays on the filter capacitors after unplugging. Discharge before every hands-in session; never run the final cage open; work one-handed when live. Use a **50 Ω dummy load rated for 6 m** (not a light bulb) for all transmit work.

> **How to read this plan.** The SB-110 is far less documented than the SB-301, HW-101 or SB-102. Items marked **[SB-110]** come from SB-110/110A sources. Items marked **[family]** are SB-line practice (shared LMO, metering, relays and construction) that very likely applies but should be confirmed in the manual.

# 1. Source documents

| Document | Where | Use |
|---|---|---|
| **Heath SB-110A Assembly Manual** (178–180 pp.) | archive.org (K6KJN upload, OCR'd); ManualsLib #895692; manualzz | Primary reference. Only the front half's OCR (parts lists, assembly) was reachable; **alignment, specs, voltage and troubleshooting pages are pending** (§11). |
| **SB-110 service bulletin SB-110-1** (Nov 1969) | Heath list (puck.nether.net), Mar 1998 | The only SB-110 bulletin on record. |
| SB-110 vs. SB-110A thread (Jun 2003) | Heath list | Model identification. |
| Heath LMO threads (Apr 2012, K9STH, G3OOU) | Heath list | TRW tube-LMO service. |
| W5RKL, *HW-101 and SB-10x Restoration and Troubleshooting* | w5rkl.com | **[family]** first power-up, relays, bias, neutralizing practice. |
| SB-100/101/102 and HW-101 service bulletins | Heath list | **[family]** fixes for shared circuits. |
| Radiomuseum, RigReference | — | Specifications. |

# 2. Transceiver at a glance

## 2.1 Key facts [SB-110]

| Item | Value |
|---|---|
| Models | **SB-110** (c. 1965–69); **SB-110A** (1969 upgrade, list price $299) |
| Band | 6 m. Tunes 49.5–54.0 MHz in 500 kHz segments; **supplied crystals cover 50.0–52.0 MHz** (crystals 42.105, 42.605, 43.105 and one more MHz). More crystals extend coverage. |
| Modes | SSB, CW, TUNE; VOX/PTT, anti-VOX, ALC |
| Input / output | 180 W PEP in (SSB), 150 W (CW); about **100 W PEP / 90 W CW out** |
| Receiver | **0.1 µV for 15 dB (S+N)/N; NF ≤ 3 dB** (nuvistor front end); 2.1 kHz SSB filter (5 kHz at −60 dB); 1 W audio |
| Stability | < 100 Hz/hr after 20 min warm-up |
| IF | 3.395 MHz. Carrier crystals 3393.6 kHz (404-205), 3396.4 kHz (404-206), 3394.4 kHz (404-263, CW). Filter 404-283. |
| LMO | Preassembled, prealigned **tube-type LMO, Heath 110-28** (TRW family; it has its own tube and shield) |
| Calibrator | 100 kHz crystal (404-43, transmitter-mixer board) |
| Metering | S-meter; in transmit it reads plate current, ALC or relative power |
| Pilot lamps | **#47 and #53** (per parts list; confirm socket assignment) |
| Weight / size | about 14.9 × 6.7 × 13.4 in. |

**Telling the SB-110 from the SB-110A:**

- **SB-110:** the heterodyne crystal oscillator **V7 (6EA8)** is on the **Carrier Generator board**, and the four heterodyne crystals sit in a **single row**.
- **SB-110A:** V7 is moved to the **chassis**, leaving a blank V7 position on board 85-152 (which keeps V6, V8, V9). The crystals sit **2 × 2** under a cover plate. Heath moved V7 because of a problem with the oscillator on the board.
- Early units may have the larger SB-300-style crystal filter.
- The label sets the date code (e.g. "SB110 531…" = 1965, week 31).
- Published references (Penson 2nd ed.) reportedly have the two models backwards.

## 2.2 Power requirements [SB-110]

| Rail | Requirement |
|---|---|
| HV | **+700 V DC @ 250 mA** |
| LV B+ | **+250 V DC @ 100 mA** |
| Bias | **−115 V DC @ 10 mA** |
| Filaments | **12.6 V @ 4.355 A** |

Supply: HP-23 family (AC) or HP-13 (mobile), via the 11-pin plug.

> **Caution:** the SB-110 specification calls for **+250 V** B+. The HW-101 and SB-102 want the HP-23 B+ switch on **300 V**. **Confirm the correct HP-23 switch position in the SB-110A manual's Power Supply Connections section before powering up.** Also confirm the HP-23 bias can reach about −115 V.

## 2.3 Tube complement

From the manual parts list (OCR) plus the specifications ("seventeen tubes and one transistor"). **V numbers are only partly known; verify them against the manual.**

| Tube | Qty | Function (known or likely) | Notes |
|---|---|---|---|
| **6DS4 nuvistor** | 2 | Receiver RF amp and 1st mixer (V1, V2; nuvistor sockets) | Source of the 3 dB noise figure. Nuvistors are scarce: **test, don't swap casually.** |
| 6EA8 | 4 | Includes **V7 heterodyne crystal oscillator**; others mixers, speech and oscillators | A weak first stage needs MIC/CW gain near maximum for full output (field report). |
| 6AZ8 | 3 | Mixer and oscillator stages (verify) | — |
| **6EB8** | 1 | **Audio amp / output** (V6 per SB-110-1) | **Runs hot**; see SB-110-1. |
| 12AT7 | 1 | (verify) | — |
| 6CB6 | 1 | (verify) | — |
| **12BY7** | 1 | **Driver** | — |
| **6146** | 2 | Finals | 6146 vs. 6146B question (§3.3). |
| 0A2 | 1 | 150 V regulator | — |
| LMO tube | 1 | Inside LMO 110-28 | Keep the original brand; it affects calibration. |

**Semiconductors [SB-110]:**

- One transistor, **2N2712** (417-67).
- **1N191 germanium** detector diodes (56-26; about 10 total).
- Silicon diodes 56-28.
- **15 V zener 56-25**.
- **Silicon rectifiers 57-29** (750 mA, 100 PIV; 6 total).

# 3. What fails, ranked

## 3.1 The one factory bulletin: SB-110-1 (Nov 3, 1969) [SB-110]

| Item | Detail |
|---|---|
| Symptom | **Audio oscillation on CW** with sidetone level fully up. Hand capacitance affects the audio output; **C658 (20 µF)** seems intermittent when moved; **V6 overheats.** |
| Cause | B+ from the VOX amp **V4B** reaches the audio output grid **V6B** through **R49 (3.3 MΩ)**, the 500 kΩ sidetone control and **R64 (3.3 MΩ)**. That puts about **+3 V on the grid**, giving instability and excess plate current. |
| Fix | **Remove R49** from the receiver IF board (85-115) and fit a **500 pF ceramic disc** (21-13) in its place. |
| Restoration note | **Check whether your unit has this change.** A hot audio tube (V6, 6EB8) is a classic SB-110 symptom, also reported on SB-110As that oscillate when warm. Also replace C658. |

## 3.2 Capacitors

**Electrolytics (manual parts lists):**

| Group | Values | Where | Action |
|---|---|---|---|
| Circuit-board electrolytics | **10 µF** (25-54 / 25-115; several), **20 µF** (25-135, incl. **C658**), **100 µF** (25-117) | Receiver IF board (10 µF), carrier generator board (100 µF, 20 µF), audio/VOX | **Replace all**, observing polarity. Ratings weren't legible in OCR; use ≥ 50 V for cathode bypasses and match or exceed the original for anything on B+. |
| Bias filter | (on the −115 V line) | Chassis | Replace; **negative supply, so check polarity.** |
| Main filtering | In the HP-23 / HP-13 | — | Recap the supply (§3.6). |

**[family]** Expect leaky paper/Mylar coupling caps in the audio, VOX and ALC circuits (SB-100-3 lists C1–C3, C9 and C213-type VOX-delay caps). Replace the blue or tan Mylars in signal paths with film parts. Disc ceramics are usually fine.

## 3.3 Tubes, by risk

1. **6EB8 audio:** overheating from the SB-110-1 grid-bias fault, oscillation when warm.
2. **6146 finals:**
   - Emission and gas.
   - **6146 vs. 6146B:** owners have asked whether the 6146B is unsuitable in the SB-110A; the list thread has no recorded answer. Heath had 6146B neutralizing and choke-heating problems on the HW-101's high bands (HW-101-18) before approving GE 6146Bs (HW-101-49).
   - On 6 m, neutralization is most critical. **If you fit 6146Bs, re-neutralize carefully and watch the plate RF choke for heat.**
   - Prefer a matched 6146/6146A pair until the manual says otherwise.
3. **6DS4 nuvistors:** loss of gain, noise. Test them on a tester with nuvistor sockets/adapters.
4. **6EA8 (×4):** heterodyne oscillator (crystal activity), first transmit stage (low drive).
5. **12BY7 driver** and **LMO tube.**

Return each tube to its original socket, and record brands.

## 3.4 LMO (TRW tube type, 110-28) [family]

The same service as the SB-301/SB-10x tube LMOs:

| Symptom | Cause | Fix |
|---|---|---|
| Jumpy or erratic at certain dial points | Intermittent rotor contact in the tuning capacitor; DeoxIT helps only briefly | **Solder braid from the rotor to the frame** (G3OOU / K9STH method). Open **only one side** of the case; spot-welded cases must be drilled. |
| Stiff, warbly tuning, better when warm | Hardened grease on the worm gear / anti-backlash clutch leaves | Clean and relube with synthetic/moly grease. |
| Calibration shift | LMO tube changed | Use the same brand. |
| Tracking off between bands | **Drifted heterodyne crystals** (common; Heath used mixed suppliers) | Check each crystal's band with the calibrator; replace or retrim. |

**Never rotate the capacitor shaft with the stop washers loose** (calibration is lost). Don't remove the side plate that carries the variable capacitor.

## 3.5 Mechanical, switches, relays [family]

- **Dial drive:** split-washer friction pulley and the circular dial's spiral follower. Clean and relube; reform or replace the washers if the dial slips (dial threads on heathkit@groups.io).
- **Relays:** clean contacts with a paper strip; carbon on the T/R relay base causes chirp and slow recovery (HW-101-32 / SB-101-21).
- **All switches and pots:** DeoxIT. Check wafer rotor orientation.
- **Grounds:**
  - Tighten board, socket and rear-jack hardware.
  - Final socket rivets: drill out and use 6-32 hardware if loose (SB-101-5D).
  - Ground the final enclosure and side rails (SB-100-4).
  - At 50 MHz, ground quality matters even more.
- **Cabinet transverter hole:** many SB cabinets had a Molex knockout; the hole alone doesn't mean a mod.
- **Heterodyne-oscillator harmonic filtering:** owners report extra filtering on some SB-110s. Photograph the V7 area before changing anything.

## 3.6 Power supply (HP-23 / HP-13)

Do this first. **[family]** HP-23 work:

- C1–C4 → 150 µF 500 V.
- C5 B+ → 47 µF 450 V.
- **Bias caps C6/C7** (often open) → 47 µF 160 V+.
- Bleeders 100 kΩ 2 W; diodes 1N4007; grounded cord.
- Variac bring-up with resistive loads on each output.

Verify these against the SB-110 requirements in §2.2: **+700 V, +250 V, −115 V, 12.6 V @ 4.4 A.** Setting the B+ switch is a manual-check item.

# 4. Restoration plan

## 4.1 Phase 0: Assess cold

- Identify SB-110 vs. SB-110A (§2.1) and note the date code.
- Photograph everything; note mods (heterodyne harmonic filtering, transverter connector, non-stock tubes). **Check whether the SB-110-1 change (R49 → 500 pF) is present.**
- Pull and label the tubes; test them (nuvistors need the right adapter).
- Check the heterodyne crystals and **extra crystals** (coverage beyond 50–52 MHz).
- Inspect: C658, the audio-tube area for heat, final cage, plate RF choke, relays, dial drive.
- Run the manual's **resistance chart** (manual p. ~118) before power.

## 4.2 Phase 1: Supply

Recap and test the supply on a variac; confirm the rails against §2.2 **and the manual's B+ switch instruction**.

## 4.3 Phase 2: Clean

Vacuum and brush. Cleaner on swabs; keep it off the dial and meter plastics and the ink markings. DeoxIT all switches and pots.

## 4.4 Phase 3: Recap and resistor survey

1. Apply **SB-110-1** if absent. Replace C658.
2. Replace all board electrolytics and the bias-filter cap.
3. Replace signal-path Mylars in audio, VOX and ALC.
4. Lift-and-measure resistors; replace any > 10% out. Priority areas:
   - **audio and VOX** (R49/R64 network);
   - carrier oscillator plate loads (**[family]**: drift there caused low single-sideband output on the HW-101);
   - heterodyne oscillator and driver plate resistors;
   - ALC network.
5. Clean the relays.

## 4.5 Phase 4: LMO and dial

LMO rotor braid and regrease if the dial jumps or is stiff (§3.4). Clean and set the dial drive.

## 4.6 Phase 5: First power-up

1. Supply on a variac; **6 m dummy load** and speaker connected.
2. Check both pilot lamps (#47/#53) light.
3. Log voltages against the manual's **voltage chart (p. ~119)**.
4. Calibrator receive check across 50.0–52.0 MHz in 100 kHz steps.
5. **Set final bias before any transmit** (manual p. ~97).

## 4.7 Phase 6: Alignment (manual pp. ~95–100)

Detailed targets are pending the manual. The manual's order is **Alignment → Transmitter Alignment → Carrier Null → LMO Shifter → Dial Calibration**.

**[family] Practice to follow:**

- Warm up 30 min; plastic tool only; receiver first.
- **Heterodyne oscillator:** peak each crystal's coil on the slow-changing side of the peak, using the manual's test-point method.
- **Receiver RF:** peak the nuvistor stage coils on the calibrator with minimum signal. At 50 MHz, small slug moves matter.
- **Bias:** set the manual's resting plate current with PTT and no drive, METER on PLATE. *(Value pending; SB-10x practice is about 50 mA idle.)*
- **Neutralization:** RF output peak and plate dip must coincide on FINAL. The **[family] alternate method** (SB-100-2):
  1. Remove screen and plate voltage, discharging first.
  2. Drive in TUNE.
  3. Null the RF-probe reading at the antenna jack with the neutralizing capacitor.

  6 m is the most demanding band for this; re-neutralize after any final or driver tube change.
- **Carrier null:** equal residual carrier on USB and LSB.
- **LMO shifter:** zero beat in USB, switch to LSB without moving the dial, then adjust the shifter.
- **Dial calibration** against the 100 kHz calibrator.
- **Calibrator** zero beat: WWV can't be heard on 6 m. Use a known-frequency signal or counter, or zero beat on HF with a second receiver as the manual describes.
- **Low drive with MIC/CW near maximum** (field report, 6EA8 good): suspect carrier level (oscillator plate resistors, crystals), balanced-modulator balance, mixer injection (heterodyne crystal activity), 12BY7 drive and neutralization, in that order.

## 4.8 Phase 7: Optional

- Additional heterodyne crystals for 52–54 MHz coverage, from the manual's "Special Crystal Considerations" section.
- **[family]** WB8JKR/K4JPN-style audio and carrier tweaks. Apply only after a stock baseline.

# 5. Known symptom → cause quick list

| Symptom | Look at |
|---|---|
| Audio oscillation on CW, hot V6, hand-capacitance effects | **SB-110-1**: R49 → 500 pF; C658 |
| Receiver oscillates when warm; hot 6EB8 | SB-110-1 status; audio tube; bypass caps; grounds |
| Full CW output only with MIC/CW gain near max | Carrier oscillator level, balanced modulator, heterodyne injection, driver, neutralizing |
| Good receive, no transmit | Relay contacts, bias/mute lines, first transmit stage and LMO injection, driver, ALC |
| Dial jumps or erratic | LMO rotor contact → braid fix |
| Tracking off between 500 kHz segments | Heterodyne crystals |
| Chirp or slow recovery | T/R relay carbon |

# 6. Operation notes

- Use a 6 m-rated dummy load for tune-up; keep key-down short.
- Zero-set on the nearest 100 kHz calibrator point before operating.
- Don't run the SB-110 as an exciter into a linear amplifier until bias, neutralization and ALC are verified.

# 7. Tips and tricks

- Keep spare 6DS4 nuvistors. They're the hardest tube to source, and the receiver's performance depends on them.
- Keep a matched 6146 pair, a 12BY7, 6EB8, 6EA8s, and #47/#53 lamps.
- Record heterodyne crystal frequencies and positions before removal.
- On 6 m, keep lead dress and shields exactly as built.

# 8. Maintenance schedule

| Interval | Task |
|---|---|
| Each session | 30 min warm-up; calibrator zero-set. |
| 6 months | Exercise switches; S-meter zero. |
| Yearly | Bias and carrier null check; receive benchmark on the calibrator; relay cleaning if chirp appears. |
| 2–3 years | Neutralization check; retighten grounds; DeoxIT. |
| 5 years | Tube test (nuvistors and finals first); supply check. |
| ~15–20 years | Re-check electrolytics. |

# 9. Parts sources

- Mouser / Digi-Key: electrolytics, film caps, resistors.
- HP-23 rebuild kits.
- Nuvistors (6DS4): specialty tube dealers; test before buying.
- Heathkit-Radios and heathkit (groups.io): SB-110 parts units, crystals, dials.

# 10. Sources

- Heath, *SB-110A Assembly Manual*, archive.org (K6KJN) and ManualsLib #895692.
- Heath list (puck.nether.net):
  - SB-110 service bulletins (Mar 1998);
  - "SB110 Question to Owners" (Jun 2003);
  - "SB-110A?" / "SOLVED" (Apr 2012);
  - "SB-110 VFO's" (Apr 2012);
  - "SB-110A Question – 6146Bs" (Feb 2003);
  - SB-110A oscillation (Oct 1997);
  - SB-110A low drive (Feb 1999);
  - SB-110 no transmit (Jun 2000);
  - SB-110 heterodyne filtering (Dec 2004).
- Radiomuseum SB-110A; RigReference SB-110A.
- **[family]** W5RKL SB-10x guide; SB-100/101/102 and HW-101 service bulletins; Latta HP-23 restoration.

# 11. Pending manual cross-check

Field documentation for the SB-110 is thin, so the manual matters more here than for the other three rigs. Items to verify:

- **HP-23 B+ switch setting** (250 vs. 300 V).
- Full tube list with V numbers.
- Electrolytic list with designators and voltages.
- Bias procedure and resting current.
- Neutralizing procedure.
- Heterodyne crystal list and test-point voltages.
- The resistance (p. ~118) and voltage (p. ~119) charts.
- The troubleshooting chart (p. ~117).
- Pilot lamp sockets.
- Whether the SB-110A manual already includes SB-110-1.

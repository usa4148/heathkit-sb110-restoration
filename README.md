# Heathkit SB-110 / SB-110A Restoration Plan

A restoration plan for the Heathkit SB-110 and SB-110A 6-meter SSB/CW transceivers and their HP-23/HP-13 power supply. It covers which parts fail with age, service bulletin SB-110-1, how to tell the SB-110 from the SB-110A, the tube-type LMO, a phased restoration procedure, alignment practice and maintenance.

**Status:** Rev. 2, checked against the original Heath SB-110A assembly manual (595-1145-01). Page references are the manual's printed page numbers. A few items the manual doesn't cover are still marked **[family]** (SB-line practice).

## Files

- [`sb110-restoration-plan.md`](sb110-restoration-plan.md) — source (pandoc markdown)
- [`sb110-restoration-plan.pdf`](sb110-restoration-plan.pdf) — rendered PDF

## Build

```sh
pandoc sb110-restoration-plan.md -o sb110-restoration-plan.pdf \
  --pdf-engine=xelatex -V mainfont="DejaVu Serif"
```

## Safety

The finals run at about +700 V DC from the external supply, which stays on the filter capacitors after unplugging. Discharge them before working inside.

**Power supply:** per the manual (p. 87), wire the HP-23A low-voltage section for the **+250 V** output, not the 300 V setting used by the HW-101 and SB-102. Bias is set with the transceiver's BIAS ADJ.

## Sources

- Heath SB-110A assembly manual 595-1145-01: archive.org (K6KJN), ManualsLib #895692
- Heath service bulletin SB-110-1 and SB-110 threads on the Heath mailing list
- SB-100/101/102 and HW-101 service bulletins; W5RKL SB-10x guide (family practice)

See also: [heathkit-sb301-restoration](https://github.com/usa4148/heathkit-sb301-restoration) · [heathkit-hw101-restoration](https://github.com/usa4148/heathkit-hw101-restoration) · [heathkit-sb102-restoration](https://github.com/usa4148/heathkit-sb102-restoration)

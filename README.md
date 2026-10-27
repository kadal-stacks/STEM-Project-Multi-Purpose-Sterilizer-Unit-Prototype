# STEM Project: Multi-Purpose Sterilizer Unit Prototype

<p align="center">
  <img src="https://img.shields.io/badge/Repository-GitHub-181717?style=flat-square&logo=github&logoColor=white" alt="Repository hosted on GitHub" />
  <img src="https://img.shields.io/badge/Documentation-Markdown-111827?style=flat-square&logo=markdown&logoColor=white" alt="Documentation written in Markdown" />
  <img src="https://img.shields.io/badge/Stage-Feasibility%20Study-0F766E?style=flat-square" alt="Project stage: feasibility study" />
  <img src="https://img.shields.io/badge/UV--C%20Safety-Review%20Required-B45309?style=flat-square" alt="UV-C safety review required" />
  <img src="https://img.shields.io/badge/License-Unlicense-64748b?style=flat-square" alt="Project source license: The Unlicense" />
</p>

> A student engineering research project exploring a modular, multi-purpose treatment chamber with an embedded controller. The design and its performance are still under study.

## Visual references

The photographs below are **real reference images found on Wikimedia Commons**, not images of our prototype. They provide context for existing UV treatment equipment and possible emitter types. Product specifications in a photo must not be taken as the specification for our own design.

<table>
  <tr>
    <td align="center" width="50%">
      <a href="https://commons.wikimedia.org/wiki/File:UV_STERILIZER_BOX_PHILIPS.jpg">
        <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/00/UV_STERILIZER_BOX_PHILIPS.jpg/500px-UV_STERILIZER_BOX_PHILIPS.jpg" alt="Photograph of a commercial enclosed UV treatment cabinet" width="300" />
      </a>
      <br /><sub><b>Enclosed UV cabinet</b><br />PT SUM HING INDONESIA · <a href="https://creativecommons.org/licenses/by-sa/4.0/">CC BY-SA 4.0</a></sub>
    </td>
    <td align="center" width="50%">
      <a href="https://commons.wikimedia.org/wiki/File:UV_Sterilisation.jpg">
        <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/3c/UV_Sterilisation.jpg/960px-UV_Sterilisation.jpg" alt="UV treatment of pipettes and tips inside a biosafety cabinet" width="300" />
      </a>
      <br /><sub><b>UV treatment in a cabinet</b><br />Orla Keogh · <a href="https://creativecommons.org/licenses/by/4.0/">CC BY 4.0</a></sub>
    </td>
  </tr>
  <tr>
    <td align="center" width="50%">
      <a href="https://commons.wikimedia.org/wiki/File:Germicidal_Lamp_1.jpg">
        <img src="https://upload.wikimedia.org/wikipedia/commons/8/87/Germicidal_Lamp_1.jpg" alt="Photograph of a compact germicidal fluorescent lamp" width="300" />
      </a>
      <br /><sub><b>Germicidal fluorescent lamp</b><br />Atlant · <a href="https://creativecommons.org/licenses/by/2.5/">CC BY 2.5</a></sub>
    </td>
    <td align="center" width="50%">
      <a href="https://commons.wikimedia.org/wiki/File:UV-C_LED_lamp.jpg">
        <img src="https://upload.wikimedia.org/wikipedia/commons/2/23/UV-C_LED_lamp.jpg" alt="Photograph of a UV-C LED module with heatsink and power connection" width="240" />
      </a>
      <br /><sub><b>UV-C LED module</b><br />Morrow363 · <a href="https://creativecommons.org/licenses/by-sa/4.0/">CC BY-SA 4.0</a></sub>
    </td>
  </tr>
</table>

<sub>Image attribution and licensing details are listed in the [component price study](docs/studi-harga-komponen.md). Images are linked from their original Wikimedia Commons files and are not endorsements or proposed final components.</sub>

## Documentation

- **[Component Price Study / BOM Review](docs/studi-harga-komponen.md)**: marketplace price observations, component comparison, preliminary budget, and purchase checks.
- **[Component-level schematic visual](docs/schematic-komponen-visual-v0.svg)**: a labeled illustration of the physical component types and low-voltage harness.
- **[Low-Voltage Schematic Draft](docs/schematic-low-voltage-v0.svg)** and [design notes](docs/schematic-notes-v0.md): JST-XH pinouts, LCD I²C, door input, and relay/MOSFET driver alternatives.

> **Image policy:** photographs are external reference imagery from Wikimedia Commons. They are not images of this prototype and are not endorsements of the project. Attribution and license links are documented in the BOM review.

## Candidate hardware marks

<p align="center">
  <img src="https://img.shields.io/badge/Candidate-STC8H1K08-2563eb?style=flat-square" alt="Candidate microcontroller: STC8H1K08" />
  <img src="https://img.shields.io/badge/Candidate-CH32V003-7c3aed?style=flat-square" alt="Candidate microcontroller: CH32V003" />
</p>
<p align="center">
  <a href="https://commons.wikimedia.org/wiki/File:RISC-V-logo.svg">
    <img src="https://upload.wikimedia.org/wikipedia/commons/9/9a/RISC-V-logo.svg" alt="RISC-V logo" width="160" />
  </a>
  <br /><sub>The RISC-V mark identifies the architecture of the CH32V003 candidate only. It does not indicate final MCU selection or endorsement by RISC-V.</sub>
</p>

## Current status

**Phase:** feasibility study and component price review. No final bill of materials (BOM), schematic, firmware architecture, validated treatment process, or electrical safety certification has been completed.

### Current design considerations

- Modular removable rack concept for different item sizes.
- Candidate MCU platforms: STC8H1K08 and CH32V003. Selection is not final.
- 16x2 display and door-state input are considered for the user interface.
- UV-C hardware, ballast/driver, enclosure, interlock, and independent cutoff need careful specification before any powered test.

## Safety and scope

**UV-C radiation and mains voltage can cause serious injury.** Do not operate an exposed UV-C source. Any future prototype must be reviewed for an opaque enclosure, fail-safe door interlock, independent safety cutoff, and appropriate electrical protection. Do not claim sterilization without suitable process and microbiological validation.

This repository is for educational and study-assignment purposes. The prototype is preliminary and is not intended for commercial use.

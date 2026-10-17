# STEM Project: Multi-Purpose Sterilizer Unit Prototype

<p align="center">
  <img src="https://img.shields.io/badge/Repository-GitHub-181717?style=for-the-badge&logo=github&logoColor=white" alt="Repository hosted on GitHub" />
  <img src="https://img.shields.io/badge/Documentation-Markdown-111827?style=for-the-badge&logo=markdown&logoColor=white" alt="Documentation written in Markdown" />
  <img src="https://img.shields.io/badge/Stage-Feasibility%20Study-0F766E?style=for-the-badge" alt="Project stage: feasibility study" />
  <img src="https://img.shields.io/badge/UV--C%20Safety-Review%20Required-B45309?style=for-the-badge" alt="UV-C safety review required" />
</p>

> A student engineering research project exploring a modular, multi-purpose treatment chamber with an embedded controller. The design and its performance are still under study.

## Visual references

The photographs below are **real reference images found on Wikimedia Commons**, not images of our prototype. They provide context for existing UV treatment equipment and possible emitter types. Product specifications in a photo must not be taken as the specification for our own design.

<table>
  <tr>
    <td align="center" width="34%">
      <a href="https://commons.wikimedia.org/wiki/File:UV_STERILIZER_BOX_PHILIPS.jpg">
        <img src="https://upload.wikimedia.org/wikipedia/commons/0/00/UV_STERILIZER_BOX_PHILIPS.jpg" alt="Photograph of a commercial enclosed UV sterilizer cabinet" width="240" />
      </a>
      <br /><sub><b>Enclosed UV cabinet</b><br />PT SUM HING INDONESIA · <a href="https://creativecommons.org/licenses/by-sa/4.0/">CC BY-SA 4.0</a></sub>
    </td>
    <td align="center" width="33%">
      <a href="https://commons.wikimedia.org/wiki/File:Germicidal_Lamp_1.jpg">
        <img src="https://upload.wikimedia.org/wikipedia/commons/8/87/Germicidal_Lamp_1.jpg" alt="Photograph of a compact germicidal fluorescent lamp" width="240" />
      </a>
      <br /><sub><b>Germicidal fluorescent lamp</b><br />Atlant · <a href="https://creativecommons.org/licenses/by/2.5/">CC BY 2.5</a></sub>
    </td>
    <td align="center" width="33%">
      <a href="https://commons.wikimedia.org/wiki/File:UV-C_LED_lamp.jpg">
        <img src="https://upload.wikimedia.org/wikipedia/commons/2/23/UV-C_LED_lamp.jpg" alt="Photograph of a UV-C LED module with heatsink and power connection" width="200" />
      </a>
      <br /><sub><b>UV-C LED module</b><br />Morrow363 · <a href="https://creativecommons.org/licenses/by-sa/4.0/">CC BY-SA 4.0</a></sub>
    </td>
  </tr>
</table>

<sub>Image attribution and licensing details are listed in the [component price study](docs/studi-harga-komponen.md). Images are linked from their original Wikimedia Commons files and are not endorsements or proposed final components.</sub>

## Documentation

- **[Component Price Study / BOM Review](docs/studi-harga-komponen.md)**: marketplace price observations, component comparison, preliminary budget, missing cost items, purchase checks, technical references, and visual-source attributions.

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

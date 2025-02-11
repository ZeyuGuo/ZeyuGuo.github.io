---
title: "FPGA-based process, voltage, and temperature insensitive picosecond resolution timing generators with offset correction for automatic test equipment"
collection: publications
category: manuscripts
permalink: /publication/2009-10-01-paper-title-number-1
# excerpt: ''
date: 2025-02-01
venue: 'Rev. Sci. Instrum.'
# slidesurl: 'http://academicpages.github.io/files/slides1.pdf'
paperurl: 'http://zeyuguo.github.io/files/timing-gen.pdf'
citation: 'Guo Z, et al. &quot;FPGA-based process, voltage, and temperature insensitive picosecond resolution timing generators with offset correction for automatic test equipment.&quot; <i>Rev. Sci. Instrum.</i>. 1 February 2025; 96 (2): 024702.'
---

This paper presents the implementation of a picosecond resolution timing generator (TG) insensitive to process, voltage, and temperature (PVT) variations for automatic test equipment. The TG is implemented in field-programmable gate arrays (FPGAs) using two-stage time interpolation, which utilizes a multi-phase generator, IDELAY3, and carry-chain resources. To enhance the test rate, each channel of the proposed TG consists of four parallel operating edge generators. The TG performance will deteriorate severely without offset correction due to its sensitivity to PVT variations. To improve the adaptability of the TG, we design a robust offset canceler to ensure stable performance of the TG, resilient to PVT variations. With the proposed architecture and offset canceler, the PVT-insensitive TG achieves a time resolution of 5 ps and offers a maximum dynamic range of 10 s. It also shows improved worst case integral non-linearity ranging from −4.7 to +4.6 ps with the operating temperature continuously varying from 15 to 65 °C and voltage ranging from 0.95 to 1.01 V in FPGAs. The proposed TG can be implemented in the Ultrascale or Ultrascale+ FPGA platform.

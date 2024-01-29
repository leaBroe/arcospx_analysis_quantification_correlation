# Detection of Actin Polymerization Waves in Rat Embryonic Fibroblasts

## Overview
This project, undertaken at the Pertz Lab, University of Bern, delved into the dynamics of actin polymerization waves in rat embryonic fibroblasts (REF52 cells). The aim was to use the ARCOS algorithm (https://github.com/bgraedel/arcos4py.git) to detect actin polymerization waves, quantify them and calculate the cross correlation to myosin and rGBD channels. Another goal of the project was the development and application of ARCOSpx, an extension of the ARCOS algorithm, designed for the tracking and analysis of cellular events, that can convert images directly into tracked collective events. The focus lay on examining the dynamics between actin waves, myosin, and rGBD channels, thereby unveiling the regulatory mechanisms of RhoA in these processes.  

## Objectives
- **Development of ARCOSpx Plugin**: Enhancing the ARCOS algorithm to convert images directly into tracked collective events.  
- **Understanding Actin Dynamics**: Investigating the patterns, directionality, and regulation of actin polymerization waves in REF52 cells.  
- **Elucidating RhoA's Role**: Exploring how RhoA functions as a negative regulator in the assembly and disassembly of these waves.  

## Methodology  
- **Cell Segmentation and Wave Tracking**: Techniques developed to segment the cells and track the progression and directionality of actin polymerization waves. For the tracking and quantification part, please see the file [arcospx_analysis_tracking_quantification_complete.ipynb](https://github.com/leaBroe/arcospx_analysis_quantification_correlation/blob/master/arcospx_analysis_tracking_quantification_complete.ipynb)  
- **Cross-Correlation Analysis**: Extensive use of Python's scipy library for temporal and spatial correlation studies between actin, myosin, and rGBD channels. For the Cross-Correlation of the Myosin and rGBD Channels please see [cross_correlation.ipynb](https://github.com/leaBroe/arcospx_analysis_quantification_correlation/blob/master/cross_correlation.ipynb)  

## Findings  
- **Actin Wave Characteristics**: Identified specific patterns in the movement of actin waves, predominantly towards the cell center.  
- **RhoA's Regulatory Function**: Teh results support RhoA's role as a negative regulator, influencing the disassembly phases of actin polymerization waves.  
- **Spatiotemporal Correlations**: Established correlations between the actin waves and myosin and rGBD channels, indicating potential regulatory mechanisms.  

## Conclusion and Future Work
This project aimed to contribute to the broader understanding of actin polymerization dynamics in cellular signaling. It sought to highlight the potential complexities in the regulatory roles of proteins like RhoA within these processes.  

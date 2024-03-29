# Detection of Actin Polymerization Waves and Cross-Correlation with Myosin and rGBD Channels in Rat Embryonic Fibroblasts using ARCOS

## Overview
This research project was done at the Pertz Lab, Institute of Cell Biology at the University of Bern. The aim of the project was to use the ARCOS algorithm (https://github.com/bgraedel/arcos4py.git) to detect actin polymerization waves, quantify them and calculate the cross correlation to myosin and rGBD channels in rat embryonic fibroblast cells (REF52). Another goal of the project was the development of ARCOSpx, an extension of the ARCOS algorithm, designed for the tracking and analysis of spatiotemporal correlations, that can convert images directly into tracked collective events. 

## Objectives
- **Development of ARCOSpx Plugin**: Enhancing the ARCOS algorithm to convert images directly into tracked collective events. The plugin can be found at: [https://github.com/bgraedel/arcosPx-napari.git](https://github.com/bgraedel/arcosPx-napari.git) 
- **Understanding Actin Dynamics**: Investigating the patterns, directionality, and regulation of actin polymerization waves in REF52 cells.  
- **Elucidating RhoA's Role**: Exploring how RhoA functions as a negative regulator in the assembly and disassembly of these waves.  

## Methodology  
### Data Collection and Preprocessing
Rat embryonic ﬁbroblasts (REF52) were treated with Platelet Derived Growth Factor (PDGF) 24 hours before real-time microscopic imaging. To mitigate the eﬀects of photobleaching during microscopy imaging, we employed a histogram matching technique. In order to make the tracking more faster afterwards, we then binned the time series images using a median ﬁlter and subsequently removed the background using arcos4py (version 0.2.3).  
### Segmentation of Fibroblast Cells and Tracking of Actin Polymerization Events
In order to avoid that the partially high signals around the edges of the cells would be falsely detected as polymerisation waves, we segmented the cells in order to calculate a distance map. The segmentation was carried out using the python package cellpose (version 2.2.3). The tracking of the actin polymerization events was done by the track events function of arcos4py.
### Quantification of Actin Polymerization Waves
The result of the event tracking process was a labeled image, where different objects in the image are marked with unique integer labels. These labels are then analyzed using the regionprops function from the skimage.measure Python package. This function calculates various properties for each labeled region, including area (pixel count), centroid (center of mass), label (unique identifier), and intensity mean (average pixel intensity). Additionally, for each uniquely identified object in the dataset, the data is isolated and sorted by the frame number. The x and y coordinates of the object's start and end points is used to determine the object's lifetime (duration across frames), average size (mean area), and average velocity (calculated from position changes over time).
### Calculation of Start and End Points of the Tracked Polymerization Waves 
Each wave, identified by a unique ID, had its start and end points (x and y coordinates) determined and visualized on the initial frame of an actin imaging time series. All the start and end points of the waves were plotted together, despite occurring at different times. A distance transform was applied to the segmented cellular structures, creating a matrix with values increasing from the cell periphery to the center. This grading allowed for quantitative analysis of each point's spatial position within the cell, with higher values indicating points further from the cell edge and lower values indicating proximity to the edge. For each wave, the distance map values at the start and end points were calculated to determine the direction of the wave's movement. The differences between start and end points for all waves were statistically analyzed using a Wilcoxon-signed rank test, suitable for non-normally distributed and paired data. Additionally, the magnitude of the distance between these points was correlated with their respective distances to the cell border. 
### Velocity Calculation of Polymerization Waves 
Due to the tendency of polymerization waves to split into different directions, using centroids as start and end points for speed calculation is not ideal. Instead, each wave, identified by a unique ID and its splitting subevents, are individually labeled. The centroids of these smaller events are calculated, and their velocities are determined. The average velocity of these subevents is then used to represent the overall velocity of each tracked wave.  
  
For the tracking and quantification part, please see the file [arcospx_analysis_tracking_quantification_complete.ipynb](https://github.com/leaBroe/arcospx_analysis_quantification_correlation/blob/master/arcospx_analysis_tracking_quantification_complete.ipynb)

### Cross-Correlation Analysis
The intensity values for each channel was extracted for a single event and plotted over time. For this, we set a middle frame where the tracked polymerization event is fully visible and extract the intensity values for the event in a range of 50 frames before and after the middle frame. The intensity values are then plotted over time. We then did this for all frames where the specific events took place. We repeated this for middle frames ranging from 180 to 246 (this was the range at which the specific tracked polymerization wave was present). From these 66 frames we took the average and repeated this for the other two channels. For the further cross-correlation, we normalized the intensities. The cross-correlation was done using the scipy package for python (version 1.11.4).  

For the Cross-Correlation of the Myosin and rGBD Channels please see [cross_correlation.ipynb](https://github.com/leaBroe/arcospx_analysis_quantification_correlation/blob/master/cross_correlation.ipynb)  

To validate the cross-correlation analysis methodology described above, a data set was also evaluated which had previously been analysed using a similar method. This also involves REF52 cells, which, however, are on PLL-g-PEG polymer and therefore cannot adhere. In addition, they were treated with Nocodazole, an anti-mitotic agent, which causes microtubules to depolymerise, leading to global rhoA activation and thus to RhoA oscillations. 

For the Cross-Correlation analysis of those cells please see [REF52_cross_correlation.ipynb](https://github.com/leaBroe/arcospx_analysis_quantification_correlation/blob/master/REF52_cross_correlation.ipynb)  

The previous analysis (carried out by Lucien Hinderling) is also in this repository for comparison: [temporal_correlation.ipynb](https://github.com/leaBroe/arcospx_analysis_quantification_correlation/blob/master/temporal_correlation.ipynb)  

## Findings  
- **Actin Wave Characteristics**: Identified specific patterns in the movement of actin waves, predominantly moving towards the cell center.  
- **RhoA's Regulatory Function**: The results support RhoA's role as a negative regulator, influencing the disassembly phases of actin polymerization waves.  
- **Spatiotemporal Correlations**: Established correlations between the actin waves and myosin and rGBD channels, indicating potential regulatory mechanisms.  

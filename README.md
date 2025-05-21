 # SIIM Hackathon 2025  -  Standardized, personal training data for GenAI hanging protocols
 
 ## Introduction
 Gen AI can today produce a good draft of report impressions based on learning the report history of the radiologist.
 We believe that GenAI could today produce valid hanging protocols for viewers if it had enough training data.

 We want to  propose a standardized way of storing personal hanging protocol Gen AI training data.  
 This data would be used by PACS viewers or AI agents to infer the appropriate display of the images available.  
 Radiologists would no longer have to train/configure each viewer they encounter.  
 They would instead provide access to their personal training data repository to the viewer software. 
 The viewers would not only use the data for display but also provide the ability to add new hanging protocol training cases to the repository. 
 
If we do not standardize how this information is stored early on radiologists will have to train each system separately.
We would also lose the benefit of accelerated development of hanging protocol AI agents because of lack of standardization.

## Example training data format
Each stored hanging protocol training data point would be composed of a folder containing:
1. A screenshot of the layout with privacy mode on.
2. A [hanging protocol DICOM information object](https://dicom.nema.org/medical/dicom/current/output/chtml/part03/sect_C.23.html) defining the layout and which series was assigned to which viewport (and other details).
3. Separate folder for each study of the patient containing the metadata of each study/series of the patient in [static DICOMweb](https://github.com/RadicalImaging/Static-DICOMWeb) format.  Therefore each series/displayset will also include a thumbnail image. 
4.  A way to identify which study was the current.


The goal being that a hanging protocol AI agent could, using the studies and series level metadata of the current and prior studies, find the most appropriate layout.  
We believe that having the full study and series metadata, in addition to the thumbnails


 

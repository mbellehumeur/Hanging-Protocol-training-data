 # SIIM Hackathon 2025  -  Standardized, personal training data for GenAI hanging protocols
 
 Gen Ai can effectively produce a good draft of report impressions based on learning the report history of the radiologist.
 We believe that GenAI could today produce valid hanging protocols for viewers if it had enough training data.

 So, we want to  propose a standardized way of storing personal hanging protocol Gen AI training data.  
 This data would be used by PACS viewers to infer the appropriate display of the images available.  
 Radiologists would no longer have to train/configure each viewer they encounter.  
 They would instead provide access to their personal training data repository to the viewer software. 
 The viewers would not only use the data for display but also provide the ability to add new hanging protocol training cases to the repository. 
 
If we do not standardize how this information is stored, radiologists will have to train each system separately.

## Format
Each stored hanging protocol training data point wiould be composed of a folder containing:
1. A screenshot of the layout with privacy mode on.
2. A hanging protocol DICOM object defining the layout and which series was assigned to which viewport (and other details).
3. Separate folder for each study of the patient containing the metadata of each study/series of the patient in static DICOMweb format.  Therefore each series/displayset will also include a thumbnail image. 
4.  A way to identify which study was the current.


The goal being that a hanging protocol AI agent could, using the metadata of the current and prior studies, find the most appropriate layout.  


 

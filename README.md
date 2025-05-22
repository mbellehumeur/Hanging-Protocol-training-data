 # SIIM Hackathon 2025  -  Standardized, personal training data for GenAI hanging protocols
 
 ## Introduction
 Gen AI / LLMs can today produce a good draft of report impressions based on learning the report history of the radiologist.
 We believe that GenAI could today produce valid hanging protocols for viewers if it had enough training data.

 We want to  propose a standardized way of storing personal hanging protocol Gen AI training data.  
 This data would be used by PACS viewers or AI agents to infer the appropriate display of the images available.  
 Because of standardization, radiologists would no longer have to train/configure each viewer they encounter.  
 They would instead provide access to their personal training data repository to the viewer software. 
 The viewers would not only use the data for display but also provide the ability to add new hanging protocol training cases to the user's repository.

## Why do this? 
If we do not standardize how this information is stored early on radiologists will have to train each system separately.
We would also lose the benefit of accelerated development of hanging protocol AI agents because of lack of standardization.

## Criterias
1. The training data should be human readable.  Therefore we would use DICOMweb/JSON encoding instead of binary.
The training data should be human manageable.  
2. The size of the data should be small enough that radiologist can keep their own backup copy, modify it manually if they wish and create multiple repositories if they need too.


## Example training data format

Each stored hanging protocol training data point would be composed of a folder containing:
1. A screenshot of the layout with privacy mode on.
2. A [hanging protocol DICOM information object](https://dicom.nema.org/medical/dicom/current/output/chtml/part03/sect_C.23.html) defining the layout and which series was assigned to which viewport (and other details).  This object would not try to define rules for the hanging protocol but just store what the user selected.  Also of interest is the work in [section V](https://dicom.nema.org/medical/dicom/current/output/chtml/part17/chapter_V.html).
3. Separate folder for each study of the patient containing the metadata of each study/series/image(object) of the patient in [static DICOMweb](https://github.com/RadicalImaging/Static-DICOMWeb) format.  Therefore each display set will also include a thumbnail image. Patient level information and bulk data (DICOM image data) would not be stored.
4.  A way to identify which study was the current.


The goal being that a hanging protocol AI agent could, using the studies and series level metadata of the current and prior studies, find the most appropriate layout. 


We believe that having the full study/series/image metadata, in addition to the thumbnails,  allow AI to compete


 ## Viewer support

Viewers would at a minimum need to support reading the hanging protocol object and assign the series specified to the layout.  Viewers that already support the existing standard object would be advantaged.

The request for the hanging protocol object would be done by the worklist or the viewer.

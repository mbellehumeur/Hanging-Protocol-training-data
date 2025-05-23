 # SIIM Hackathon 2025  -  Standardized, personal training data for GenAI hanging protocols
 
 ## Introduction
 Gen AI / LLMs can today produce a good draft of report impressions based on learning the report history of the radiologist.
 We believe that GenAI could today produce reasonably valid hanging protocols if it had enough training data.

 Therefore, we want to  propose a standardized way of storing personal hanging protocol Gen AI training data.  
 This data would be used by PACS viewers or AI agents to infer the appropriate display of the images available. 


 Because of standardization, radiologists would no longer have to train/configure each viewer they encounter.  
 They would instead provide access to their personal training data repository to the viewer software. 


Ideally, the viewers would not only use the data for display but also provide the ability to add new hanging protocol training cases to the user's repository.

We believe that having the full study/series/image metadata, in addition to the thumbnails, could allow AI to compete with rule based systems.  Especially when those systems are not constantly maintained by highly skilled individuals.  

Gen AI would also enable personal hanging protocols which is almost impossible today because of maintenance costs.  

## Why do this? 
If we do not standardize how this information is stored early on radiologists will have to train each system separately.
We would also lose the benefit of accelerated development of hanging protocol AI agents because of lack of standardization.
We could reallocate the significant resources spent on hanging protocols to other important tasks like reporting integration and workflow, data quality, security, ect.

## Criterias
1. The training data should be human readable.  Therefore we would use DICOMweb/JSON encoding instead of DICOM binary.
 
2. The training data should be portable. The size of the data should be small enough that radiologist can keep their own backup copy, modify it manually if they wish and create multiple repositories if they need to.


## Example training data format

Each stored hanging protocol training data point would be composed of a folder containing:
1. A screenshot of the layout with privacy mode on.
2. A [hanging protocol DICOM information object](https://dicom.nema.org/medical/dicom/current/output/chtml/part03/sect_C.23.html) defining the layout and which series was assigned to which viewport (and other details).  This object would not try to define rules for the hanging protocol but just store what the user selected.  Also of interest is the work in [section V](https://dicom.nema.org/medical/dicom/current/output/chtml/part17/chapter_V.html).  THe hard work of defining monitor geometry, layouts, viewport types, viewport linking, ect, all that is already existing in the DICOM standard.
3. Separate folder for each study of the patient containing the metadata of each study/series/image(object) of the patient in [static DICOMweb](https://github.com/RadicalImaging/Static-DICOMWeb) format.  Therefore each display set will also include a thumbnail image. Patient level information and bulk data (DICOM image data) would not be stored.
4.  A way to identify which study was the current.


The goal being that a hanging protocol AI agent could, using the studies and series level metadata of the current and prior studies, find the most appropriate layout. 

## How Hanging Protocol AI Agents Work


```
+-----------------------------------+         +---------------------+         +-------------------+
|                                   |         |                     |         |                   |
|   PACS Viewer                     +-------->+  Hanging Protocol   +-------->+   Display Layout  |
| (current & prior study metadata   |         |    AI Agent         |         | (images assigned  |
|  and thumbnails)                  |         | (selects protocol   |         |   to viewports)   |
|                                   |         |  and assigns series |         |                   |
+-----------------------------------+         +---------------------+         +-------------------+
```
*The PACS viewer sends current and prior study metadata and thumbnails to the AI agent, which selects the best hanging protocol and returns the layout for display.*
*The PACS viewer sends study metadata and images to the AI agent, which selects the best hanging protocol and returns the layout for display.*

 ## Viewer support

Viewers would at a minimum need to support reading the hanging protocol object and assign the series specified by the AI to the layout.  Viewers that already support the existing hanging protocol DICOM standard object would be advantaged as they should be.

The request for the hanging protocol object would be done by the worklist or the viewer.  They would provide the same study/series metadata that is in the training data and the AI agent would return the most appropriate hanging protocol from your training data and assign series to the defined viewports in the hanging protocol object. 




## How can I help?

If your hanging protocols are working OK, maybe take a few minutes in the near future to thank your technologists, imaging IT and vendor support team if you are not doing so regularly already.


Get in touch with your favorite IHE & DICOM committee standards writer or board member.  Thank them for their service and ask them if they feel that standardizing hanging protocol training data would be useful.


If you feel that having open-source software to support new or existing standards is useful,  consider donating to an organization that works on that.


# COVID 19 X-Ray Dataset
We are building a database of COVID-19 cases with chest X-ray or CT images. We are looking for COVID-19 cases as well as [MERS](https://en.wikipedia.org/wiki/Middle_East_respiratory_syndrome), [SARS](https://en.wikipedia.org/wiki/Severe_acute_respiratory_syndrome), and [ARDS](https://en.wikipedia.org/wiki/Acute_respiratory_distress_syndrome).

All images and data will be released publicly in this GitHub repo. Currently we are building the database with images from publications as they are images that are already available.

## Background
The 2019 novel coronavirus (COVID-19) presents several unique features. While the diagnosis is confirmed using polymerase chain reaction (PCR), infected patients with pneumonia may present on chest X-ray and computed tomography (CT) images with a pattern that is only moderately characteristic for the human eye [Ng, 2020](https://pubs.rsna.org/doi/10.1148/ryct.2020200034). COVID-19’s rate of transmission depends on our capacity to reliably identify infected patients with a low rate of false negatives. In addition, a low rate of false positives is required to avoid further increasing the burden on the healthcare system by unnecessarily exposing patients to quarantine if that is not required. Along with proper infection control, it is evident that timely detection of the disease would enable the implementation of all the supportive care required by patients affected by COVID-19.

In late January, a Chinese team published a paper detailing the clinical and paraclinical features of COVID-19. They reported that patients present abnormalities in chest CT images with most having bilateral involvement [Huang 2020](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736(20)30183-5/fulltext). Bilateral multiple lobular and subsegmental areas of consolidation constitute the typical findings in chest CT images of intensive care unit (ICU) patients on admission [Huang 2020](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736(20)30183-5/fulltext). In comparison, non-ICU patients show bilateral ground-glass opacity and subsegmental areas of consolidation in their chest CT images [Huang 2020](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736(20)30183-5/fulltext). In these patients, later chest CT images display bilateral ground-glass opacity with resolved consolidation [Huang 2020](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736(20)30183-5/fulltext).

COVID is possibly better diagnosed using radiological imaging [Fang, 2020](https://pubs.rsna.org/doi/10.1148/radiol.2020200432) and [Ai 2020](https://pubs.rsna.org/doi/10.1148/radiol.2020200642).

## Motivation

While PCR tests offer many advantages they are physical things that require shipping the test or the sample. X-ray machines can be plugged in to screen patients as long as they have electricity.

Imagine a future where we run out of tests and then the majority of radiologists get sick. AI tools can help general practitioners to triage and treat patients.

Companies are developing AI tools and deploying them at hospitals [Wired 2020](https://www.wired.com/story/chinese-hospitals-deploy-ai-help-diagnose-covid-19/). We should have an open database to develop free tools that will also provide assistance.

## Goal

Our goal is to use these images to develop AI based approaches to predict and understand the infection.
The tasks are as follows using chest X-ray or CT (preference for X-ray) as input to predict these tasks:

## Metadata
Here is a list of each metadata field, with explanations where relevant

| Attribute | Description |
|------|-----|
| patientid | Internal identifier |
| offset | Number of days since the start of symptoms or hospitalization for each image. If a report indicates "after a few days", then 5 days is assumed. This is very important to have when there are multiple images for the same patient to track progression. |
| sex | Male (M), Female (F), or blank |
| age | Age of the patient in years |
| finding | Type of pneumonia |
| survival | Yes (Y) or no (N) or blank if unknown|
| intubated | Yes (Y) if the patient was intubated (or ventilated) at any point during this illness or No (N) or blank if unknown. |
| went_icu | Yes (Y) if the patient was in the ICU (intensive care unit) or CCU (critical care unit) at any point during this illness or No (N) or blank if unknown.|
| needed_supplemental_O2 | Yes (Y) if the patient required supplemental oxygen at any point during this illness or No (N) or blank if unknown |
| extubated | Yes (Y) if the patient was successfully extubated or No (N) or blank if unknown |
| temperature | Temperature of the patient in Celsius at the time of the image|
| pO2 saturation | partial pressure of oxygen saturation in % at the time of the image |
| wbc count | white blood cell count in units of 10^3/uL at the time of the image |
| neutrophil count | neutrophil cell count in units of 10^3/uL at the time of the image |
| lymphocyte count | lymphocyte cell count in units of 10^3/uL at the time of the image |
| view | Posteroanterior (PA), Anteroposterior (AP), AP Supine (APS), or Lateral (L) for X-rays; Axial or Coronal for CT scans |
| modality | CT, X-ray, or something else |
| date | Date on which the image was acquired |
| location | Hospital name, city, state, country |
| filename | Name with extension |
| doi | Digital object identifier ([DOI](https://en.wikipedia.org/wiki/Digital_object_identifier)) of the research article |
| url | URL of the paper or website where the image came from |
| license | License of the image such as CC BY-NC-SA. Blank if unknown |
| clinical notes | Clinical notes about the image and/or the patient |
| other notes | e.g. credit |


## Sources
- Some data are sourced from [Identifying Medical Diagnoses and Treatable Diseases by Image-Based Deep Learning](https://www.cell.com/cell/fulltext/S0092-8674(18)30154-5).
- Healthy vs Pneumonia (prototype already implemented [Chester](https://mlmed.org/tools/xray/) with ~74% AUC, validation study [here](https://arxiv.org/abs/2002.02497))
- ~~Bacterial vs Viral vs COVID-19 Pneumonia~~ (not relevant enough for the clinical workflows)
- Survival/prognosis of patient

## Initial results

![](covid-xray-umap.png)

## Credits
- Skytells Research
    - Data Reformatting
- Zhang Lab
    - X-Ray Images
- ieee8023
    - X-Ray Images

## Contribute

- We can extract images from publications. Help identify publications which are not already included using a GitHub issue (DOIs we have are listed in the metadata file). There is a searchable database of COVID-19 papers [here](https://www.who.int/emergencies/diseases/novel-coronavirus-2019/global-research-on-novel-coronavirus-2019-ncov), and a non-searchable one (requires download) [here](https://pages.semanticscholar.org/coronavirus-research).

- Submit data to these sites (we can scrape the data from them):
    - https://radiopaedia.org/ (license CC BY-NC-SA)
    - https://www.sirm.org/category/senza-categoria/covid-19/
    - https://www.eurorad.org/ (license CC BY-NC-SA)

- Provide bounding box/masks for the detection of problematic regions in images already collected.

- See [SCHEMA.md](SCHEMA.md) for more information on the metadata schema.

*Formats:* For chest X-ray dcm, jpg, or png are preferred. For CT nifti (in gzip format) is preferred but also dcms. Please contact with any questions.

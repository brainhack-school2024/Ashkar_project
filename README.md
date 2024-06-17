---
type: "project" # DON'T TOUCH THIS ! :)
date: "2024-06-17" # Date you first upload your project.
# Title of your project (we like creative title)
title: "Generating synthetic CT scans from MRIs to enhance radiotherapy tretement planning"

# List the names of the collaborators within the [ ]. If alone, simple put your name within []
names: [Khaled Ashkar]

# Your project GitHub repository URL
 github_repo: git@github.com:brainhack-school2024/Ashkar1_project.git

# If you are working on a project that has website, indicate the full url including "https://" below or leave it empty.
website:

# List +- 4 keywords that best describe your project within []. Note that the project summary also involves a number of key words. Those are listed on top of the [github repository](github_repo:git@github.com:brainhack-school2024/Ashkar1_project.git), click `manage topics`.
# Please only lowercase letters
tags: [mri, ct, cbct, radiotherapy, treatement planning]

# Summarize your project in < ~75 words. This description will appear at the top of your page and on the list page with other projects..

summary:"This project aims to develop a deep learning model that generates reliable synthetic CT scans from MRIs only, Contrast and Field magnitude-agnostic to eliminate the need for additional CT scans in hospitals and clinics."

# If you want to add a cover image (listpage and image in the right), add it to your directory and indicate the name
# below with the extension.
image: ""
---

## Project definition
---
### Background

Over the past decades, medical imaging has significantly enhanced the diagnosis and treatment of oncological patients, particularly in radiotherapy (RT). Traditionally, 3D computed tomography (CT) is the primary imaging modality used in RT for accurate patient geometry, dose calculations, and plan optimization. However, CT exposes patients to ionizing radiation, which is a concern, especially for repeated simulations or vulnerable populations such as pediatric patients. Magnetic resonance imaging (MRI), with its superior soft-tissue contrast, has proven valuable for tumor and organ-at-risk delineation, patient positioning, and monitoring. Despite its advantages, MRI lacks the necessary tissue attenuation information required for accurate dose calculations, making CT still necessary in RT workflows. To overcome these challenges, recent advancements have focused on generating synthetic CT (sCT) images from MRIs. This approach aims to combine the superior imaging capabilities of MRI with the essential dose calculation information of CT, reducing the patient's exposure to radiation and simplifying the workflow. Artificial intelligence (AI) techniques, particularly machine learning and deep learning, have emerged as leading methods for creating sCT images from MRI data. These AI-driven methods have the potential to enhance the accuracy of RT planning and delivery. However, the field still faces the challenge of a lack of public datasets and standardized benchmarks to validate and compare different AI approaches. This project aims to develop and refine AI algorithms to generate high-quality CT scans from MRIs, thereby improving RT workflows and patient outcomes by leveraging the best features of both imaging modalities.

### Tools
This project relied on numerous tools such as:
1) Git and GitHub to use and share methods;
2) High performance computing (HPC), such as Google Colab, for executing scripts; 
3) Python packages, such as matplotlib, pandas and torch to save the data in torch arrays. 

### Data

The dataset can be downloaded from https://doi.org/10.5281/zenodo.7260705 and a detailed description is offered at "synthRAD2023_dataset_description.pdf".
The training datasets for Task1 is in Task1.zip, while for Task2 in Task2.zip. After unzipping, each Task is organized according to the following folder structure:
Task1.zip/
├── Task1
   ├── brain
    ├── 1Bxxxx
       ├── mr.nii.gz
       ├── ct.nii.gz
       └── mask.nii.gz

Each patient folder has a unique name that contains information about the task, anatomy, center and a patient ID. The naming follows the convention below:
[Task]    [Anatomy]    [Center]    [PatientID]
   1          B            A           001
In each patient folder, three files can be found: 
ct.nii.gz: CT image 
mr.nii.gz or cbct.nii.gz (depending on the task): CBCT/MR image
mask.nii.gz:image containing a binary mask of the dilated patient outline 
For each task and anatomy, an overview folder is provided which contains the following files:
[task]_[anatomy]_train.xlsx: This file contains information about the image acquisition protocol for each patient.
[task][anatomy][center][PatientID]_train.png: For each patient a png showing axial, coronal and sagittal slices of CBCT/MR, CT, mask and the difference between CBCT/MR and CT is provided. These images are meant to provide a quick visual overview of the data.

This challenge dataset contains imaging data of patients who underwent radiotherapy in the brain or pelvis region. Overall, the population is predominantly adult and no gender restrictions were considered during data collection. For Task 1, the inclusion criteria were the acquisition of a CT and MRI during treatment planning while for task 2, acquisitions of a CT and CBCT, used for patient positioning, were required. Datasets for task 1 and 2 do not necessarily contain the same patients, given the different image acquisitions for the different tasks.
Data was collected at 3 Dutch university medical centers:

Radboud University Medical Center
University Medical Center Utrecht
University Medical Center Groningen
For anonymization purposes, from here on, institution names are substituted with A, B and C, without specifying which institute each letter refers to.
All images were acquired with the clinically used scanners and imaging protocols of the respective centers and reflect typical images found in clinical routine. As a result, imaging protocols and scanner can vary between patients. A detailed description of the imaging protocol for each image, can be found in spreadsheets that are part of the dataset release (see dataset structure).

Data was acquired with the following scanners:
Center A:
MRI: Philips Ingenia 1.5T/3.0T
CT: Philips Brilliance Big Bore or Siemens Biograph20 PET-CT
CBCT: Elekta XVI

Center B:
MRI: Siemens MAGNETOM Aera 1.5T or MAGNETOM Avanto_fit 1.5T
CT: Siemens SOMATOM Definition AS
CBCT: IBA Proteus+ or Elekta XVI

Center C:
MRI: Siemens Avanto fit 1.5T or Siemens MAGNETOM Vida fit 3.0T
CT: Philips Brilliance Big Bore
CBCT: Elekta XVI

For task 1, MRIs were acquired with a T1-weighted gradient echo or an inversion prepared - turbo field echo (TFE) sequence and collected along with the corresponding planning CTs for all subjects. The exact acquisition parameters vary between patients and centers. For centers B and C, selected MRIs were acquired with Gadolinium contrast, while the selected MRIs of center A were acquired without contrast.
For task 2, the CBCTs used for image-guided radiotherapy ensuring accurate patient position were selected for all subjects along with the corresponding planning CT.
The following pre-processing steps were performed on the data:
Conversion from dicom to compressed nifti (nii.gz)
Rigid registration between CT and MR/CBCT
Anonymization (face removal, only for brain patients)
Patient outline segmentation (provided as a binary mask)
Crop MR/CBCT, CT and mask to remove background and reduce file sizes
The code used to preprocess the images can be found at: https://github.com/SynthRAD2023/. Detailed information about the dataset are provided in SynthRAD2023_dataset_description.pdf published here along with the data and will also be submitted to Medical Physics.

ETHICAL APPROVAL
Each institution received ethical approval from their internal review board/Medical Ethical committee:
UMC Utrecht approved not-WMO on 4/03/2022 with number 22/474 entitled: “Synthetizing computed tomography for radiotherapy Grand Challenge (SynthRAD)”.
UMC Groningen approved not-WMO on 20/07/2022 with number 202200310 entitled: “Synthesizing computed tomography for radiotherapy - Grand Challenge”.
Radboud UMC declared the study not-WMO on 17/10/2022 with number 2022-15950 entitled “Synthetizing computed tomography for radiotherapy Grand Challenge”.

### Project deliverables 
At the end of this project, these files will be made available:
 Python scripts to train the model or load the pre-trained versions ;
 A repository on GitHub.

## Results
---
### Progress overview
First, this project involved correcting the format of my dataset. I had to convert it to BIDS format and preprocess the Nifti files with fmriprep. These steps took longer than expected. So far, only one participant's files have been converted to BIDS format and preprocessed. However, I was able to run a first-level general linear model on this participant to present: 1) BOLD activity in the visual cortex and the superior frontal gyrus (SFG) when images were shown at this participant (effect of interest)  and 2) no significant region of BOLD activity when contrasting high vs low calorie snacks.

#####     Figure 1
![]

#####     Figure 2.
![]


### Tools I learned during this project

 [GitHub](https://github.com/): 

### Deliverables


### Future work


## Conclusion and acknowledgement


## References



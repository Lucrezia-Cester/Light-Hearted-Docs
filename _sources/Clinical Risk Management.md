---
documentid: synct-crmp-001
version: 1.0

---

# Clinical Risk Management - SyntheticCT


|             |                 |
|-------------|-----------------|
| Document Id | synct-crmp-v1.0 |
| Version     | 1.0             |
| Author      | Anil Mistry     |
|             |                 |


## Purpose 
This purpose of this document is to describe the activities involved in the clinical risk management process

This document is meant to be read and agreed-upon by the project owners, the CSC team, and the Clinical Scientific
Officer during design and development.

The document also provides traceability for risk controls throughout the project. 

## Scope

This document applies to SyntheticCT release 1.0.

## Definitions

| Term    | Definition                    |
|---------|-------------------------------|
| CRMF    | Clinical Risk Management File |
| CRMP    | Clinical Risk Management Plan |


## Roles and Responsibilities
 
| Role                    | Responsibilities                                                                                       |
|-------------------------|--------------------------------------------------------------------------------------------------------|
| Development Lead        | - Completing documentation <br>  - Gathering requirements <br >- Organising meetings with stakeholders |
| Clinical Lead           | - Organising meetings with stakeholders <br>  - Providing requirements                                 ||
| Clinical Safety Officer | - Final approval of clinical risk management activities.                                               |

### Resource allocation

| Role                    | Name               | Evidence of competence                    |
|-------------------------|--------------------|-------------------------------------------|
| Development lead        | Anil Mistry        | Stage 1 Clinical Risk Management Training |
| Clinical Lead           | Christopher Thomas | N/A                                       |
| Clinical Safety Officer | David Eaton        | Head of Department - clinical experience  |

## Project overview and clinical safety


### Impact of DCB0129 and DCB0160 on the project 

Since CSC will be both the Manufacturer and user of the software, the project will therefore adhere to all applicable 
requirements of DCB0129 and DCB0160 in this regard.


## Clinical Risk Management File 
 
The clinical risk matrix, evaluation and management process used is defined below and can also be found in more detail 
within the appendix. The hazard assessment process will follow the standard Clinical Risk Management System approach.
Hazards may be identified in other ways during the development and use of the programme such as:

- Discovery during design of a solution by supplier or NHS Organisation;
- Testing of amended functionality;
- Ad hoc testing of live service functionality;
- Reporting of an incident or problem within the live service; and

For each identified hazard, the following information will be defined, recorded and summarised in the Hazard Log:

- Hazard number;
- Hazard description;
- Potential clinical impact – this will describe the effect of the hazard in the care setting and potential impact on 
the patient;
- Possible causes – these may be technical, human, error etc. A hazard may have a number of causes; and
- Existing controls – these are identified existing controls or measures that are currently in place and will remain in 
place post implementation that provide mitigation again the hazard, i.e. will be used as part of the initial Hazard Risk 
Assessment.

Each Hazard will be discussed by the programme Clinical Safety team and any other appropriate people. They will perform 
the following tasks and record the outcome in the Hazard Log:

- Estimation of clinical risks
- Clinical risk evaluation 
- Clinical risk control option management

For each identified hazard estimation will be made of the clinical risk. This will include the severity of the hazard, 
the likelihood of the hazard and the resulting clinical risk. The estimation process will follow that established by the
safety processes defined in DCB0129.

## Hazard Log

| Hazard ID    | Hazard description                                                                                                                                                      | Potential clinical impact                                                                                                                                                                                                                                         | Possible causes                                                                                                                                               | Existing controls                                                                                                                                                                                                                                                            | Initial severity | Initial likelihood | Initial risk | Design controls 	                                                                                                                                                                                                                                                                                                                                                    | Final likelihood | residual risk     | residual risk comment                                                                                                                               |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|--------------------|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| SYNCT-HZ-001 | Incorrect Hounsfield units assigned to tissues.                                                                                                                         | Incorrect dose distribution calculated, leading to mistreatment (incorrect treatment such as over irradiation of OARs and poor coverage of target) or patient delays. Patient reverts to CT pathway -> Patient delays                                             | Trained model unable to process unfamiliar data.  Patient anatomy not representative of training data.  Patient scanned with incorrect orientation (non-HFS). | RT Checking and RT Treatment Planning to check HU values Thresholding tools on eclipse Diamond check > forces patient to water, checks dose distribution within tolerance                                                                                                    | Major            | Low                | 3            | Mean HU value <br> Histogram analysis of HU <br>>Acceptable range -1000HU to 2000HU <br> Comparing Volumes between CT and MRIs <br> Geometric scaling check <br> threshold on CT and MR <br>  Mean distance to agreement, DICE, Volume check.                                                                                                                        | Very Low         | 2                 | Checks will ensure significant discrepancies in contour difference will be noted in log file to alert user doing manual SynCT QA checks             |                                                                                                                                                                                                |
| SYNCT-HZ-002 | Wrong series/study sent.                                                                                                                                                | Incorrect HU values assigned to tissues, gives incorrect dose distribution <br> mistreatment or patient delays. No SynCT generated for patient. Correct series to be resent -> Slight delay in pathway. Re-imaging of patient -> longer delay in pathway          | Poor / lack of training	Work instruction for radiographers.                                                                                                   | Written instruction at end of MR protocol.                                                                                                                                                                                                                                   | Minor            | Low                | 1            | is_valid_function: Check to confirm Series name, Scanner, modality                                                                                                                                                                                                                                                                                                   | Very Low         | 1                 | Limits access to SynCT processing through predicate. Log file created for MRI's failing predicate to aid analysis on non-triggering SynCT inference |
| SYNCT-HZ-003 | Incorrect Protocol used for MRI imaging.                                                                                                                                | No SynCT generated for patient <br> Re-imaging of patient, delays in patient pathway.                                                                                                                                                                             | Poor / lack of training <br>Protocol not available. Clinician error on request form MRI vetting team book onto wrong MR scanner.                              | Work Instruction for radiographer. <br> Work instruction for clinicians for EPR referral. Availability of protocol on MR console.                                                                                                                                            | Minor            | Very low           | 1            |                                                                                                                                                                                                                                                                                                                                                                      | Very Low         | 1                 |                                                                                                                                                     |
| SYNCT-HZ-004 | Acquisition protocol parameters changed or alternative coil used on MR. Causes change in geometric distortion, signal intensity, scanned anatomy, FOV, missing tissues. | Incorrect HU values assigned to tissues, gives incorrect dose distribution <br> mistreatment or patient delays. Geometric distortion affects dose distribution <br> mistreatment or patient delays.                                                               | Optimisation of parameter by MR radiographer.<br>Changes to protocol during update <br> Removal of protocol during update                                     | Protocol is locked for all patients.<br>RT staff present on scanner. <br> Written instruction to provide limits on each parameter in protocol.                                                                                                                               | Considerable     | Medium             | 3            | is_valid_function: Check to confirm scanning parameters within tolerance (e.g. bandwidth, TE, TR, distortion correction ON). <br>Store backup of MRI scan protocol on GitHub alongside model.<br> Adding noise to training data. <br> Log file to output warnings of out of tolerance MR-specific dicom tags, where appropriate, for validation by MR physicists and | Very Low         | 2                 | Added info for Manual QA analysis by MR/Radiotherapy physicist. Automated QA checks before triggering inference.                                    |
| SYNCT-HZ-005 | Wrong HU as a result of artefact from prosthetic.                                                                                                                       | Causes incorrect HU values, incorrect dose distribution -> mistreatment or patient delays. Causes geometric distortion of image significant enough to affect dose distribution -> mistreatment or patient delays. Patient reverts to CT pathway -> patient delays | Trained model causes HU incorrect estimation of tissue within artefact region, differing from water > +/-50HU.                                                | Allow single prosthetic hip<br>planning work instruction to avoid hip implant <br> Fiducials are not a concern<br>SPACE-OAR affects MR contrast Electron density is water equivalent - get more info on this.<br>Planning to contour and force HU before Treatment planning. | Considerable     | Low                | 2            |                                                                                                                                                                                                                                                                                                                                                                      | Very Low         | 2                 |                                                                                                                                                     |
| SYNCT-HZ-006 | Unintended patient imaged with protocol. Synthetic CT generated when not required.                                                                                      | Planner misinterprets synthetic CT as true CT and treatment planning using MR-only planning pathway when not intended. Correct scan needs to be booked <br> delays in patient treatment                                                                           | Clinician error on request form MRI vetting team error in EPR interpretation.                                                                                 | MR-only pathway SOP document defining eligibility, pre-requisites (clinician's EPR request for MR-only prostate, no nodal involvement, ...). Oncologists training on how to                                                                                                  | Minor            | Very Low           | 1            |                                                                                                                                                                                                                                                                                                                                                                      | Very Low         | 1                 |                                                                                                                                                     |
| SYNCT-HZ-007 | Wrong patient orientation causes miscalculation of HU in Inference.                                                                                                     | Incorrect HU generated <br> Mistreatment or re-imaging of patient, delays in patient pathway.                                                                                                                                                                     | Poor / lack of training	Work instructions to ensure patients are scanned HFS.                                                                                 |                                                                                                                                                                                                                                                                              | Significant      | Very low           | 1            | Check in predicate for is_valid_function is HeadFirstSupine                                                                                                                                                                                                                                                                                                          | Very low         | 1                 | Risk of incorrect orientation now limited to radiographer set-up. can be resolved by training/ work instructions                                    |
| SYNCT-HZ-008 | Connection between MR and DicomServer goes down.                                                                                                                        | No SynCT generated for patient. Patient delayed while system comes back online.<br>Patient reverts to CT pathway <br> patient delays                                                                                                                              | DicomServer computer turns off/has fault. MRI machine system update by engineers.                                                                             |                                                                                                                                                                                                                                                                              | Minor            | Low                | 1            | Ability to send images from Eclipse or PACS to DicomServer                                                                                                                                                                                                                                                                                                           | Very low         | 1                 | Low chance of in-accessibility to SynCT for valid use.                                                                                              |
| SYNCT-HZ-009 | Docker container is lost/overridden/corrupted.                                                                                                                          | No SynCT generated for patient. Patient delayed while system comes back online.<br>Patient reverts to CT pathway <br> patient delays                                                                                                                              | DicomServer computer turns off/has fault.                                                                                                                     |                                                                                                                                                                                                                                                                              | Minor            | Low                | 1            | Restore Docker from GitHub.                                                                                                                                                                                                                                                                                                                                          | Very low         | 1                 | Very low risk of application being unavailable on GitHub.                                                                                           |
| SYNCT-HZ-010 | DicomServer goes down / becomes unavailable.                                                                                                                            | No SynCT generated for patient. Patient delayed while system comes back online.<br>Patient reverts to CT pathway <br> patient delays                                                                                                                              | DicomServer computer turns off/has fault.                                                                                                                     |                                                                                                                                                                                                                                                                              | Minor            | Low                | 1            |                                                                                                                                                                                                                                                                                                                                                                      | Low              | 1                 |                                                                                                                                                     |

### References

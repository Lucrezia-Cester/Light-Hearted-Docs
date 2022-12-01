risk_levels:
1. label: Low
  description: Acceptable
2. label: Medium
  description: Investigate further risk reduction
3. label: High
  description: Unacceptable
risk_probability_levels:
1. label: Low
  description: Unlikely
2. label: Medium
  description: Somewhat likely
3. label: High
  description: Likely
risk_severity_levels:
1. label: Negligible
  description: Inconvenience or temporary discomfort
2. label: Minor
  description: Results in temporary injury or impairment not requiring professional medical intervention
3. label: Serious
  description: Results in injury or impairment requiring professional medical intervention
4. label: Critical
  description: Results in permanent impairment or life-threatening injury
5. label: Catastrophic
  description: Results in patient death
risk_acceptability_matrix:
    1.[Low, Low, Low, Low, Low]
    2.[Low, Low, Low, Low, Medium]
    3.[Low, Low, Low, Medium, Medium]
    4.[Low, Low, Medium, Medium, High]
    5.[Low, Medium, Medium, High, High]
risks:
      1.hazard_id : SYNCT-HZ-001
      hazard_description : Incorrect Hounsfield units assigned to tissues
      potential_clinical_impact : Incorrect dose distribution calculated, leading to mistreatment (incorrect treatment such as over irradiation of OARs and poor coverage of target) or patient delays. Patient reverts to CT pathway -> Patient delays
      possible_causes : NN unable to process unfamiliar data.  Patient anatomy not representative of training data. Patient scanned with incorrect orientation (non-HFS)
      existing_controls : Checking and treatment planning to check HU values Thresholding tools on eclipse Diamond check > forces patient to water, checks dose distribution within tolerance
      initial_severity : Major
      initial_likelihood: Low
      initial_risk : 3
      design_controls: Mean HU value Histogram analysis of HU Acceptable range -1000HU to 2000HU  Comparing Volumes between CT and MRIs  Geometric scaling check > threshold on CT and MR > Mean distance to agreement, DICE, Volume check.
      final_likelihood: Very Low
      final_risk: 2

      2.hazard_id : SYNCT-HZ-002
      hazard_description : Wrong series/study sent
      potential_clinical_impact : Incorrect HU values assigned to tissues, gives incorrect dose distribution -> mistreatment or patient delays.  No SynCT generated for patient.  Correct series to be resent -> Slight delay in pathway.  Re-imaging of patient -> longer delay in pathway
      possible_causes : Poor / lack of training
      existing_controls : Work instruction for radiographers.  Written instruction at end of MR protocol.
      initial_severity : Minor
      initial_likelihood: Low
      initial_risk : 1
      design_controls: is_valid_function, Check to confirm Series name, Scanner, modality
      final_likelihood: Very Low
      final_risk: 1

      3.hazard_id : SYNCT-HZ-003
      hazard_description : Incorrect Protocol used for MRI imaging
      potential_clinical_impact : No SynCT generated for patient Re-imaging of patient, delays in patient pathway.
      possible_causes : Poor / lack of training Protocol not available. Clinician error on request form MRI vetting team book onto wrong MR scanner.
      existing_controls : Work Instruction for radiographer.  Work instruction for clinicians for EPR referral. Availability of protocol on MR console.
      initial_severity : Minor
      initial_likelihood: Very low
      initial_risk : 1
      design_controls:
      final_likelihood: Very Low
      final_risk: 1

      4.hazard_id : SYNCT-HZ-004
      hazard_description : Acquisition protocol parameters changed or alternative coil used on MR. Causes change in geometric distortion, signal intensity, scanned anatomy, FOV, missing tissue.
      potential_clinical_impact : Incorrect HU values assigned to tissues, gives incorrect dose distribution -> mistreatment or patient delays.  Geometric distortion affects dose distribution -> mistreatment or patient delays.
      possible_causes : Optimisation of parameter by MR radiographer.  Changes to protocol during update removal of protocol during update
      existing_controls : Protocol is locked between patients but can be tweeked when scanning.  RT staff present on scanner.  Written instruction to provide limits on each parameter in protocol.
      initial_severity : Considerable
      initial_likelihood: Medium
      initial_risk : 3
      design_controls: is_valid_function, Check to confirm scanning parameters within tolerance (e.g. bandwidth, TE, TR, distortion correction ON). Store backup of MRI scan protocol on GitHub alongside model. Adding noise to training data.
      final_likelihood: Very Low
      final_risk: 2

      5.hazard_id : SYNCT-HZ-005
      hazard_description : Wrong HU as a result of artefact from prosthetic
      potential_clinical_impact : Causes incorrect HU values, incorrect dose distribution -> mistreatment or patient delays.  Causes geometric distortion of image significant enough to affect dose distribution -> mistreatment or patient delays.  Patient reverts to CT pathway -> patient delays
      possible_causes : Trained model causes HU incorrect estimation of tissue within artefact region, differing from water > +-50HU.
      existing_controls : Allow single prosthetic hip planning work instruction to avoid hip implant Fiducials are not a concern  SPACE-OAR affects MR contrast? Electron desity is water equivalent - get more info on this.  Planning to contour and force HU before Treatment planning.
      initial_severity : Considerable
      initial_likelihood: Low
      initial_risk : 2
      design_controls:
      final_likelihood: Very Low
      final_risk: 2

      6.hazard_id : SYNCT-HZ-007
      hazard_description : Unintended patient imaged with protocol. Synthetic CT generated when not required.
      potential_clinical_impact :  Planner misinterprets synthetic CT as true CT and treatment planning using MR-only planning pathway when not intended.  Correct scan needs to be booked -> delays in patient treatment
      possible_causes : Clinician error on request form MRI vetting team error in EPR interpretation.
      existing_controls : MR-only pathway SOP document defining eligibility, pre-requisites (clinician's EPR request for MR-only prostate, no nodal involvement, ...)
      initial_severity : Minor
      initial_likelihood: Very Low
      initial_risk : 1
      design_controls:
      final_likelihood: Very Low
      final_risk: 1

      7.hazard_id : SYNCT-HZ-008
      hazard_description : Wrong patient orientation causes miscalculation of HU in Inference
      potential_clinical_impact : Incorrect HU generated -> mistreatment or re-imaging of patient, delays in patient pathway.
      possible_causes : Poor / lack of training
      existing_controls : Work instructions to ensure patients are scanned HFS.
      initial_severity : Significant
      initial_likelihood: Very low
      initial_risk : 1
      design_controls: Check in predicate for is_valid_function is HeadFirstSupine
      final_likelihood: Very low
      final_risk: 1

      8.hazard_id : SYNCT-HZ-009
      hazard_description : Connection between MR and Dicomserver goes down
      potential_clinical_impact : No SynCT generated for patient. Patient delayed while system comes back online. Patient reverts to CT pathway -> patient delays
      possible_causes : DicomServer computer turns off/has fault. MRI machine system update by engineers
      existing_controls :
      initial_severity : Minor
      initial_likelihood: Low
      initial_risk : 1
      design_controls: Ability to send images from Eclipse or PACS to Dicomserver
      final_likelihood: Very low
      final_risk: 1

      9.hazard_id : SYNCT-HZ-010
      hazard_description : Docker container is lost/overridden/corrupted,
      potential_clinical_impact : No SynCT generated for patient. Patient delayed while system comes back online. Patient reverts to CT pathway -> patient delays
      possible_causes : DicomServer computer turns off/has fault.
      existing_controls :
      initial_severity : Minor
      initial_likelihood: Low
      initial_risk : 1
      design_controls: Restore Docker from GitHub.
      final_likelihood: Very low
      final_risk: 1

      10.hazard_id : SYNCT-HZ-011
      hazard_description : DicomServer goes down / becomes unavailable
      potential_clinical_impact : No SynCT generated for patient. Patient delayed while system comes back online. Patient reverts to CT pathway -> patient delays
      possible_causes : DicomServer computer turns off/has fault.
      existing_controls :
      initial_severity : Minor
      initial_likelihood: Low
      initial_risk : 1
      design_controls:
      final_likelihood: Low
      final_risk: 1

# Hazard-Log
## risk levels:
1. label: Low
  description: Acceptable
2. label: Medium
  description: Investigate further risk reduction
3. label: High
  description: Unacceptable
  
 ## risk probability levels:
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
## risk acceptability matrix:
    1.[Low, Low, Low, Low, Low]
    2.[Low, Low, Low, Low, Medium]
    3.[Low, Low, Low, Medium, Medium]
    4.[Low, Low, Medium, Medium, High]
    5.[Low, Medium, Medium, High, High]
## risks:
      1. hazard_id : LH-001
      hazard_description : Laser pointed in patient's eye
      potential_clinical_impact : Patient's eye is damaged.
      possible_causes : Device is not used according to manual specifications. The device, through the handle is pointed incorrectly to the wrong body part.
      existing_controls : Patient should wear laser protective goggles. The device handle should be handled with care to point the laser in the correct direction.
      initial_severity : Medium
      initial_likelihood: Medium
      initial_risk : 3
      design_controls: Laser Goggles. Device Handle. Device tripod which stabilises the device.
      final_likelihood: Very Low
      final_risk: 2

      

      

      

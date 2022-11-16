---
documentid: Light-Hearted-v0.1
version: 0.1

---

# Software and Hardware Design Specification 


|             |                   |
|-------------|-------------------|
| Author      | Lucrezia Cester   |
|             |                   |


# Purpose and Scope.
This document contains the design specification for the hardware and software of the Light-Hearted device. It will describe what the light-hearted device is supposed to do.


### Scope
This document applies to Light-Hearted release v.1.0.

# Roles and Responsibilities 

| Role             | Responsibility                               |
|------------------|----------------------------------------------|
| Development lead | To create the design specifications to match |
| Clinical lead    | To provide clinical advice on the specificaitons of the device    |


# Acronyms

| Item | Definition                                                                   |
|------|------------------------------------------------------------------------------|
| ML   | Machine Learning                                                             |
| AI   | Artificial Intelligence                                                      | 
| AS   | Aortic Stenosis                                                              | 
| CVDs | Cardiovascular Diseases                                                      | 
| HSs  | Heart Sounds                                                                 | 
| UI   | User Interface                                                               | 


The following stakeholders contributed to the requirements gathering process. 

| Name               | Role                         |
|--------------------|------------------------------|
| Lucrezia cester    | Development Lead             |
| Thomas Keeble.     | Clinical Lead                |


### Introduction

Cardiovascular diseases are the leading cause of death worldwide. The NHS long-term plan states that CVDs are a preventable if detected eearly and outlines the need to save 100,000 deaths by these diseases by 2025.
Aortic Stenosis is one example of CVDs. This disease is usually diagnosed through heart ultrasound, but the waiting list for this exam is very long, it requires a clinical expert and 50% of the patients that undertake this exam end up having a normal exam. 
Therefore we propose a method to gatekeep heart ultrasound exams and pick up asymptomatic AS patients so that we can screen out normal patients from having heart ultrasound and also pick up asymptomatic patients to start treaatment early and focus on prevention.

In order to fullfil the vision for this device, it first needs to undergo a clinical trial. It was already bench-mark tested.

The device as it stands can acquire cardiovascular sounds and provide the same kind of data (albeit more precise, given its ability to get the high frequency ranges of the HSs) that a stethoscope can. However the purpose of the trial will be the acquire data from patients with AS. The dataset 
will allow to train an AI algorithm (that was already bench-tested). Thus the end product will be an AI-powered non-contacless remote heart monitoring device that can be used automatically in the GP practice to be focus where healthcare should head towards: prevention.

### Users

#### (when the device will be finished and tested) GP practices 
- The primary users will patients in GPs practices. A disproportionate amount of money is used to cure patients that are already sick and not enough money is spent on prevention and GP practices, which see the vast majority of the population. 
By having this remote monitoring contact-less and automatic CVD diagnostic device in the GP practice, patients will be able to check in just a few seconds whether they have AS or not and check its progressions everytime they see their GP, sparing them an expert visit to the cardiologist.

#### Cardiologists (during the clinical trial)
- The trial will take place in the cardiology clinic and tested on patients with AS.

### Use Environments

#### (when the device will be finished and tested) GP waiting room 
- The device will be placed in a booth in the GP waiting room and 

#### Cardiologists' clinics (during the clinical trial)
- The device will be used on AS patients in the cardiologists' clinic. The device will be composed of a small box, which will be connected to a personal computer. The device will be placed in the 
cardiologist's clinic. The tripod on which it stands can be regulated to adjust to the height of the patient. The device will be connected to a computer. The cardiologist will have simple UI on the computer where they will need to press a button to start the acquisition. The UI will advert the cardiologist when 
the acquisition has ended.
The device will be kept in the cardiologist' clinic.

### Use Cases 

#### Use Case During the Clinical Trial (normal device functioning)
Data will be acquired from patients with AS as they undergo their normal visit at the Cardiologist. The patient will be sitting down and breathe normally while the device will be pointed at their neck for a few seconds. 
The patient won't feel any burn on their skin during or after the dtaa taking process. 
The cardiologist will start the device by switching a button on the device's back The cardiologist will have the device's software on a nerby computer. The cardiologist will press the start button on the 
device's complimentary software. The device will start acquisition and then the UI of the software will announce to the cardiologist when the acquisition is finished. This will take seconds. The cardiologist will then switch off the device 
with the switch at the back. 
The data will then be analysed by the complimentary software and the heart sounds of the patient will be displayed on the UI. 
The data will then be used to train a ML model.

#### Use Case During the Clinical Trial (faulty device functioning)
A faulty use of the device might occur because of the following reasons:
- The cardiologist points the device in the eye of the patient for a prolonged period of time instead than pointing it at the patient's neck as outlined in the device instructions.
- The cardiologist forgets to switch on the device thus no data is acquired. 
- The cardiologist forgets to switch on the software and press the start button thus no data is acquired.
- The cardiologist forgets to switch off the device in between acquisition thus the device overheats and there is a laser on.

### Considerations

The following list of considerations Has been compiled from relevant suggestions from ISO 13485, BSI 62304 and BSI 62366:

- input data format to be processed.
- output format of the application
- destination of the output data
- the expected application/service uptime 
- the workload e.g. number of CTs per week.
- maximum acceptable turnaround time
- number and frequency of users to be supported
- user access 
- platform for delivery
- past complaints, failure reports, adverse events of similar products
- usability and maintenance
- security controls
- workflow integration
- local population demographics, to be reflected in training data.
- minimum sensitivity, specificity, true/false positive/negative rates.
- turnaround time for inference
- expected frequency of retraining.
- training data bias to acknowledge
- quality objectives for the project - e.g. quality metrics, ranges and thresholds
- contents of surveillance plan including metric to monitor once the application is deployed
- applicable regulatory requirements
- training requirements, such as workshops, training, documents etc.
- safety considerations for patients and staff
- information derived from similar/previous designs
- functional and capability requirements
- interfaces between systems
- software driven alarms, warnings and operator messages
- security requirements
- data definitions and database requirements
- installation and acceptance requirements of the delivered software at operation and maintenance site (* although this 
is GSTT only for projects built under this QMS)
- requirements related to methods of operation and maintenance
- requirements of IT network, Trust IT integration
- user maintenance requirements
- software update requirements

### User requirements

| Reference | Requirement title                                                                                           | Requirements Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                                                                           
|-----------|-------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SRS-001   | Shall be safe for use on patients                                                                           | The device should be built in a manner that ensures safety of the patients during and after treatment.                                                                                                                                                                                                                                                                                           | 
| SRS-002   | Shall be easy to use                                                                                        | The device should be built in a manner such that the cardiologist will just need to press a button and the device will do the rest, focusing on ease of usability for the patient and comfort for the user.                                                                                                                                                                                                                                                                                                                                                       |
| SRS-003   | Shall acquire CVDs sounds from patients                                                                     | The device should be able to acquire CVDs sounds.                                                                                                                                                                                                                                                                 |

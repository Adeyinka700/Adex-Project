
# Adex Project
**Omolara oni anger issue**
### Cry no more our baby will join us soon
1. First tutorial class
* Adekoya Omolara now Adebowale Omolara
  ---
  ```SELECT
"APIN" AS "IP",
(SELECT `state_province`  FROM  `location` WHERE `location_id` = 8 LIMIT 1) AS State,
(SELECT `city_village`  FROM  `location` WHERE `location_id` = 8 LIMIT 1) LGA,
(SELECT `address1`  FROM  `location` WHERE `location_id` = 8 LIMIT 1) Datim_Code,
(SELECT `name`  FROM  `location` WHERE `location_id` = 8 LIMIT 1) FacilityName,
pid2.identifier AS `PepID`,
pid3.identifier AS `HospitalID`,
IFNULL(pid1.identifier,MAX(IF(obs.concept_id=165567,obs.value_text, NULL))) AS `ANCID`,
person.gender AS Gender,
DATE_FORMAT(person.birthdate,'%d/%m/%Y') AS DOB,
DATE_FORMAT(enc.encounter_datetime,'%d/%m/%Y')  AS EnrollmentDate,
MAX(IF(obs.concept_id=1427,DATE_FORMAT(obs.value_datetime,'%d/%m/%Y'), NULL)) AS `LastMenstralPeriod`,
MAX(IF(obs.concept_id=1438,obs.value_numeric, NULL)) AS `GestationalAge(in Weeks)`,
MAX(IF(obs.concept_id=5596,DATE_FORMAT(obs.value_datetime,'%d/%m/%Y'), NULL)) AS `ExpectedDeliveryDate`,
MAX(IF(obs.concept_id=5624,obs.value_numeric, NULL)) AS `Gravidity`,
MIN(IF(obs.concept_id=1053,obs.value_numeric, NULL)) AS `Parity`,
MAX(IF(obs.concept_id=1053,obs.value_numeric, NULL)) AS `Number Alive`,
MAX(IF(obs.concept_id=164894,obs.value_numeric, NULL)) AS `Losses`,
MAX(IF(enc.form_id=54 AND obs.concept_id= 159427,cn1.name, NULL)) AS `ResultOfHIVTest`
   FROM obs
LEFT JOIN patient ON(patient.patient_id=obs.person_id AND obs.voided=0 AND patient.voided=0)
LEFT JOIN person ON(person.person_id=patient.patient_id AND person.voided=0)
LEFT JOIN encounter enc ON(enc.encounter_id=obs.encounter_id AND enc.voided=0 AND obs.voided=0 AND enc.form_id IN (16,54,15,40,45))
LEFT JOIN visit ON (enc.visit_id=visit.visit_id AND visit.voided=0)
LEFT JOIN concept_name cn1 ON(obs.value_coded=cn1.concept_id AND cn1.locale='en' AND cn1.locale_preferred=1)
LEFT JOIN patient_identifier pid1 ON(pid1.patient_id=patient.patient_id AND patient.voided=0 AND pid1.identifier_type=6 AND pid1.voided=0)
LEFT JOIN patient_identifier pid2 ON(pid2.patient_id=patient.patient_id AND patient.voided=0 AND pid2.identifier_type=4 AND pid2.voided=0)
LEFT JOIN patient_identifier pid3 ON(pid3.patient_id=patient.patient_id AND patient.voided=0 AND pid3.identifier_type=5 AND pid3.voided=0)
WHERE patient.voided=0 AND enc.voided=0 GROUP BY patient.patient_id;```

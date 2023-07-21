# ChatGPTVoiceSemanticSearchDocuments
ChatGPT AI Pipeline featuring voice input with Whisper, vector database embeddings with FAISS, and ChatGPT Document AI

## Demonstration:

### AI Pipeline Demo Space:  https://huggingface.co/spaces/awacke1/ChatGPT-Memory-Chat-Story-Generator

1. ChatGPT using Voice input - OpenAI GPT ChatCompletion Service and Whisper Text to Speech Service
2. ChatGPT embeddings and vector database with Facebook AI Semantic Search using ada embeddings, FAISS, and streamlit for PDF uploads.
3. Multi-Section inference allowing system and agent prompts to interact with 12 to 80 pages depending on model capability.

### Prompt Engineering:

Create three robust HL7 examples with the same data just in three versions: 1) An HL7 v.2.x ADT and corresponding ORU for emergency admit PV1 with coverage of "Demo Payer Policy Name" for Patient "Aaron Wacker" from Mound,MN with several conditions and ICD10 codes for sundowning, abdominal pain, head injury due to fall trauma, comorbidities include asthma, skin cancer, and allergies to aspirin, mold, cats and dogs.  Medications administered were ambulatory with heart monitoring.  Patient is seeing Dr Sunny California of the Center of Syncope hospital.  2) An HL7 v.3 CCDA xml file example with same patient information and admit.  3) An HL7 v4 FHIR example that shows the data fields hydrated for these FHIR objects:  Patient, Coverage, Conditions, Service Requests, Procedures, Medications, Organization, Allergies, Encounters, and Provider and Hospital details.


# HL7 v.2.x ADT and corresponding ORU:

## ADT in HL7 version 2.x ADT and ORU Format:

### ADT:
```
MSH|^~\&|CenterOfSyncopeHosp|COSH|||202307210800||ADT^A01|0001|P|2.6
EVN||202307210800
PID|||1234^^^COSH||WACKER^AARON||19800101|M|||123 MAIN ST^^MOUND^MN^55111||1234567890||ENGLISH|M|OTHER||1234567890|||NOT HISPANIC OR LATINO
PV1||E|COSH^^^ER^301|1|||123456^CALIFORNIA^SUNNY^^DR^MD^^^NPI|||EMERGENCY ADMIT||1234
IN1|1|1234|Demo Payer Policy Name|||||||||WACKER^AARON
DG1|1|ICD10|F01.51|Sundowning||A
DG1|2|ICD10|R10.9|Abdominal pain||A
DG1|3|ICD10|S06.0X0|Head injury due to fall trauma||A
DG1|4|ICD10|J45.909|Asthma||H
DG1|5|ICD10|C44.9|Skin cancer||H
AL1|1||ASPIRIN
AL1|2||MOLD
AL1|3||CATS
AL1|4||DOGS
```

### ORU:
```
MSH|^~\&|CenterOfSyncopeHosp|COSH|||202307210800||ORU^R01|0002|P|2.6
PID|||1234^^^COSH||WACKER^AARON||19800101|M|||123 MAIN ST^^MOUND^MN^55111||1234567890||ENGLISH|M|OTHER||1234567890|||NOT HISPANIC OR LATINO
ORC|RE|123456^COSH|123456^COSH
OBR|1|123456^COSH|123456^COSH|PROC^Procedure|P|||202307210800||||||||123456^CALIFORNIA^SUNNY^^DR^MD^^^NPI||||||||P||||||AMBULATORY WITH HEART MONITORING||||F
```

# HL7 v.3 CCDA xml file:

## ADT in HL7 version 3.x CCD Format:
```
<ClinicalDocument xmlns="urn:hl7-org:v3">
    <!-- Header Elements -->
    <realmCode code="US"/>
    <id root="1234" extension="5678"/>
    <code code="34133-9" displayName="Summarization of Episode Note"/>
    <title>Emergency Admit for Aaron Wacker</title>
    <effectiveTime value="202307210800"/>
    <confidentialityCode code="N"/>
    <languageCode code="en-US"/>
    <!-- Patient and Encounter Details -->
    <recordTarget>
        <patientRole>
            <id root="2.16.840.1.113883.19.5" extension="1234"/>
            <addr use="HP">
                <streetAddressLine>123 Main St</streetAddressLine>
                <city>Mound</city>
                <state>MN</state>
                <postalCode>55111</postalCode>
                <country>USA</country>
            </addr>
            <patient>
                <name>
                    <given>Aaron</given>
                    <family>Wacker</family>
                </name>
                <administrativeGenderCode code="M"/>
                <birthTime value="19800101"/>
            </patient>
            <providerOrganization>
                <id root="2.16.840.1.113883.19.5"/>
                <name>Center of Syncope hospital</name>
                <telecom value="tel:+11234567890"/>
                <assignedPerson>
                    <name>Dr. Sunny California</name>
                </assignedPerson>
            </providerOrganization>
        </patientRole>
    </recordTarget>
    <!-- Conditions -->
    <component>
        <section>
            <templateId root="2.16.840.1.113883.10.20.22.2.5.1"/>
            <code code="11450-4" displayName="Problem list"/>
            <entry>
                <act classCode="ACT" moodCode="EVN">
                    <code code="282291009" displayName="Diagnosis"/>
                    <statusCode code="completed"/>
                    <entryRelationship typeCode="SUBJ">
                        <observation classCode="OBS" moodCode="EVN">
                            <code code="409586006" displayName="Comorbidity">
                                <value code="F01.51" displayName="Sundowning"/>
                                <value code="R10.9" displayName="Abdominal pain"/>
                                <value code="S06.0X0" displayName="Head injury due to fall trauma"/>
                                <value code="J45.909" displayName="Asthma"/>
                                <value code="C44.9" displayName="Skin cancer"/>
                            </code>
                        </observation>
                    </entryRelationship>
                </act>
            </entry>
        </section>
    </component>
    <!-- Allergies -->
    <component>
        <section>
            <templateId root="2.16.840.1.113883.10.20.22.2.6.1"/>
            <code code="48765-2" displayName="Allergies"/>
            <entry>
                <act classCode="ACT" moodCode="EVN">
                    <code code="ASSERTION"/>
                    <statusCode code="completed"/>
                    <entryRelationship typeCode="SUBJ">
                        <observation classCode="OBS" moodCode="EVN">
                            <value code="ASPIRIN"/>
                            <value code="MOLD"/>
                            <value code="CATS"/>
                            <value code="DOGS"/>
                        </observation>
                    </entryRelationship>
                </act>
            </entry>
        </section>
    </component>
</ClinicalDocument>
```


## HL7 v4 FHIR example in JSON format:

### Patient

```
{
  "resourceType": "Patient",
  "id": "1234",
  "text": {
    "status": "generated",
    "div": "<div xmlns=\"http://www.w3.org/1999/xhtml\">Aaron Wacker</div>"
  },
  "name": [
    {
      "family": "Wacker",
      "given": ["Aaron"]
    }
  ],
  "gender": "male",
  "birthDate": "1980-01-01",
  "address": [
    {
      "line": ["123 Main St"],
      "city": "Mound",
      "state": "MN",
      "postalCode": "55111"
    }
  ]
}
```

### Condition
```
{
  "resourceType": "Condition",
  "id": "cond1",
  "subject": {
    "reference": "Patient/1234"
  },
  "code": {
    "coding": [
      {
        "system": "http://hl7.org/fhir/sid/icd-10",
        "code": "F01.51",
        "display": "Sundowning"
      }
    ]
  }
}
```

### Allergy Intolerance
```
{
  "resourceType": "AllergyIntolerance",
  "id": "all1",
  "patient": {
    "reference": "Patient/1234"
  },
  "substance": {
    "coding": [
      {
        "system": "http://snomed.info/sct",
        "code": "419263009",
        "display": "Allergy to mold"
      }
    ]
  }
}
```

# Exploration of service request for authorization.

## Python code:
```
import hl7

# HL7 v2.x ADT message
adt_message = """
MSH|^~\&|CenterOfSyncopeHosp|COSH|||202307210800||ADT^A01|0001|P|2.6
EVN||202307210800
PID|||1234^^^COSH||WACKER^AARON||19800101|M|||123 MAIN ST^^MOUND^MN^55111||1234567890||ENGLISH|M|OTHER||1234567890|||NOT HISPANIC OR LATINO
PV1||E|COSH^^^ER^301|1|||123456^CALIFORNIA^SUNNY^^DR^MD^^^NPI|||EMERGENCY ADMIT||1234
IN1|1|1234|Demo Payer Policy Name|||||||||WACKER^AARON
DG1|1|ICD10|F01.51|Sundowning||A
DG1|2|ICD10|R10.9|Abdominal pain||A
DG1|3|ICD10|S06.0X0|Head injury due to fall trauma||A
DG1|4|ICD10|J45.909|Asthma||H
DG1|5|ICD10|C44.9|Skin cancer||H
AL1|1||ASPIRIN
AL1|2||MOLD
AL1|3||CATS
AL1|4||DOGS
"""

adt_hl7 = hl7.parse(adt_message)

# HL7 v2.x ORU message
oru_message = """
MSH|^~\&|CenterOfSyncopeHosp|COSH|||202307210800||ORU^R01|0002|P|2.6
PID|||1234^^^COSH||WACKER^AARON||19800101|M|||123 MAIN ST^^MOUND^MN^55111||1234567890||ENGLISH|M|OTHER||1234567890|||NOT HISPANIC OR LATINO
ORC|RE|123456^COSH|123456^COSH
OBR|1|123456^COSH|123456^COSH|PROC^Procedure|P|||202307210800||||||||123456^CALIFORNIA^SUNNY^^DR^MD^^^NPI||||||||P||||||AMBULATORY WITH HEART MONITORING||||F
"""

oru_hl7 = hl7.parse(oru_message)
```


## Python code - v3 CCDA:
```
import xml.etree.ElementTree as ET

ccda_message = """
<ClinicalDocument xmlns="urn:hl7-org:v3">
    <!-- Header Elements -->
    <realmCode code="US"/>
    <id root="1234" extension="5678"/>
    <code code="34133-9" displayName="Summarization of Episode Note"/>
    <title>Emergency Admit for Aaron Wacker</title>
    <effectiveTime value="202307210800"/>
    <confidentialityCode code="N"/>
    <languageCode code="en-US"/>
    <!-- Patient and Encounter Details -->
    <recordTarget>
        <patientRole>
            <id root="2.16.840.1.113883.19.5" extension="1234"/>
            <addr use="HP">
                <streetAddressLine>123 Main St</streetAddressLine>
                <city>Mound</city>
                <state>MN</state>
                <postalCode>55111</postalCode>
                <country>USA</country>
            </addr>
            <patient>
                <name>
                    <given>Aaron</given>
                    <family>Wacker</family>
                </name>
                <administrativeGenderCode code="M"/>
                <birthTime value="19800101"/>
            </patient>
            <providerOrganization>
                <id root="2.16.840.1.113883.19.5"/>
                <name>Center of Syncope hospital</name>
                <telecom value="tel:+11234567890"/>
                <assignedPerson>
                    <name>Dr. Sunny California</name>
                </assignedPerson>
            </providerOrganization>
        </patientRole>
    </recordTarget>
    <!-- Conditions -->
    <component>
        <section>
            <templateId root="2.16.840.1.113883.10.20.22.2.5.1"/>
            <code code="11450-4" displayName="Problem list"/>
            <entry>
                <act classCode="ACT" moodCode="EVN">
                    <code code="282291009" displayName="Diagnosis"/>
                    <statusCode code="completed"/>
                    <entryRelationship typeCode="SUBJ">
                        <observation classCode="OBS" moodCode="EVN">
                            <code code="409586006" displayName="Comorbidity">
                                <value code="F01.51" displayName="Sundowning"/>
                                <value code="R10.9" displayName="Abdominal pain"/>
                                <value code="S06.0X0" displayName="Head injury due to fall trauma"/>
                                <value code="J45.909" displayName="Asthma"/>
                                <value code="C44.9" displayName="Skin cancer"/>
                            </code>
                        </observation>
                    </entryRelationship>
                </act>
            </entry>
        </section>
    </component>
    <!-- Allergies -->
    <component>
        <section>
            <templateId root="2.16.840.1.113883.10.20.22.2.6.1"/>
            <code code="48765-2" displayName="Allergies"/>
            <entry>
                <act classCode="ACT" moodCode="EVN">
                    <code code="ASSERTION"/>
                    <statusCode code="completed"/>
                    <entryRelationship typeCode="SUBJ">
                        <observation classCode="OBS" moodCode="EVN">
                            <value code="ASPI
....
```

# Markdown generation creates formatted output for documentation.

|Example Type|Summary|Emoji| 
|---|---|---| 
|HL7 v.2.x ADT and ORU|Emergency admit for Patient "Aaron Wacker" with multiple conditions, comorbidities, and allergies. Medications administered. Seen by Dr. Sunny California.|🚑| 
|HL7 v.3 CCDA|Emergency admit for Patient "Aaron Wacker" with provider and hospital details. Includes problem list and allergies.|📝| 
|HL7 v4 FHIR|Hydrated data fields for Patient, Coverage, Conditions, Service Requests, Procedures, Medications, Organization, Allergies, Encounters, and Provider and Hospital details.|💡|

# ChatGPT Code Interpreter Demo: Create 10 Visualizations for the ADT data
## Given the nature of the data you described, here are some visualizations that could be generated:
1. Bar Plot of Conditions: Given the ICD10 codes for sundowning, abdominal pain, and head injury due to fall trauma, a bar plot could be created to visualize the count of each condition in the dataset.
2. Pie Chart of Comorbidities: Given the comorbidities of asthma and skin cancer, a pie chart could be created to show the proportion of each comorbidity.
3. Bar Plot of Allergies: Given the allergies to aspirin, mold, cats, and dogs, a bar plot could be created to visualize the count of each allergy in the dataset.
4. Heatmap of Conditions vs Allergies: A heatmap could be created to show the co-occurrence of conditions and allergies. The x-axis would represent conditions, the y-axis would represent allergies, and the color intensity would represent the count of co-occurrences.
5. Time Series Plot of Admissions: If the date and time of each admission is available, a time series plot could be created to visualize the number of admissions over time.
6. Box Plot of Admissions by Doctor: If the doctor for each admission is known, a box plot could be created to visualize the distribution of admissions by each doctor.
7. Count Plot of Medications Administered: If the medications administered for each admission are known, a count plot could be created to visualize the count of each medication.
8. Bar Plot of Encounters by Service Requested: If the service requested for each encounter is known, a bar plot could be created to visualize the count of encounters by service requested.
9. Pie Chart of Procedures Performed: If the procedures performed for each admission are known, a pie chart could be created to show the proportion of each procedure.
10. Count Plot of Coverage: If the coverage for each patient is known, a count plot could be created to visualize the count of each type of coverage.

## Prompt Engineering:  For the visualizations just show these basic graphs with the limited data in the example.  Make up information needed by the visualization and make sure to include the terms or words to do more a visualization of the language itself.

![image](https://github.com/AaronCWacker/ChatGPTVoiceSemanticSearchDocuments/assets/30595158/7e2549bf-c2c2-44f3-968f-7f2374ea16a1)
![image](https://github.com/AaronCWacker/ChatGPTVoiceSemanticSearchDocuments/assets/30595158/3e6c455f-75fe-428b-b1df-153fd0bb0347)
![image](https://github.com/AaronCWacker/ChatGPTVoiceSemanticSearchDocuments/assets/30595158/ba6c0abd-b586-4343-afd0-23b824f085a6)
![image](https://github.com/AaronCWacker/ChatGPTVoiceSemanticSearchDocuments/assets/30595158/12d39f5f-de67-4e6b-877c-7cfd5b7d0257)

### Conditions: The bar chart visualizes the count of each condition. It shows that 'Abdominal pain' is the most common condition, followed by 'Sundowning' and 'Head injury'.
### Comorbidities: The bar chart visualizes the count of each comorbidity. It shows that 'Asthma' is more common than 'Skin cancer'.
### Allergies: The bar chart visualizes the count of each allergy. It shows that 'Mold' is the most common allergy, followed by 'Dogs', 'Cats', and 'Aspirin'.
### Comorbidities (Pie Chart): The pie chart visualizes the proportion of each comorbidity. It shows that 'Asthma' accounts for a larger proportion of the comorbidities than 'Skin cancer'.




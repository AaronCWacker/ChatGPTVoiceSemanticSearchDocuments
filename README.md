# ChatGPTVoiceSemanticSearchDocuments
ChatGPT AI Pipeline featuring voice input with Whisper, vector database embeddings with FAISS, and ChatGPT Document AI

Demonstration:

Demo space:  https://huggingface.co/spaces/awacke1/ChatGPT-Memory-Chat-Story-Generator

1) ChatGPT using Voice input - OpenAI GPT ChatCompletion Service and Whisper Text to Speech Service
2) ChatGPT embeddings and vector database with Facebook AI Semantic Search using ada embeddings, FAISS, and streamlit for PDF uploads.
3) Multi-Section inference allowing system and agent prompts to interact with 12 to 80 pages depending on model capability.


# Sample prompt:

Create three robust HL7 examples with the same data just in three versions: 1) An HL7 v.2.x ADT and corresponding ORU for emergency admit PV1 with coverage of "Demo Payer Policy Name" for Patient "Aaron Wacker" from Mound,MN with several conditions and ICD10 codes for sundowning, abdominal pain, head injury due to fall trauma, comorbidities include asthma, skin cancer, and allergies to aspirin, mold, cats and dogs.  Medications administered were ambulatory with heart monitoring.  Patient is seeing Dr Sunny California of the Center of Syncope hospital.  2) An HL7 v.3 CCDA xml file example with same patient information and admit.  3) An HL7 v4 FHIR example that shows the data fields hydrated for these FHIR objects:  Patient, Coverage, Conditions, Service Requests, Procedures, Medications, Organization, Allergies, Encounters, and Provider and Hospital details.


# CDS-Hook: patient-view

## Pre-fetch

    "context":{
      "userId" : "Practitioner/123",
      "patientId" : "1288992"
    }
 
## What is in the Patient record?
 
The CDS-Hooks app will receive the patientId. 

## Prefetch

    "prefetch": {
      "healthPlanMember": "Patient/{{context.patientId}}"
    }



# appointmentresponse-create

A hook is required on appointmentResponse create.

This enables a practitioner to request information from the payer about the
patient. The practitioner may require information about the patient in order
to prepare for an appointment in advance.

## Service Definition

    {
      "services": [
        {
          "hook": "member-view",
          "title": "Advance request for Member Information",
          "description": "A CDS Service that returns patient information from a health plan",
          "id": "patient-information-request",
          "prefetch": {
            "planMember": "Patient/{{context.patientId}}"
          }
        }
      ]
    }

## Calling the Hook

The CDS Hooks call to the service looks like this example:

    {
       "hookInstance" : "d1577c69-dfbe-44ad-ba6d-3e05e953b2ea",
       "fhirServer" : "http://hooks.smarthealthit.org:9080",
       "hook" : "member-view",
       "fhirAuthorization" : {
         "access_token" : "some-opaque-fhir-access-token",
         "token_type" : "Bearer",
         "expires_in" : 300,
         "scope" : "patient/Patient.read patient/Coverage.read",
         "subject" : "cds-service1"
       },
       "context" : {
           "userId" : "Practitioner/example",
           "patientId" : "1288992",
           "coverageId" : "89284"
       },
       "prefetch" : {
          "planMember" : {
             "resourceType" : "Patient",
             "gender" : "male",
             "birthDate" : "1925-12-23",
             "id" : "1288992",
             "active" : true
             "identifier": [
                {
                    "id": "1",
                    "use": "usual",
                    "type": "XV",
                    "system": "http://www.acme.com/identifiers/member",
                    "value": "89284",
                    "period": {
                        "start": "2018-01-31"
                    },
                    "assigner": "Acme Health Plan Company"
                }         
             ]
          }
       }
    }
    

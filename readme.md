Loan Application Demo Repository
================================

This repository can be cloned in Red Hat Decision Manager v7.8

*NOTE:* This repo is used in the following demo: [Red Hat Decision Manager Loan Demo](https://github.com/jbossdemocentral/rhdm7-loan-demo).

**Testing the decisions implemented with DMN:**

To test the rule execution on the kieserver:

1. Open Swagger : `http://localhost:8080/kie-server/docs`
2. In the KIE Server Swagger UI, navigate to the "DMN Assets" section and locate the POST "/server/containers/{containerId}/dmn" item.
   1. ContainerID: loan-application_1.2.0
   2. Change the "Parameter content type" and the "response content type" to "application/json"
   3. Body:
```
{ 
  "model-namespace" : "https://kiegroup.org/dmn/_C159F266-40FF-49CB-B4D9-447DFACDDC16", 
  "model-name" : "recommendation", 
  "decision-name" : [ ], 
  "decision-id" : [ ], 
  "dmn-context" : {"Credit Score": 250}
}
```
**Testing the business rules implemented with the guided decision table:**

To test the rule execution on the kieserver:

1. Open Swagger : `http://localhost:8080/kie-server/docs`
2. To send a request to the Decision Service, navigate to "KIE session assets", and search for POST "/server/containers/instances/{containerId}". 	 
   3. Insert for container **id**: `loan-application_1.2.0`
   2. Change the "Parameter content-type" and "Response content type" to "application/json";
   3. And use the following payload for **body**:
```
{
	"lookup": "default-stateless-ksession",
	"commands": [
		{
			"insert": {
				"object": {
					"com.redhat.demos.dm.loan.model.Applicant": {
						"creditScore": 120,
						"name": "Jim Whitehurst"
					}
				},
				"out-identifier": "applicant"
			}
		},
		{
			"insert": {
				"object": {
					"com.redhat.demos.dm.loan.model.Loan": {
						"amount": 2500,
						"approved": false,
						"duration": 24,
						"interestRate": 1.5
					}
				},
				"out-identifier": "loan"
			}
		},
		{
			"fire-all-rules": {}
		},
		{
			"get-objects": {
				"out-identifier": "objects"
			}
		},
		{
			"dispose": {}
		}
	]
}
```




Loan Application Demo Repository
================================

This repository can be cloned in Red Hat Decision Manager v7.0.

It's related to [Red Hat Decision Manager Loan Demo](https://github.com/jbossdemocentral/rhdm7-loan-demo)

To test the rule execution on the kieserver:

1. Open Swagger : `http://localhost:8080/kie-server/docs`
2. Select **Rule Evaluation :: BRM**
3. Insert for container **id**: `loan-application_1.1.0`
4. And use the following payload for **body**:

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

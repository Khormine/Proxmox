# OpenTestFactory:

## Quickstart:

1. Prepare a Robot Framework execution environment
2. Prepare an OpenTestFactory Orchestrator that is linked to this execution environment
3. Get the generated token
```
foo@bar:~$ docker logs orchestrator 2>&1 | grep --after-context=10 "Creating temporary JWT token"
```

4. Assign this token value to an environment variable:
```console
foo@bar:~$ export TOKEN=eyJ...
```

5. Clone your repository in a local directory:
```
foo@bar:~$ git clone https://xxx.xxx/RobotDemo.git
```
6. In this repository, create a .opentf/workflows directory.

7. Copy the YAML file in the .opentf/workflows/workflow.yaml file. You then commit your changes and then push them to your git repository.

8. To run your workflow, run the following command:
```
foo@bar:~$ curl -X POST \
  --data-binary @.opentf/workflows/workflow.yaml \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-type: application/x-yaml" \
  http://localhost:7774/workflows

{
    "apiVersion": "v1",
    "code": 201,
    "details": {
        "workflow_id": "..."
    },
    "kind": "Status",
    "message": "Workflow Robot Framework Example accepted (workflow_id=...).",
    "metadata": {},
    "reason": "Created",
    "status": "Success"
}
```

9. Check the logs of the orchestrator:
```
foo@bar:~$ curl \
  -H "Authorization: Bearer $TOKEN" \
  http://localhost:7775/workflows

{
    "apiVersion": "v1",
    "code": 200,
    "details": {
        "items": [
            "b2f27d1b-b947-4a7f-8627-5a3bdd73103e"
        ]
    },
    "kind": "Status",
    "message": "Running and recent workflows",
    "metadata": {},
    "reason": "OK",
    "status": "Success"
}
```

10. You can then query the orchestrator to get the details of specific workflow execution. In the following command, replace ... with the relevant workflow ID:
```
foo@bar:~$ curl \
  -H "Authorization: Bearer $TOKEN" \
  http://localhost:7775/workflows/.../status
```

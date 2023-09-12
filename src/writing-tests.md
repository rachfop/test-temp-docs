# Writing tests

# How to add a Testing Framework and Tests for the Workflow and Activity

**Setting up Testing Environment for your Application**

---

Follow the steps below to set up the necessary folder structure and code for testing using Temporal's Workflow environment.

Temporal’s SDKs come with a testing suite.

In the Python SDK, Temporal uses the [testing](https://python.temporal.io/temporalio.testing.html) package, where it can help set up testing environments for your Workflow or Activity.

- **[ActivityEnvironment](https://python.temporal.io/temporalio.testing.ActivityEnvironment.html)**
- **[WorkflowEnvironment](https://python.temporal.io/temporalio.testing.WorkflowEnvironment.html)**

In this section, you will focus on the `WorkflowEnviroment` package.

For the Temporal SDK in Python, [pytest](https://docs.pytest.org/) is a recommended testing framework. It offers features like environment setup/teardown fixtures, test discovery, and parameterized testing.

### Folder Structure:

Firstly, set up the following folder structure inside your application's codebase:

```
.
├── tests
│   ├── __init__.py
│   ├── pytest.ini
│   └── workflow_test.py

```

### Import Dependencies:

Within the `workflow_test.py` file, make sure you have the necessary imports including the Temporal Workflow Environment and the relevant parts of your application:

```python
import uuid
import pytest

from temporalio import activity
from temporalio.testing import WorkflowEnvironment
from temporalio.worker import Worker

from activities import ssn_trace_activity
from workflows import BackgroundCheck
```

The `WorkflowEnviroment` import allows you to setup a client and start the time skipping server as `env`.

### Workflow Execution Test:

To test the execution of your workflow, initiate the Worker and set the expected outcome of the activity's argument to `Pass`.

```python
@pytest.mark.asyncio
async def test_execute_workflow():
    task_queue_name = str(uuid.uuid4())

    async with await WorkflowEnvironment.start_time_skipping() as env:
        async with Worker(
            env.client,
            task_queue=task_queue_name,
            workflows=[BackgroundCheck],
            activities=[ssn_trace_activity],
        ):
            result = await env.client.execute_workflow(
                BackgroundCheck.run,
                "555-55-5555",
                id=str(uuid.uuid4()),
                task_queue=task_queue_name,
            )
            assert "Pass" == result

```

### Mocking an Activity:

To simulate an activity for testing, you can mock it. Here's how you can mock the `ssn_trace_activity`:

```python
@activity.defn(name="ssn_trace_activity")
async def ssn_trace_activity_mocked(name: str) -> str:
    return f"Pass, {name} from mocked activity!"

@pytest.mark.asyncio
async def test_mock_activity():
    task_queue_name = str(uuid.uuid4())

    async with await WorkflowEnvironment.start_time_skipping() as env:
        async with Worker(
            env.client,
            task_queue=task_queue_name,
            workflows=[BackgroundCheck],
            activities=[ssn_trace_activity_mocked],
        ):
            result = await env.client.execute_workflow(
                BackgroundCheck.run,
                "555-55-5555",
                id="my-workflow-id",
                task_queue=task_queue_name,
            )
            assert "Pass, 555-55-5555 from mocked activity!" == result

```

### Execute the Test:

With everything set up, you can now run your tests to verify the functionality.

With poe the poet, run `poe test`.
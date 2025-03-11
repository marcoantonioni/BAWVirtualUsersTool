<table>
<tr>
<td width=350 height=350>
<img src="./images/agent1.jpg" width="300" height="300">
</td>
<td>
<pre>
Source code

https://github.com/marcoantonioni/virtual-users-locust-sandbox


Configurations
https://github.com/marcoantonioni/virtual-users-locust-test-configs

BAW Applications
https://github.com/marcoantonioni/virtual-users-locust-apps
</pre>
</td>
</tr>
</table>


<b>BAWVirtualUsersTool</b> is a tool written in Python language for simulating interactions between users and tasks of applications deployed in IBM Business Automation Workflow (both Traditional and CP4BA deployments).

## Context

Business Process Testing (BPT) validates end-to-end business workflows across multiple applications and systems, emphasizing the interconnectedness of these components. Crucial for identifying cross-functional impacts, BPT relies heavily on regression testing to detect unintended consequences from system changes. Given the complexity and time-intensive nature of testing diverse scenarios in long-running processes, automation is essential for effective BPT implementation, enabling efficient bug detection and ensuring system stability before production release.


## Test automation for business processes

The complexity in designing and executing end-to-end tests of a business process can lead the manager of the project to limit the preventive verification of the application functions with a consequent increase in the risks regarding the quality offered to the end user.
Due to the stateful nature of business process management applications, it is never trivial nor cheaper to deal with bug-fixing operations and subsequent migration of process instances from the original template to the new template which offers fixes or even new features.

In my experience gained in the previous role (business automation architect in the IBM Technology Expert Labs team), I have often supported customers also in this activity; each customer has independently chosen the products for generic functional tests, both open source and specific vendors. 
These have always been products that allow user interactions to be recorded via the browser and evaluate the outcome of the test based on the output presented in the browser.
This approach has its value but can only be thought of and implemented at the time of GUI stabilization.
It lacks the ability to evaluate everything that is internal to the business process or even what happens in the integration and choreography of activities outside the business process (intended in terms of values of process instance variables).
It is normal that generic products cannot in any way "look" inside the instance of the process nor apply logic of "assertions" on the internal data/variables of the process instance.

So it would be very useful to have a simple and flexible tool, easily adaptable to the functional business context and data model of each single process template and which allows you to make "assertions" on what is expected regarding the value of the process variables.

Here a list of the generic activities and costs necessary for business process testing.

The costs and time required are very often derived from:
- business solutions with frequent evolution of requirements and modification of user interfaces
- the process model becomes stable before the completion of the web interfaces, with generic tools (web interaction only) to perform an automated test you have to wait for the consolidation of the gui
- different frequency between user interface variation(+) and business process(-)
- redesigning tests that interact at the web browser level is often expensive, generic products are used to interact with the web browser
- complexity in collecting the final information relating to the outcome of a process instance

Some ideas on what is needed to carry out the activity

### Manual operations necessary for unit test setup
The costs and times required are very often derived from:
- definition of the snapshot on which to run the test
- cleaning of processes/tasks present on test environment (other versions of snapshots, previous runs, etc...)
- configuration of users and their profiling in the specific run time environment
- definition of the procedures and datasets that the user will have to follow/use for each use case (entire path of a process instance)
-- whoever defines the operating manual is usually not the developer, it's a second figure with knowledge of the application who will then have to somehow support the tester
- environment setup operations (among the recurring ones for each test and initial one-shot)

### Manual execution of unit tests
The costs and times required are very often derived from:
- it can be the developer if he has end-to-end visibility of the process, otherwise another suitably trained figure/role
- manual verification of results and comparison with expected data
- historicization of the test result
- difficulty of simultaneous use of the development environment between developers and testers caused by long times for manual execution of the tests
- dilated times between version development, manual tests and any feedback to the programmer for bug correction with subsequent reiteration of the tests

### Complexities, limitations and costs of manual activities
- communication between roles, obligation to produce updated documentation for each evolution
- use of common resources, runtime environment if not available a specific test environment
- continuous versioning and new version deployment in case of dedicated test environment, this involves exponential growth of the number of snapshots and increased frequency of environment updating activities
- execution and verification times

### Benefits of test automation
The benefits of adopting ad hoc tools
With a dedicated tool for IBM Business Automation Workflow you can:
- automate almost all of the manual test environment preparation operations
- run human interaction tests automatically
- perform automatic verification of the expected results
Redesigning the tests that interact at the TASK level is relatively simple and fast with the help of ad hoc tools for IBM Business Automation Workflow and allows to anticipate the test of the process logic compared to the test of the unique/gui specific logics.

### Benefits of Assertion Capability for Long-Running Processes

Assertions are crucial for verifying the correctness of long-running BPM processes. Here's why:

- <b>Verification of Asynchronous Operations</b>:
Long-running processes often involve asynchronous operations, making it challenging to determine when a process has completed and whether it has achieved the desired outcome. Assertions allow for the verification of the final state.

- <b>Data Integrity Checks</b>:
Assertions can verify that data has been correctly processed and stored at various stages of the process, ensuring data integrity.

- <b>Outcome Validation</b>:
They enable the validation of specific outcomes, such as the creation of a record in a database, the sending of an email, or the triggering of a downstream process.

- <b>Fault Tolerance Verification</b>:
Assertions can be used to verify that the process handles errors and exceptions correctly, ensuring fault tolerance.

- <b>Increased Test Reliability</b>:
Assertions provide a precise and automated way to verify process behavior, reducing the reliance on manual inspection and improving test reliability.

- <b>Monitoring of Process State</b>:
Assertions can be used to monitor the process state over time, and verify that the process has moved through the correct states.

- <b>Verification of business rules</b>:
Assertions can verify that the business rules within the process are being executed correctly.

- <b>Reduced manual testing</b>:
Automated assertions reduce the amount of manual testing required, saving time and resources.

### One of the possible solution is "BAW Virtual Users Tool" (BAWVUT)
With this open source tool you can:
- simulate the interaction with the process tasks present in the portal task list (list, claim, release, get data, update data, complete)
- start new process instances when exposed to a specific role
- define automatic verification of expected values (process instance variables)
- maintain the history of the runs and their outcome
- highlight which tests have failed and for what reason

### What if the same instrument dedicated to tests could also be used as a load generator?
With BAW VUT it is possible and with the only limitation of exclusion of GUI user interfaces,
these are not used because REST interactions directly use the API dedicated to TASKS.
This means that the measured performance will be related only to the server side business logic.
How ? Maintaining the same basic configuration and replacing the payload generator with, for example, the generation of random values always within the ranges allowed by the application.

### What can you achieve with this automation tool
- greater efficiency and productivity with reduction of test processing times and software correction
- reduction of costs inherent to the resources used
- improvement of the quality of the produced software

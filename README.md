# lambda-redesign
A clone of AWS Lambda that executes Python Script and offers FaaS. The service is distributed with a master slave architeture, and built on consensus algorithm between slaves.

**System Architecture**

<img width="740" alt="image" src="https://github.com/pvinoda/lambda-redesign/assets/60209393/c4b04692-6bb3-4311-96ef-6cdfb58f62d3">

**Design**
Designing an entire system with all its complexities is a detailed process that involves considering various aspects like architecture, components, communication protocols, data flow, and more. Below is a high-level design of the system you described, considering its complexities:

### System Architecture: [kafka to be added]

#### Components:
1. **User Interface (UI):**
   - A web-based dashboard for users to interact with the system.
   - A command-line interface (CLI) for programmatic interaction.

2. **API Gateway:**
   - Handles incoming requests and routes them to the appropriate services.

3. **Task Scheduler:**
   - Receives code submissions and schedules tasks based on user-defined cron expressions or intervals.

4. **Execution Manager:**
   - Manages the execution of Python code in isolated environments (containers).
   - Monitors resource usage and enforces resource limits.

5. **Replication Manager:**
   - Manages primary and replica nodes for fault tolerance.
   - Replicates user code, configurations, and results to ensure availability.

6. **Consensus Module:**
   - Implements a consensus algorithm (e.g., Raft or Paxos) to maintain consistency among primary and replica nodes.

7. **Result Storage:**
   - Stores the results of code executions in a distributed and fault-tolerant manner.

8. **Logging and Monitoring:**
   - Captures logs generated during code execution.
   - Provides real-time and historical performance metrics.

9. **User Management:**
   - Handles user authentication and authorization.
   - Manages user roles and permissions.

10. **Dependency Management:**
    - Manages Python runtime versions and dependencies for code execution.

11. **Event Trigger System:**
    - Allows integration with external event sources for triggering code execution.

12. **Notification Service:**
    - Sends notifications to users based on task status (success, failure).

13. **Cost Management System:**
    - Tracks resource usage for billing purposes.
    - Provides cost estimates to users.

#### Communication Protocols:

- **gRPC:** For communication between various services.
- **REST API:** For user interactions and external integrations.
- **Message Queues (e.g., RabbitMQ):** For handling asynchronous communication between components.

### Data Flow:

1. **User Submits Code:**
   - Users submit Python code through the UI or CLI.

2. **Task Scheduling:**
   - Task Scheduler receives code submissions and schedules tasks based on user-defined schedules.

3. **Code Execution:**
   - Execution Manager executes the code in isolated environments, managing resources and dependencies.

4. **Logging and Monitoring:**
   - Execution Manager logs execution details and metrics.

5. **Result Storage:**
   - Results of code execution are stored in a distributed and fault-tolerant storage system.

6. **Notification:**
   - Users receive notifications based on task status.

7. **Event Trigger (Optional):**
   - Event Trigger System may initiate code execution based on external events.

8. **Consensus and Replication:**
   - Consensus Module ensures consistency among primary and replica nodes.
   - Replication Manager replicates user code, configurations, and results for fault tolerance.

9. **Cost Tracking:**
   - Cost Management System tracks resource usage for billing.

### Security Considerations:

- **Isolation:** Ensure secure isolation between code executions.
- **Authentication and Authorization:** Implement robust user authentication and authorization mechanisms.
- **Code Analysis:** Scan user-submitted code for security vulnerabilities.
- **Secure Communication:** Use secure communication channels between services.

### Scalability Considerations:

- **Horizontal Scaling:** Allow for adding more nodes to handle increased load.
- **Load Balancing:** Distribute tasks evenly across execution environments.
- **Auto-scaling:** Automatically adjust resources based on demand.

### Other Considerations:

- **Documentation:** Provide comprehensive documentation for users and developers.
- **Testing:** Implement unit tests, integration tests, and performance tests.
- **Backup and Recovery:** Regularly backup user data and configurations, and have a disaster recovery plan.

### Technologies:

- **Programming Language:** Golang for its concurrency support and performance.
- **gRPC:** For efficient communication between services.
- **Docker:** For containerization.
- **Kubernetes:** For orchestration and scaling.
- **etcd or Consul:** For distributed configuration management.
- **Raft or Paxos Library:** For consensus and fault tolerance.

### Deployment:

- Deploy the system on a cloud infrastructure like AWS, GCP, or Azure.
- Utilize container orchestration tools like Kubernetes for managing the deployment.

### Maintenance:

- Implement automated updates and health checks.
- Regularly review and update security measures.
- Provide a mechanism for users to report issues.

**Data Flow with Kafka:**
User Submits Code:

Users submit Python code through the UI or CLI.
Task Scheduling:

Task Scheduler publishes scheduling events to a Kafka topic.
Code Execution:

Execution Manager subscribes to the code execution topic, retrieves tasks, and executes code.
Publishes execution results to a Kafka topic.
Logging and Monitoring:

Optionally, publish logs and metrics events to Kafka for centralized monitoring.
Result Storage:

Listens for execution result events on Kafka topics for storage.
Notification:

Users receive notifications based on Kafka events.
Consensus and Replication:

Utilize Kafka for communication and coordination among primary and replica nodes.
Event Trigger (Optional):

Event Trigger System may initiate code execution based on external events and publish to Kafka.


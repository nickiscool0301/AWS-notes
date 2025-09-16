# Step Functions

## Overview
**Serverless workflow orchestration** - Coordinate distributed applications and microservices  
**Visual workflows** - Define business logic using visual workflows  
**AWS service integration** - Connect AWS services without custom code  
**Built-in error handling** - Automatic retry, catch, and rollback capabilities

## Core Concepts

**State Machine**
: JSON-based workflow definition (Amazon States Language)  
: Contains states that define workflow logic  
: Can be Standard or Express workflows

**State**  
: Individual step in workflow  
: Performs work, makes decisions, or waits  
: Receives input, processes it, and produces output

**Execution**  
: Instance of state machine processing input  
: Each execution has unique name and status  
: Can be monitored and debugged individually

## Workflow Types

| Type | Use Case | Duration | Execution History | Pricing |
|------|----------|----------|-------------------|---------|
| **Standard** | Long-running processes | Up to 1 year | Full history kept | Per state transition |
| **Express** | High-volume, short-duration | Up to 5 minutes | CloudWatch Logs | Per execution + duration |

## State Types

**Pass**
: Transform input data or inject fixed data  
: Useful for testing and data manipulation  
: No work performed, just data transformation

**Task**  
: Single unit of work performed by AWS service  
: Lambda function, ECS task, SNS message, etc.  
: Can include retry and error handling

**Choice**  
: Branching logic based on input conditions  
: Multiple conditional branches  
: Default branch for unmatched conditions

**Wait**  
: Delay workflow for specified time  
: Seconds, timestamp, or seconds path  
: Useful for rate limiting or scheduled tasks

**Parallel**  
: Execute multiple branches simultaneously  
: All branches must complete successfully  
: Results combined into single array

**Map**  
: Process array of items in parallel  
: Execute same logic for each array item  
: Configurable concurrency limits

**Succeed/Fail**  
: Terminal states to end execution  
: Succeed: successful completion  
: Fail: error termination with cause/error

## Error Handling

**Retry**
: Automatic retry on errors  
: Configurable retry count and backoff  
: Supports exponential backoff and jitter

**Catch**  
: Handle specific error types  
: Redirect to different state on error  
: Can preserve error information

**Error Types**
- `States.ALL`: Catch all errors
- `States.Timeout`: Task timeout
- `States.TaskFailed`: Task execution failed
- `States.Permissions`: Insufficient permissions
- Custom error names from Lambda functions

## AWS Service Integrations

**Optimized Integrations** (300+ AWS services)
- Lambda: Invoke functions
- ECS: Run tasks
- SNS/SQS: Send messages
- DynamoDB: Read/write data
- S3: Object operations
- Batch: Submit jobs

**Service Integration Patterns**
- **Request Response**: Synchronous, wait for completion
- **Run a Job (.sync)**: Wait for job completion
- **Wait for Callback (.waitForTaskToken)**: Wait for external callback

## Input/Output Processing

**InputPath**: Select portion of input to pass to state  
**OutputPath**: Select portion of output to return  
**ResultPath**: Where to place result in output  
**Parameters**: Create new input using input data and literal values

## Monitoring & Debugging

**Execution History**: Detailed log of all state transitions  
**CloudWatch Integration**: Metrics and logs for monitoring  
**X-Ray Tracing**: Distributed tracing across services  
**Visual Console**: Graphical execution tracking

## Use Cases

**Data Processing Pipelines**
: ETL workflows with multiple steps  
: Error handling and retry logic  
: Coordinate AWS batch jobs

**Microservices Orchestration**  
: Coordinate multiple Lambda functions  
: Handle inter-service communication  
: Implement saga patterns

**Human Approval Workflows**  
: Wait for manual approval steps  
: Send notifications and wait for response  
: Route based on approval decisions

## Best Practices
- Keep state machines focused and modular
- Use appropriate workflow type (Standard vs Express)
- Implement proper error handling with retry/catch
- Use InputPath/OutputPath to minimize data transfer
- Monitor executions with CloudWatch and X-Ray
- Design for idempotency in all states
- Use Map state for parallel array processing
- Keep state machine definitions under version control

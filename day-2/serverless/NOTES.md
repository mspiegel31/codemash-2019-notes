# Hotness === Serverless - Learn how to harness the power of Lambda's in AWS

## What is Serverless?
- Serverless === Using Other Companies Servers

- Serverless is an execution model where the cloud provider is responsible for executing a (preferably small) piece of code by dynamically allocating the computational resources

## What is AWS Lambda?
- Backed by containers (Docker?)
> AWS Lambda lets you run code without provisioning or managing servers. You pay only for the compute time you consume - there is no charge when your code is not running.
> - [AWS lambda main page](https://aws.amazon.com/lambda/)

## Advantages
- Bring Your Own Language
- (Virtually) limitless scalability
- Pay only for what you use
- "Just code, no fuss"
- Fault Tolerance/Automatic Failover

## When does Lambda make sense
- Small, focused tasks
    - some HTTP requests, some triggered events (i.e. chron jobs)
- Event Driven Applications
    - message gets added to queue
    - log writes
- Serverless/static website hosting
- High Volume / High Availability

## When does Lambda **not** make sense
- Long running tasks
    - Lambdas come with a default ~3s timeout, max 10m timeout

- Data intensive applications
    - defaults to max memory of 128 MB

- Highly Parallelized Code

## Technical Considerations
- How will lambda be invoked?
- What data will be returned?
- Execution Roles (IAM rights)
    - Defaults to closed, must open W/intent
- Short lifecycle
    - i.e., using traditional DI may not be good idea with Lambda, as it adds overhead at runtime
- Limited Memory
    - limited cache space
    - because container is spun up and down, no guarantees that cache will survive between Lambda invocations

## Warm vs Cold Startup
- **First invocation also incurs the overhead of starting a container.** (cold startup)
- if cache is a must, consider something out-of-process

## Software considerations
- keep dependencies, codebase *lean*
- Log early, Log often, log _EVERYTHING_
    - no attaching to running process for debugging
    - remember your obligations though: don't log PII
    - setup a retention policy
    - bonus: `stdout` is piped to cloudwatch
- Unit testing is especially important in this scenario.
- As is integration testing with real data

## Lambda Layers
>You can configure your Lambda function to pull in additional code and content in the form of layers. A layer is a ZIP archive that contains libraries, a custom runtime, or other dependencies. With layers, you can use libraries in your function without needing to include them in your deployment package.

>Layers let you keep your deployment package small, which makes development easier. You can avoid errors that can occur when you install and package dependencies with your function code. For Node.js, Python, and Ruby functions, you can develop your function code in the Lambda console as long as you keep your deployment package under 3 MB.

## Debugging considerations
- Non-prod log:  human readable
- Prod log: machine readable

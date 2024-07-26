Sure, here's a README file based on the provided information:

---

# mob_api_base

This repository contains the Groovy scripts and XML configurations for the `mob_api_base` project. The purpose of this project is to replace the existing Newman collection built by Postman with a ReadyAPI project that offers enhanced testing capabilities. 

## Overview

The `mob_api_base` project aims to achieve the following:

1. **1:1 Exact Test Replacement**: Each test in the current Newman collection will be replicated in ReadyAPI, ensuring a seamless transition.
2. **Data-Driven Additional Coverage**: The new setup will introduce data-driven tests to expand coverage and enhance reliability.
3. **Improved Schema Validations**: Enhanced schema validation scripts will ensure that API responses adhere strictly to the expected formats.
4. **Improved Database Validations**: Integration of database validation scripts will verify the integrity and accuracy of the data stored in the database.
5. **Modular Design**: All scripts will be modular, reusing smaller scripts to maintain clarity and simplicity.
6. **Enhanced Naming Conventions**: Consistent and clear naming conventions will be applied across all scripts and test steps for better maintainability.

## Project Structure

- **scripts/xml**: Directory for XML configurations.
- **scripts/groovy**: Directory for Groovy scripts.

## Getting Started

### Prerequisites

Ensure you have the following tools installed:

- ReadyAPI
- Git

### Installation

1. Clone the repository to your local machine:

    ```sh
    git clone https://github.com/your-username/mob_api_base.git
    cd mob_api_base
    ```

2. Open ReadyAPI and import the project from the cloned repository.

### Running Tests

To run the tests in ReadyAPI:

1. Open the project in ReadyAPI.
2. Select the test suite you want to run.
3. Right-click on the test suite and select "Run TestSuite".

### Sample Scripts

#### Groovy Script for Retry Logic

Below is an example of a Groovy script that retries a request up to 3 times if it fails:

```groovy
import com.eviware.soapui.support.GroovyUtils
import com.eviware.soapui.impl.wsdl.teststeps.WsdlTestRequestStep
import com.eviware.soapui.model.testsuite.TestStepResult

def maxRetries = 3
def retryCount = 0
def testStepName = "YourRequestTestStepName"
def testStep = testRunner.testCase.testSteps[testStepName]

if (testStep instanceof WsdlTestRequestStep) {
    def result
    while (retryCount < maxRetries) {
        retryCount++
        log.info "Attempt ${retryCount} of ${maxRetries}"
        
        result = testStep.run(testRunner, context)
        
        if (result.status == TestStepResult.TestStepStatus.OK) {
            log.info "Request succeeded on attempt ${retryCount}"
            break
        } else {
            log.warn "Request failed on attempt ${retryCount}"
            if (retryCount == maxRetries) {
                log.error "Request failed after ${maxRetries} attempts"
                testRunner.fail("Request failed after ${maxRetries} attempts")
            } else {
                sleep(2000)
            }
        }
    }
} else {
    log.error "Test step is not a request step"
}
```

## Contributing

We welcome contributions to the `mob_api_base` project. If you have any ideas, suggestions, or bug reports, please open an issue or submit a pull request.

### How to Contribute

1. Fork the repository.
2. Create a new branch for your feature or bug fix.
3. Implement your changes.
4. Submit a pull request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact

For any questions or support, please reach out to [Reggie](mailto:reginald.moore@dealerware.com).



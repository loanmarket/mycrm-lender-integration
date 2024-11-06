# Testable Lodgement Solution
Our objective is to establish direct integration with lenders for lodging loan applications via APIs, eliminating the need for third-party intermediaries. To facilitate a smooth and efficient integration process, we have developed a testing tool designed to streamline communication and issue identification between our system and lender platforms. This document outlines the purpose and usage of this tool to assist lenders in their testing and onboarding process.
## Purpose of the Testing Tool

The testing tool is intended to simplify the process of validating API integrations for direct loan application lodgement. It enables lenders to test the receipt and handling of loan applications submitted from MyCRM, ensuring that any issues, such as data formatting or structural discrepancies in the JSON payload, can be identified and reported efficiently. This approach accelerates issue resolution and enhances the overall integration experience.
### Key Features:

- **Issue Detection and Reporting**: Lenders can use the tool to verify that the loan application data they receive conforms to their expected structure and business rules. The tool is equipped to identify issues related to JSON structure, field formats, missing data, and more.
- **Preconfigured Sample Loan Applications**: To save time and reduce the overhead of creating dummy loan applications manually, the tool includes prebuilt sample loan applications. Each sample is designed to cover a specific scenario, making it easier for lenders to evaluate various use cases and identify issues.
- **Scenario-based Testing**: Users can select from predefined scenarios, each corresponding to a different type of loan application or test case. Based on the selected scenario, the tool sends the relevant sample loan application to the specified endpoint.
- **Containerized for Ease of Use**: The testing tool is packaged as a Docker container, allowing it to be run locally on the lender’s environment without the need for complex installations or configurations. This enables quick deployment and isolated testing without affecting existing systems.
---
# Configuration Settings for the Testable Lodgement Solution

The **Testable Lodgement Solution** requires specific configuration settings to define how the tool interacts with the lender’s systems during the integration process. These settings can be provided either through environment variables or via the `appsettings.json` file. Proper configuration is essential for ensuring that the solution behaves as expected and successfully communicates with the designated endpoints.

## Required Configuration Settings

The following settings are necessary for the Testable Lodgement Solution to operate correctly:

1. **`SubmissionUrl`**
    
    - **Description**: Specifies the base URL for sending requests from the tool. This is the endpoint where the loan application packages will be submitted.
    - **Format**: URL string (e.g., `"https://127.0.0.1:44362/submit"`).
    - **Usage**:The tool sends a package to the specified endpoint by this variable. The full url of the endpoint that is supposed to recieve the pacakge should be provided by this URL.
    - **Important Consideration**:
    Docker containers use isolated networks, meaning that `localhost` inside the container refers to the container’s own network, not the host machine’s network. If your endpoint is running on your host machine and you want the Docker container to connect to it, use `host.docker.internal` (for Docker on Windows and macOS).For example:
        ` LodgementSettings__SubmissionUrl="http://host.docker.internal:54856/submit"`   
        This ensures that the container can communicate with the services running on your   host machine.
    - **Environment Variable**: `LodgementSettings__SubmissionUrl`
2. **`ValidationUrl`**
    
    - **Description**: Specifies the base URL for sending requests for validation from the tool. This is the endpoint where the loan application packages will be validated.
    - **Format**: URL string (e.g., `"https://127.0.0.1:44362/validate"`).
    - **Usage**:The tool sends a package to the specified endpoint by this variable. The full url of the endpoint that is supposed to recieve the pacakge should be provided by this URL.
    - **Important Consideration**:
    Docker containers use isolated networks, meaning that `localhost` inside the container refers to the container’s own network, not the host machine’s network. If your endpoint is running on your host machine and you want the Docker container to connect to it, use `host.docker.internal` (for Docker on Windows and macOS).For example:
        ` LodgementSettings__ValidationUrl="http://host.docker.internal:54856/validate"`   
        This ensures that the container can communicate with the services running on your   host machine.
    - **Environment Variable**: `LodgementSettings__ValidationUrl`
3. **`MediaType`**
    
    - **Description**: Defines the media type (content type) of the packages that are being sent to the endpoint.
    - **Format**: String (e.g., `"application/json"`).
    - **Supported Values**: `application/json`, `application/xml`.
    - **Usage**: This setting determines the format in which the loan application packages are serialized and transmitted.
    - **Environment Variable**: `LodgementSettings__MediaType`
4. **`Country`**
    
    - **Description**: Specifies the country context for the loan application. This setting is used to determine the serialization format of the JSON based on the functionalities provided by `DotnetLixi` package.
    - **Supported Values**: `Australia`, `NewZealand`
    - **Usage**: The country setting controls how the loan application data is serialized to ensure compliance with local regulations and standards. It should be set to the corresponding country where the lender operates.
    - **Environment Variable**: `LodgementSettings__Country`
5. **`Version`**
    
    - **Description**: Indicates the LIXI version that the loan application package should be serialized to. The LIXI standard is used for structuring loan application data in a format that is consistent and interoperable across different systems.
    - **Format**: String (e.g., `"2.6.73"`).
    - **Supported Values**: 
        - "2.6.35"  (Cal2635)
        - "2.6.46"  (Cal2646) 
        - "2.1.8"   (Cnz218)
        - "2.1.19"  (Cnz2119) 
        - "2.6.56"  (Cal2656) 
        - "2.1.29"  (Cnz2129) 
        - "2.6.73"  (Cal2673) 
        - "2.1.31"  (Cnz2131) 
    - **Usage**: This setting ensures that the loan package is serialized in the correct version of the LIXI standard that the lender’s system expects.
    - **Environment Variable**: `LodgementSettings__Version`
6. **`IgnoreSSL`**
    
    - **Description**: Determines whether SSL certificate validation should be ignored when the tool is making HTTPS requests to the specified endpoints.
    - **Supported Values**: `true`, `false`
    - **Usage**: This setting is particularly useful when running the tool as a Docker image and making requests to `localhost` endpoints that use self-signed certificates. By setting `IgnoreSSL` to `true`, SSL certificate validation is bypassed, preventing certificate-related errors. If this setting is `false`, the user must configure proper SSL certificates or use HTTP ports instead. 
    - **Warning**: This will bypass the CA validation process, use wisely at your own risk. 
    - **Environment Variable**: `LodgementSettings__IgnoreSSL`

## Configuration Options

The above settings can be provided in one of the following ways:
### 1. **Environment Variables**

Set each configuration setting as an environment variable, using the following format:

- `LodgementSettings__SubmissionUrl=https://host.docker.internal:7182/submit`
- `LodgementSettings__ValidationUrl=https://host.docker.internal:7182/validate`
- `LodgementSettings__MediaType=application/json`
- `LodgementSettings__Country=Australia`
- `LodgementSettings__Version=2.6.73`
- `LodgementSettings__IgnoreSSL=true`

This approach is recommended when deploying the tool in a containerized environment, as it allows for greater flexibility and isolation between different configurations. 

### 2. **`appsettings.json` File**

Alternatively, the settings can be included in the `appsettings.json` configuration file as shown below:


```
  "LodgementSettings": {
    "SubmissionUrl": "https://host.docker.internal:7182/submit",
    "ValidationUrl": "https://host.docker.internal:7182/validate",
    "MediaType": "application/json",
    "Country": "Australia",
    "Version": "2.6.73"
  } 
```

This option is suitable for local testing and development environments where settings are unlikely to change frequently.

## Additional Considerations

- When running the tool within a Docker container, ensure that the configuration values, especially the `LodgementSettings__Url` and `LodgementSettings__IgnoreSSL`, are appropriately set. Failure to do so can result in issues connecting to local or secured endpoints due to SSL validation errors.
- For production environments, it is advisable to use a properly configured SSL certificate and set `LodgementSettings__IgnoreSSL` to `false` to enforce secure communication.

---

# Endpoints Overview

### 1. `POST /Lodgement/Submit`

- **Purpose**: This endpoint is used to submit a loan application package directly to the specified endpoint, simulating the end-to-end submission process.
- **Functionality**: Users must construct the loan application package in JSON format and include it in the request body. The package is then forwarded to the designated endpoint for further processing.
- **Parameters**:
    - `LoanApplicationPackage` (JSON): The complete loan application package, formatted as per the LIXI or lender-specific schema.
    - `EndpointURL`: The target URL where the package should be sent.
- **Use Case**: This endpoint is ideal for testing the actual submission of dynamically created loan packages, enabling users to verify that the package contents and structure conform to lender expectations and requirements.

### 2. `POST /Lodgement/SubmitTestPackage`

- **Purpose**: Designed primarily for testing purposes, this endpoint allows users to submit predefined sample loan application packages without the need to manually construct them.
- **Functionality**: The tool comes with a set of prebuilt sample loan applications, covering various scenarios such as Refinancing, Top-Up, and First Home Buyer applications. Users can select a scenario and submit the corresponding sample package directly to the specified endpoint.
- **Parameters**:
    - `Scenario` (string): Specifies the type of loan scenario for which the test package should be submitted (e.g., `Refinancing`, `TopUp`).
    - `EndpointURL`: The target URL where the sample package should be sent.
- **Use Case**: This endpoint simplifies testing by allowing users to evaluate specific scenarios without needing to manually create loan packages. It helps validate how different types of loan applications are processed by the lender’s systems.

### 3. `POST /Lodgement/Validate`

- **Purpose**: This endpoint is used to validate the structure and content of a loan application package before submission.
- **Functionality**: Users can pass a loan package in JSON format to this endpoint, which then forwards it to the validation service. The service checks the package against schema and business rules, ensuring compliance and correctness.
- **Parameters**:
    - `LoanApplicationPackage` (JSON): The loan package to be validated, formatted as per LIXI standards or lender-specific requirements.
    - `ValidationEndpointURL`: The URL of the validation service to which the package should be sent.
- **Use Case**: This endpoint is useful for verifying loan packages prior to submission, helping to catch any errors or inconsistencies in the package content early in the process.

### 4. `POST /LixiPackage/SaveLixiPackageSample`

- **Purpose**: This endpoint is used to save a LIXI-format loan application package sample, making it available for future testing or reference.
- **Functionality**: Users can create a LIXI package sample for a particular scenario and save it using this endpoint. The saved sample can include specific data and configurations that reflect lender requirements or unique testing cases.
- **Parameters**:
    - `Scenario` (string): The scenario name associated with the sample package (e.g., `Refinancing`, `TopUp`).
    - `BeObfuscated`(boolean): Determines if the data for a specific field should be obfuscated or not. At this point, if the flag is true, only the value of  following properties get obfuscated: "CompanyName", "Email", "Number", "ABN", "WebAddress", "BusinessNumber", "Name"
    - `LIXIPackageSample` (JSON): The LIXI package to be saved, formatted as per industry standards.
- **Use Case**: This endpoint is valuable for maintaining a repository of sample packages that can be reused across different testing sessions, eliminating the need to recreate packages for commonly tested scenarios.

### 5. `GET /LixiPackage/GetLixiPackageSample/{scenario}`

- **Purpose**: This endpoint retrieves a previously saved LIXI package sample based on a specified scenario.
- **Functionality**: Users can query this endpoint to access the stored LIXI package for a given scenario. The retrieved package can then be used as a template or reference for creating new packages or for testing the submission and validation processes.
- **Parameters**:
    - `scenario` (string): The scenario identifier for which the LIXI package sample should be retrieved (e.g., `Refinancing`, `TopUp`).
- **Use Case**: This endpoint is useful for quickly accessing predefined LIXI packages without manually searching or recreating them, enabling more efficient testing and validation workflows.

---
# Running the Testable Lodgement Solution Docker Image
Follow the steps below to set up and run the Docker container for the Testable Lodgement Solution for. This tool allows lenders to test the submission and validation of loan packages in various scenarios using a standard set of APIs. 

## Using docker compose
This guide will help you set up and run the `mycrmfinance/mycrm-testable-lodgement` service using Docker Compose. This service simulates a testable lodgement for loan applications. You will use the provided `compose.yml` file to configure and run the service.

### Prerequisites
Make sure the following prerequisites are met:
1. **Docker** is installed and running on your machine. If not installed, download and install Docker from [here](https://docs.docker.com/get-docker/).
2. **Docker Compose** is installed. It is typically bundled with Docker Desktop. You can verify by running:
   ```bash
   docker-compose --version
   ```

### Steps to Use Docker Compose

1. **Download the `compose.yml` File**
   Save the [`compose.yml`](https://github.com/loanmarket/mycrm-lender-integration/blob/main/compose.yaml) file to your local system. 



2. **Navigate to the Directory**
   Open a terminal or command prompt and navigate to the directory where you saved the `compose.yml` file:

   ```bash
   cd /path/to/your/compose-directory
   ```
2. **Set up the environment variables**
    you need to provide four critical environment variables:

    - **`LodgementSettings__SubmissionUrl`**: The base endpoint URL for receiving the loan packages for submission.
    - **`LodgementSettings__ValidationUrl`**: The base endpoint URL for receiving the loan packages for validation.
    - **`LodgementSettings__Country`**: The country for which the lodgement is being tested. Valid options are `Australia` or `NewZealand`.
    - **`LodgementSettings__Version`**: The supported LIXI version for the loan application package (e.g., `2.6.35`).
    - **`LodgementSettings__IgnoreSSL`**: A boolean setting that indicates whether to bypass SSL certificate validation. This should be set to `true` if using self-signed certificates or when connecting to HTTPS endpoints on localhost.
    For example:
    ```yaml
    environment:
      - LodgementSettings__SubmissionUrl=https://yourapiendpoint.com/submit
      - LodgementSettings__ValidationUrl=https://yourapiendpoint.com/validate
      - LodgementSettings__Country=Australia
      - LodgementSettings__Version=2.6.35
      - LodgementSettings__MediaType=application/json
      - LodgementSettings__IgnoreSSL=true
    ```
    #### Explanation:
    Make sure to replace the placeholder values with your actual configurations:
    
    - Replace `LodgementSettings__SubmissionUrl` and `LodgementSettings__ValidationUrl` values with your actual endpoint URL.
    - Replace `"Australia"` with the appropriate country (`Australia` or `NewZealand`).
    - Replace `"2.6.35"` with the Lender’s supported LIXI version.
    

    
  
3. **Run the Docker Compose Command**
   Run the following command to start the service in detached mode (running in the background):

   ```bash
   docker-compose up -d
   ```

   This command will:
   - Pull the `mycrmfinance/mycrm-testable-lodgement:latest` image from Docker Hub (if not already pulled).
   - Start the container and expose it on port 8080.
   - Automatically set up the necessary environment variables.
   - **`-d`**: Runs the container in detached mode (in the background).

4. **Verify the Service is Running**
   You can check if the container is running by using the following command:

   ```bash
   docker ps
   ```

   This will list all running containers. You should see a container with the image `mycrmfinance/mycrm-testable-lodgement:latest` in the list.

5. **Access the Service**
   The service will be available on sepecifed port by docker compose which in this case would be`8080`. You can interact with the API or perform lodgement tests by using the Swagger which can be reached via `http://localhost:8080/swagger/index.html`address.

6. **Stop the Service**
   If you want to stop the service, run the following command:

   ```bash
   docker-compose down
   ```

   This will stop and remove the running container.

#### **Notes**
- **Sample loan applicaiton files**: All the sample loan applications for different scenarios could be find in the app/LixiPackageSamples folder as json files in the container. Please be noticed, each time you run the image for testable lodgement, the content of this folder would get reset and all the previous changes on the sample files would be lost. 

#### **Troubleshooting**

- **If you can't access the service**: Ensure that no other service is using port 8080 on your machine. You can change the port in the `docker-compose.yml` file if necessary (e.g., change `"8080:8080"` to `"9090:8080"`).
- **If you need to change environment variables**: You can modify the values for `LodgementSettings__URL`, `LodgementSettings__Country`, etc., directly in the `docker-compose.yml` file before running `docker-compose up`.
- **If you encounter permission issues**: Ensure that Docker Desktop is running with sufficient permissions, and try running the terminal or command prompt as an administrator.

---

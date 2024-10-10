# Lender Integration for Direct Lodgement

This guide outlines the process of integrating a lender’s API with MyCRM to facilitate direct submission of loan applications, eliminating the need for third-party intermediaries. With direct lodgement, MyCRM enables the seamless transmission of loan applications straight to a lender’s system, enhancing efficiency and reducing processing time. The integration process involves collaboration between LMG and the lender. 

# Integration Steps

By following these steps, lenders can successfully integrate their APIs with MyCRM to enable direct lodgement of loan applications. Each party has distinct responsibilities to ensure a smooth implementation. Here’s a high-level overview of the steps required:


![image](https://github.com/user-attachments/assets/71a09fa8-d220-4971-a784-91d5a6683c78)


## Step 1: Gather and Share Prerequisite Information

Both LMG and the lender need to gather and share the following information before beginning the integration:

| Prerequisite | Details | Responsible Party |
| :---- | :---- | :---- |
| API Documentation | Lender’s API documentation with details about endpoints, authentication methods, and expected payloads. | Lender |
| API Credentials | API keys, client IDs, secrets, or any tokens required for authentication. | Lender |
| Test Environment | Access to the lender's sandbox or test environment | Lender |
| Lixi Version | Supported Lixi standards for receiving loan application packages | Lender |
| Media type | Supported media type for receiving Lixi Packages (JSON, XML, etc.) | Lender |
| Testable lodgement tool | A tool for testing direct lodgment via sending sample loan applications to the lenders API endpoints. | LMG |
| Access to MyCRM (Integration environment) | Developer access to MyCRM with the necessary permissions to test end to end. | LMG |

## Step 2: Implement Integration in MyCRM 

LMG is responsible for setting up MyCRM to communicate with the lender’s API. This step involves several configurations to enable direct submission of loan applications:

1. **Set Up Authentication**  
   * Configure MyCRM with the lender’s authentication requirements.  
   * Use secure credentials like API keys or OAuth tokens for secure communication.  
2. **Configure API Endpoints**  
   * Set up the **Submission Endpoint** to send complete loan application packages.  
   * Set up the **Validation Endpoint** to verify the loan application package before submission.  
3. **Ensure Compatibility with LIXI Version**  
   * Make sure that MyCRM can send loan application packages that match the lender’s expected LIXI version.  
4. **Implement the Lodgement Service**  
   * Develop a specific lodgement service in MyCRM that will handle the direct submission of loan applications.

## Step 3: Test the Integration

Before moving forward, it’s crucial to test the integration to ensure everything is working correctly. LMG will perform the following tests:

1. **Test Authentication**  
   * Verify that MyCRM can securely connect to the lender’s system using the provided credentials.  
2. **Submit a Test Loan Application**  
   * Use MyCRM to send a test loan application using dummy data.  
   * Confirm that the test application is received successfully by the lender’s API.  
3. **Validate Responses**  
   * Monitor the responses from the lender’s API.  
   * Address any errors or mismatches to refine the integration.

## Step 4: Verify Functionality and End-to-End Testing

Both LMG and the lender need to conduct comprehensive testing to verify that the integrated solution works as intended. This step involves:

1. **Coordinated Testing**  
   * Conduct joint testing sessions where both parties review and test the submission and validation processes.  
2. **Validate Realistic Loan Scenarios**  
   * Use realistic test scenarios, such as New Loan Applications, Refinancing, and Top-Up, to ensure the integration handles each case correctly.  
3. **Check for Data Accuracy**  
   * Verify that all loan application data is accurately transmitted between MyCRM and the lender’s system without loss or corruption of information.  
4. **Review Error Handling and Responses**  
   * Simulate potential errors or unexpected inputs to confirm that the integration can handle various scenarios gracefully.  
5. **Confirm Successful Lodgement**  
   * Ensure that loan applications are successfully lodged in the lender’s system and that responses are processed correctly in MyCRM.

## Using the Testable Lodgement Tool 

The **Testable Lodgement Tool** is a specialized utility developed by LMG to assist lenders in testing the integration of their API with MyCRM before going live. This tool is designed to simulate the submission of loan applications from MyCRM to the lender’s API, ensuring that the integration is working correctly in various scenarios without having to use real loan data. Lenders can begin testing their API integration using the Testable Lodgement Tool **while LMG is still developing the integration**. This allows for early detection of any issues related to JSON format, field structure, or data compatibility, making the integration process faster and more efficient.

### What Does the Testable Lodgement Tool Do?

* **Simulates Loan Application Submissions**: The tool sends sample loan applications to the lender’s API, mimicking real-life scenarios such as new loans, refinancing, and top-ups.  
* **Pre-Configured Scenarios**: It includes several pre-built test cases with sample data to test different types of loan applications, making it easy for lenders to validate their system’s response to a variety of situations.  
* **Validation and Error Testing**: The tool allows lenders to test validation logic and error handling by submitting sample loan applications with valid or intentionally invalid data.  
* **Supports Multiple Loan Types**: With configurations for different loan types and variations, the tool ensures that the integration is robust and can handle different application structures.

### Benefits of Using the Testable Lodgement Tool

1. **Quick and Easy Testing**: The tool allows lenders to test the integration without needing to build their own testing framework or use real data.  
2. **Identify Issues Early**: By testing with pre-configured scenarios, lenders can identify any discrepancies, errors, or compatibility issues before going live.  
3. **Supports Multiple Environments**: The tool can be configured to test in various environments such as development, test, or sandbox, ensuring it aligns with different stages of integration.

### How to Use the Testable Lodgement Tool

Instructions for setting up and using the Testable Lodgement Tool are provided in a separate document. Please refer to this link for detailed step-by-step instructions on how to use the tool.



# Points of contact

For any assistance or questions during the integration process, please reach out to the LMG integration team:

| Name | Role | Email |
| :---- | :---- | :---- |
| Jesse Creech | Engineering Manager | jesse.creech@lmg.broker |
| Isabella Shoard | Product Manager | isabella.shoard@lmg.broker |
| Ali Arman | Lead Software Engineer | ali.arman@lmg.broker |
| Andrew Beasley | Senior Software Engineer | andrew.beasley@lmg.broker |



# CMPG 323 Project 4 : Testing and Robotic Process Automation (RPA) with UiPath
<img src="https://github.com/ChiefMonk/CMPG-323-Overview-37016776/blob/main/nwu_logo.jpg" width="200px" style="text-align:center;float:center;" />

### Table of Contents
1. [Introduction](#intro) 
2. [Authentication and Authorization](#auth) 
3. [Testing the IoT Zones](#zones)
4. [Testing the IoT Categories](#categories)
5. [Testing the IoT Devices](#devices)
6. [Contributors](#cont)
7. [References](#refs)

<a name="intro"></a>
## 1. Introduction
This is the fourth project of the CMPG 323 module deliverables. Testing is a crucial part of any solution and can be done from many different perspectives; the internal development team testing, business user acceptance testing (UAT), etc.

Robotic Process Automation (RPA) refers to the use of technology to mimic human tasks in the same way that a person would execute a process. This usually refers to, what we would call, ‘front-end’ or UI (User Interface) automation. RPA is often used to automate time-consuming and highly repetitive tasks to allow people the availed capacity to work on more intuitive tasks.

Therefore this project aims to use the power of RPA with UiPath to test the functionality of the IoT Device Management System hosted at https://connectedoffice-devicemanagement.azurewebsites.net.


### Testing Scope
The system stores the following specific information about Zones, Categories and Devices. Therefore, the testing scope involves the creation, reading, editing and deletion of the following information about every applicable entity:
* Zone   
    * Zone Name
    * Zone Description   

* Category  
    * Category Name
    * Category Description    

* Device
    * Device Name
    * Category ID
    * Zone ID
    * Status
    * Is Active   


### Test Data
The test data is contained in an excel file named 'Connected Office Test Data.xlsx' located under a folder called 'Data'. The file has four distinct sheets:
* Zone - contains the zones test data
* Category - contains the zones test data
* Device - contains the zones test data
* Test Results - records the results of each test per Zone ID, Category ID and Device ID. The test results per ID are recorded under the following headings:
    * Create Test Passed = 'TRUE' otherwise 'FALSE'
    * Read Test Passed = 'TRUE' otherwise 'FALSE'
    * Update Test Passed = 'TRUE' otherwise 'FALSE'
    * Delete Test Passed = 'TRUE' otherwise 'FALSE'

The image below show the initial state of the Test Results sheet. On startup, the automation process actually resets all the test results to 'FALSE', just incase the process is being rerun on the same test data.

<img src="tests_before_excel_data.png" width="500px" style="display: inline-block; margin: 0 auto; max-width: 300px" />
<p><sup></sup><em>Figure 1: The image above shows the initial state of the test results data</em><sub></sub></p>

<a name="auth"></a>
## 2. Authentication and Authorization
The IoT Device Management System only authorizes properly authenticated users to perform the actions defined and specified in the process definition document. Therefore, when the automation script launches the web application, the following checks are done:
* Checks if a user is already logged onto the system. If there is, then the user is logged out first by auto-clicking the logout menu option.
* The system then auto-logs in a user with the username and password defined and hardcoded in the process document.
* The automation will only proceed if the user is properly authenticated and authorized.


<a name="zones"></a>
## 3. Testing the IoT Zones
The test data to be used for Zones is contained in same excel file under sheet 'Zones'. As indicated in the image below, the data consists three (3) distinct columns: 
* ID
* Zone Name
* Zone Description.

<img src="zones_excel_data.png" width="500px" style="display: inline-block; margin: 0 auto; max-width: 300px" />
<p><sup></sup><em>Figure 2: The image above shows the zones subset of test data from the provided Excel file</em><sub></sub></p>

For performance reasons, at the beginning of the test process for zones, the whole test data is read from the excel file into the ZoneDtatable. Before the test zones data in the datatable is processed, the automation process first iteratively deletes all exiting zones in the web application. 

After the previous test data is removed, then for each row of test data, the following automation process is followed:
* CREATE
    * A zone is created by entering the name and description in the fields provided
    * If the creation is successful, then the 'Create Test Passed' for that Zone ID is updated to 'TRUE', otherwise 'FALSE'
* READ
    * After the zone is created, the details are read and displayed on the zone details page
    * If the read is successful, then the 'Read Test Passed' for that Zone ID is updated to 'TRUE', otherwise 'FALSE'
* UPDATE
    * The created zone is edited by appending the text 'EDITED' at the end of the name and description
    * If the update is successful, then the 'Update Test Passed' for that Zone ID is updated to 'TRUE', otherwise 'FALSE'
* DELETE
    * The created zone is then finally deleted by auto-clicking the delete icon for that row on the zones home page
    * If the deletion is successful, then the 'Delete Test Passed' for that Zone ID is updated to 'TRUE', otherwise 'FALSE'

All the above updates of the test results are stored in the TestResults datatable. After all the test data has been processed, the 'Test Results' sheet of the excel file is updated with the test results datatable as indicated below, assuming that all tests passed.

<img src="zones_results_excel_data.png" width="500px" style="display: inline-block; margin: 0 auto; max-width: 300px" />
<p><sup></sup><em>Figure 3: The image above shows the test results sheet after all zones has been processed successfully and the Excel file updated accordingly</em><sub></sub></p>

<a name="categories"></a>
## 4. Testing the IoT Categories
The test data to be used for Categories is contained in same excel file under sheet 'Category'. As indicated in the image below, the data consists three (3) distinct columns: 
* ID
* Category Name
* Category Description.

<img src="categories_excel_data.png" width="500px" style="display: inline-block; margin: 0 auto; max-width: 300px" />
<p><sup></sup><em>Figure 4: The image above shows the categories subset of test data from the provided Excel file</em><sub></sub></p>

For performance reasons, at the beginning of the test process for categories, the whole test data is read from the excel file into a CategoryDtatable. Before the test categories data in the datatable is processed, the automation process first iteratively deletes all exiting categories in the web application. 

After the previous test data is removed, then for each row of test data, the following automation process is followed:
* CREATE
    * A category is created by entering the name and description in the fields provided
    * If the creation is successful, then the 'Create Test Passed' for that Category ID is updated to 'TRUE', otherwise 'FALSE'
* READ
    * After the category is created, the details are read and displayed on the zone details page
    * If the read is successful, then the 'Read Test Passed' for that Category ID is updated to 'TRUE', otherwise 'FALSE'
* UPDATE
    * The created category is edited by appending the text 'EDITED' at the end of the name and description
    * If the update is successful, then the 'Update Test Passed' for that Category ID is updated to 'TRUE', otherwise 'FALSE'
* DELETE
    * The created category is then finally deleted by auto-clicking the delete icon for that row on the zones home page
    * If the deletion is successful, then the 'Delete Test Passed' for that Category ID is updated to 'TRUE', otherwise 'FALSE'

All the above updates of the test results are stored in the TestResults datatable. After all the test data has been processed, the 'Test Results' sheet of the excel file is updated with the test results datatable as indicated below, assuming that all tests passed.

<img src="categories_results_excel_data.png" width="500px" style="display: inline-block; margin: 0 auto; max-width: 300px" />
<p><sup></sup><em>Figure 5: The image above shows the test results sheet after all categories has been processed successfully and the Excel file updated accordingly</em><sub></sub></p>


<a name="devices"></a>
## 5. Testing the IoT Devices
The test data to be used for Devices is contained in same excel file under sheet 'Device'. As indicated in the image below, the data consists six (6) distinct columns: 
* ID
* Device Name
* Category Name
* Zone Name
* Status
* Is Active

<img src="devices_excel_data.png" width="500px" style="display: inline-block; margin: 0 auto; max-width: 300px" />
<p><sup></sup><em>Figure 6: The image above shows the devices subset of test data from the provided Excel file</em><sub></sub></p>

For performance reasons, at the beginning of the test process for devices, the whole test data is read from the excel file into a DeviceDtatable. Before the test devices data in the datatable is processed, the automation process first iteratively deletes all exiting devices in the web application. 

Thereafter, all the distinct categories and zones to be used for device testing are first created, so they can be available in the respective drop down lists.

After the previous test data is removed, then for each row of test data, the following automation process is followed:
* CREATE
    * A device is created by entering the name, selecting the category and zone, the entering the status and indicating if active or not in the fields provided
    * If the creation is successful, then the 'Create Test Passed' for that Device ID is updated to 'TRUE', otherwise 'FALSE'
* READ
    * After the device is created, the details are read and displayed on the zone details page
    * If the read is successful, then the 'Read Test Passed' for that Device ID is updated to 'TRUE', otherwise 'FALSE'
* UPDATE
    * The created device is edited by appending the text 'EDITED' at the end of the name and status, selecting a random category and zone, toggling is the is active field
    * If the update is successful, then the 'Update Test Passed' for that Device ID is updated to 'TRUE', otherwise 'FALSE'
* DELETE
    * The created device is then finally deleted by auto-clicking the delete icon for that row on the zones home page
    * If the deletion is successful, then the 'Delete Test Passed' for that Device ID is updated to 'TRUE', otherwise 'FALSE'

All the above updates of the test results are stored in the TestResults datatable. After all the test data has been processed, the 'Test Results' sheet of the excel file is updated with the test results datatable as indicated below, assuming that all tests passed.

<img src="tests_after_excel_data.png" width="500px" style="display: inline-block; margin: 0 auto; max-width: 300px" />
<p><sup></sup><em>Figure 7: The image above shows the test results sheet after all categories has been processed successfully and the Excel file updated accordingly</em><sub></sub></p>


<a name="cont"></a>
## 6. Contributors
* [Chipo Hamayobe (37016776)](https://github.com/ChiefMonk) - Project Lead

<a name="refs"></a>
## 7. References
### Software Testing
* [Testing in .NET](https://learn.microsoft.com/en-us/dotnet/core/testing/)
* [Test Driven Development](https://deviq.com/practices/test-driven-development)
* [Unit testing best practices with .NET Core and .NET Standard](https://learn.microsoft.com/en-us/dotnet/core/testing/unit-testing-best-practices)
* [Unit testing C# in .NET Core using dotnet test and xUnit](https://learn.microsoft.com/en-us/dotnet/core/testing/unit-testing-with-dotnet-test)
* [What is User Acceptance Testing (UAT)? Examples](https://www.guru99.com/user-acceptance-testing.html)
* [What Is User Acceptance Testing (UAT): A Complete Guide](https://www.softwaretestinghelp.com/what-is-user-acceptance-testing-uat/)
* [User Acceptance Testing and the Application Lifecycle](https://www.red-gate.com/simple-talk/development/dotnet-development/user-acceptance-testing-application-lifecycle/)
* [What is Automation Testing? Test Tutorial](https://www.guru99.com/automation-testing.html)
* [Automated software testing](https://www.atlassian.com/continuous-delivery/software-testing/automated-testing)
* [Connected Office: Device Management](https://connectedoffice-devicemanagement.azurewebsites.net/)
* [CMPG-323-IOT-Device-Management](https://github.com/JacquiM/CMPG-323-IOT-Device-Management)


### Robotic Process Automation (RPA) with UiPath
* [UiPath Website](https://www.uipath.com)
* [Robotic Process Automation (RPA)](https://www.uipath.com/rpa/robotic-process-automation)
* [Introduction to RPA and Automation (Course)](https://academy.uipath.com/courses/introduction-to-rpa-and-automation)
* [UI Automation with UiPath](https://docs.uipath.com/studio/docs/ui-automation)
* [Excel Automation with UiPath Studio](https://www.uipath.com/learning/video-tutorials/excel-datatables-automation)
* [UiPath Automation Cloud Account](https://platform.uipath.com)
* [Introduction to UiPath Portal, Orchestrator & Studio](https://www.youtube.com/watch?v=BAYmmUuB2Zo)
* [How to Calculate and Update Data within an Excel Workbook in UiPath](https://www.youtube.com/watch?v=-w8rorapLS8)
* [UIPath read excel and enter the data into web forms](https://www.youtube.com/watch?v=lw6bxrMNzfM)
* [How to Automate a Website Login with UiPath Studio](https://www.youtube.com/watch?v=030dEAB8oyg)
* [UiPath - Use Application/Browser Activity| Modern Activity in UiPath | Open Browser & Application](https://www.youtube.com/watch?v=s1InnQCymPA)
* [UiPath Community Forums: Find A Chapter](https://community.uipath.com/chapters/)
* [How to Open Browser and Login with UiPath - Full Tutorial](https://www.youtube.com/watch?v=wk2PBLU3mg0)
* [UiPath RPA Beginners Tutorial - 2020](https://www.youtube.com/watch?v=3ZKzTHdpsTs)
* [How to get the entire row based on the cell value in UiPath](https://forum.uipath.com/t/how-to-get-the-entire-row-based-on-the-cell-value-in-uipath/193445/3)
* [UiPath Studio: Your First Process Automation](https://www.youtube.com/watch?app=desktop&v=OyQAhrcBr9U)




---
parser: v2
author_name: Chaitanya Priya Puvvada
author_profile: https://github.com/chaitanya-priya-puvvada
auto_validation: true
time: 25
tags: [ tutorial>intermediate , software-product>sap-business-technology-platform, software-product>document-information-extraction, topic>artificial-intelligence, tutorial>free-tier]
primary_tag: software-product>sap-build-process-automation
---

# Create an Automation to Extract Invoice Details
<!-- description --> Extract invoice document using Document Extraction Template to send the invoice details to the process

## Prerequisites
 - Complete the tutorial on creating an [Invoice Approval Process](spa-dox-create-process)
 - [Install and Setup the Desktop Agent](spa-setup-desktop-3-0-agent)
 - Download the [Invoice Document](invoice.pdf) to your local machine

## You will learn
  - How to extract data using Document Extraction Template
  - How to bind parameters between process and automation

---

### Create automation


1. In the process **Get Invoice Details**:
    - Choose **+**,
    - Select **Automation**,  **New Automation**.

    <!-- border -->![Automation](001.png)

2. A pop up will appear to configure the Desktop Agent version. Do the following in the pop up:
    - From the dropdown, select the version of the Desktop Agent installed on your machine.
    - Choose **Confirm**.

    > It would be with suffix as **Registered**.

    <!-- border -->![Automation](002.png)

3. A new pop-up will appear to create the automation. Do the following in the pop-up:

    -  Enter **Name** of the automation: **Extract Invoice Data**,
    -  Enter **Description** of your choice,
    -  Choose **Create**.    

    <!-- border -->![Automation](003.png)

    An automation **Extract Invoice Data** will be created successfully.

    <!-- border -->![Automation](004.png)


### Create data types


1. Go to the **Overview** Tab. Choose the **Create** button. Create an artifact of the type **Data Type**.

    <!-- border -->![Automation](005.png)

2. A new pop-up will appear:
    - Enter **Name** of the data type: **Invoice**,
    -  Enter **Description** of your choice,
    - Choose **Create**.

    <!-- border -->![Automation](006.png)

3.  In the Data Type **Invoice** add new fields as following:

    |  Field Name     | Type
    |  :------------- | :-------------
    |  `DocumentNumber`| String
    |  `GrossAmount`   | Number
    |  `SenderName`    | String

    <!-- border -->![Automation](007.png)

4. Choose **Save**.

    <!-- border -->![Automation](008.png)


### Create input and output parameters


    Input and output parameters allow you to exchange data in the workflow of your automation between activities, screens, and scripts.

1. Go to the **Overview** tab. Open **Extract Invoice Data** Automation.

    <!-- border -->![Automation](009.png)

2.  In **Automation Details**, select the **Input/Output** section.

    <!-- border -->![Automation](010.png)

3. Add Input and Output parameters.

    <!-- border -->![Automation](012.png)

4. Edit Input and Output parameters as follows:

    |  Parameter Name       | Data type        | Parameter Type | Description
    |  :---------------     | :-------------   | :------------- | :---------------
    |  `FilePath`      | String     | Input          | Please provide the full qualified path to the PDF file containing the invoice
    |  `InvoiceDetails`    | Invoice| Output         | Extracted Invoice Details

    <!-- border -->![Automation](011.png)

3. Choose **Save**.    


### Create document template


1. Go the **Overview** Tab. Choose **Create** and **Document Template**.

    <!-- border -->![Automation](013.png)

2. In the **Add Document Template** window, under **Start**:
    - Choose **Create a new template**,
    - Enter the **Name** of the template,
    - Upload the invoice document which you have downloaded from prerequisites,
    - Choose **Next**.

    <!-- border -->![Automation](014.png)

3. Under **Enter Details**:
    - Enter the **Name** of the template,
    - Upload the invoice document which you have downloaded from prerequisites,
    - Choose **Next**.

    <!-- border -->![Automation](042.png)

4. Select **Invoice** as the document type of your template and choose **Next**.

    <!-- border -->![Automation](015.png)

5. Under **Choose Schema**:
    - Choose **New**.

    <!-- border -->![Automation](016.png)

6. Under **Create New Schema**:
    - Enter **Invoice Schema Name** such as `ABCSchema`.
    - Choose **Next**.

    <!-- border -->![Automation](045.png)

7. Under **Define information to extract**:
    - Select the **Add** option to add **Header Fields**. For this scenario you will be adding `documentNumber` of Type String, `grossAmount` of Type Number and `senderName` of Type String.

    <!-- border -->![Automation](044.png)
    
    - Choose **Next**.

8. Under **Summary**:
    - SAP Build provides the summary of all the details related to the schema to be created,
    - Choose **Add**.

    <!-- border -->![Automation](043.png)

9. Document Information Extraction SDK would be added as dependency to your project. The schema and template are created successfully.

10. Once Upload will be completed, choose **Open Template Editor**.

    <!-- border -->![Automation](017.png)



### Annotate and activate the document template


1. Choose **Refresh**

    <!-- border -->![Automation](019.png)

2. Choose **Edit**.

    <!-- border -->![Automation](021.png)

3. Select the data in your invoice document which you would like to extract the information. In this scenario, you will read the Document Number, Gross Amount and Sender Name.
    - Select the value  **174221** in the document and map to the field `documentNumber`. Choose **Apply**.

        <!-- border -->![Automation](022.png)

    - Select the value **ABC Communication** in the document and map to the field `senderName`. Choose **Apply**.

        <!-- border -->![Automation](023.png)

    - Select the value **220.00** in the document and map to the field `grossAmount`. Choose **Apply**.

        <!-- border -->![Automation](024.png)

4. Once mapping is done. Choose **Save** and **Close** the template.

    <!-- border -->![Automation](025.png)


### Build the automation


1. Navigate back to **Build Process Automation** and select **Extract Invoice Data** automation tab.

    <!-- border -->![Automation](026.png)

2. In Automation Details, under Tools, in search field, search for **Extract data (Template)** activity.

    > You can extract data with Document Information Extraction using the chosen document template and given PDF file.

    <!-- border -->![Automation](027.png)

3. Drag and drop the activity **Extract Data (Template)** into the automation flow.

    <!-- border -->![Automation](028.png)

4. Select the activity. Choose **Add Document Template**

    <!-- border -->![Automation](046.png)

5. In the **Add Document Template** window:

    - Select **Choose a template from the current project**,
    - Choose **Next**.

    <!-- border -->![Automation](047.png)

6. Under **Select Template**:

    - Choose the `ABCSchema_1` template, you created in the previous steps,
    - Choose **Next**.

    <!-- border -->![Automation](048.png)

7. Under Summary, choose **Add**.

    <!-- border -->![Automation](049.png)

8. Select the activity. Maintain the parameters for the activity as follows:

    - Under `documentPath`: choose `FilePath`

    <!-- border -->![Automation](029.png)

9. You have already created the data type **Invoice** in Step 2. Now, you will create a variable of type **Invoice**.

10. Click on the canvas. Search for the datatype **Invoice**, located under the **Data Types** section.

    <!-- border -->![Automation](030.png)

11. Drag and drop the data type **Invoice** into the automation flow.

    <!-- border -->![Automation](031.png)

12. Select **Create Invoice variable**. In the Input Parameters, under value, choose **Create Custom Data**.

    <!-- border -->![Automation](032.png)

13. Choose the Edit button to map the parameters:
    - `DocumentNumber` to the extracted invoice data from the activity Extract Data (template),
    - Repeat the same for `GrossAmount` and `SenderName` and map it to the corresponding fields of `extractedData`.

    <!-- border -->![Automation](033.png)

14. Rename the output parameter to `myInvoiceData`.

15. The final input and output parameters of **Create Invoice Variable** looks as below.

    <!-- border -->![Automation](034.png)

16. Print the invoice data using the activity **Log message**.

    >  With this activity you generate a log message within the tester and the trace file, which is useful for setting up an automation. By default, a log will be "Information".

17. Click on the canvas, search for **Log Message** activity and drag and drop it into the automation flow.

    <!-- border -->![Automation](035.png)

18. Select **Log Message** activity. In Input Parameters under message add `myInvoiceData` value.

    <!-- border -->![Automation](036.png)

19. Select **Save**.



### Passing the parameters outside the automation


1. Select the **End**. Pass the variable `myInvoiceData` to the output parameter `InvoiceDetails`, which you have created in Step 2.

    <!-- border -->![Automation](037.png)

2. **Save** the automation.


### Mapping of parameters to the automation and process


1. Navigate to the **Get Invoice Details** process and select the automation **Extract Invoice Data**. Map the input parameter of the automation to the form parameter `FilePath`.

    <!-- border -->![Mapping](040.png)

2. Select **Save**.


### Test the automation


1. Select Test button and enter the `Filepath` where the invoice document is stored locally on your machine.

    <!-- border -->![Test](038.png)

2. The automation opens the Invoice Document, extracts data and prints the details i.e Document number, Gross amount and Sender name.

    <!-- border -->![Test](039.png)

3. Your automation is built successfully.

4. Once this tutorial is completed, the process will look like this:

    <!-- border -->![Mapping](041.png)



---

# udx-compliance-specification

This repository contains the UDX NGSI-LD Test Suite, used to verify the compliance of Context Brokers(Data Plane) with
the UDX (Unified Data Exchange) NGSI-LD API Specification.

## Contents

<details>

<summary><strong>Details</strong></summary>

- [Install the Test Suite](#install-the-test-suite)
- [Configure the test suite](#configure-the-test-suite)
- [Execute the NGSI-LD Test Suite](#execute-the-ngsi-ld-test-suite)
- [Frameworks and libraries used in the project](#frameworks-and-libraries-used-in-the-project)
- [Useful links](#useful-links)
- [LICENSE](#license)

</details>

## Install the Test Suite

## Configure the test suite

The first operation that you have to clone the Repository on your own machine and follow the following steps:

Import environment file i,e ```IS 18003 Part 3-  UDX - Resource Access Service.postman_environment.json ``` in postman

#### Steps to Import an Environment File in Postman

* **Open Postman**
    * Launch the Postman application on your computer or open the Postman web version in your browser.
  <div style="text-align: center;">
  <img src="./docs/envImport.png" />
    </div>

    * Go to the Environments Section
        * Click on the **Environments** button (gear icon) in the top-right corner of the Postman interface.
        * Navigate to the **Import** Option
        * On the Postman home page, look for the **Import** button and click on it.
        * You can find it in the top-left corner of the interface, near the **New** button.
* **Choose the File**
    * A pop-up window will appear with multiple import options. Select the **File** tab
  <div style="text-align: center;">
  <img src="./docs/choose_file.png"/>
    </div>

    * Click the **Upload Files** button and browse your system to locate the environment file (.json format).
    * Once you've located the file, select it and click **Open** or **Choose** (depending on your operating system).

* **Import the File**

  <div style="text-align: center;">
  <img src="./docs/Verify_and_import.png" />
    </div>

    * After selecting the file, Postman will display its name and details.
    * Click the **Import** button to proceed.
* **Verify the Imported Environment**
    * Once imported, the Environment will appear in the **Environment** tab on the left-hand side of the Postman
      interface.
    * Click on it to view or edit its key-value pairs.

<div style="text-align: center;">
  <img src="./docs/env_key_values.png" />
    </div>

In the `IS 18003 Part 3-  UDX - Resource Access Service.postman_environment.json` file, configure the following
parameters:

| Key                 |                                                                             Value Example                                                                             | Description                           |
|:--------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:--------------------------------------|
| auth-url            |                                                                           authvertx.iudx.io                                                                           | URL of DX Auth Server                 |
| baseUrl             |                                                                          https://rs.iudx.io                                                                           | URL of DX Resource Server             |
| secureResourceToken | eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.<br/>eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.<br/>SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c | Jwt token issued by the Dx auth sever |
| openResourceToken   | eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.<br/>eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.<br/>SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c | Jwt token issued by the Dx auth sever |
| enabled             |                                                                              true/false                                                                               | Enable or disable the key             |

Import collection file i,e ```IS 18003 Part 3-  UDX - Resource Access Service.postman_collection.json ``` in postman

#### Steps to Import a Collection File in Postman

* **Open Postman**
    * Launch the Postman application on your computer or open the Postman web version in your browser.
  <div style="text-align: center;">
  <img src="./docs/collectionImport.png" />
    </div>

    * Go to the Environments Section
        * Click on the **Environments** button (gear icon) in the top-right corner of the Postman interface.
        * Navigate to the Import Option
            * On the Postman home page, look for the **Import** button and click on it.
            * You can find it in the top-left corner of the interface, near the **New** button.

* **Choose the File**
    * A pop-up window will appear with multiple import options. Select the **File** tab.

   <div style="text-align: center;">
  <img src="./docs/choose_collection.png"/>
    </div>

    * Click the **Upload Files** button and browse your system to locate the collection file. Supported file types
      include **.json** and **.postman_collection.**
    * Once you've located the file, select it and click **Open** or **Choose** (depending on your operating system).

* **Import the File**

  <div style="text-align: center;">
  <img src="./docs/import_Collection.png" />
    </div>

    * After selecting the file, Postman will display its name and details.
    * Click the **Import** button to proceed.
* **Verify the Imported Collection**
  <div style="text-align: center;">
  <img src="./docs/veriry_and_import_collection.png" />
    </div>

    * Once imported, the Environment will appear in the **Collections** tab on the left-hand side of the Postman
      interface.
    * Expand the collection to view its requests and folders.

## Execute the NGSI-LD Test Suite

There are several ways to run a Postman collection, with some of the commonly used methods mentioned below:

### Steps to Run APIs Individually

<div style="text-align: center;">
  <img src="./docs/single_run.png" />
    </div>

* **Open Postman**
    * Launch the Postman application on your computer or access the Postman web interface.
* **Go to the Collections Tab**
    * On the left-hand sidebar, click the **Collections** tab.
    * Expand the collection containing the API request you want to run.
* **Select the API Request**
    * Locate the desired API request within the collection.
    * Click on the request name to open it in the main request editor.
* Choose an Environment
    * select the appropriate environment from the Environment dropdown in the top-right corner of the interface.
* **Verify Request Details**
    * Review the request details in the editor, including the following:
        * Method (e.g., GET, POST, PUT).
        * URL: Ensure it is correct and complete.
        * Headers: Verify or modify if needed.
        * Body: For POST/PUT requests, check the payload (if applicable).
* **Send the Request**
    * Click the "Send" button located near the top of the Postman interface.
    * Postman will execute the request and display the response in the Response section below.

### Step to Run APIs Using Postman Collection Runner

<div style="text-align: center;">
  <img src="./docs/runner.png" />
    </div>

* **Open Postman**
    * Launch the Postman application on your computer or access the Postman web interface.
* **Go to the Collections Tab**
    * On the left-hand sidebar, click the **Collections** tab.
    * Select the desired collection
    * Configure the options such as **iterations**, **environment**, and **delay**, then click **Run** to execute.

### Specific test requirements

- In G3 (Subscription), components 085a, 087a,089a 091a, and 093a require a data broker (RabbitMQ). Ensure RabbitMQ is
  installed and running for proper functionality.

### Installation


### Restore Elasticsearch Indices Using Elasticdump

#### Prerequisites

Ensure you have **Node.js** installed, then install `elasticdump` globally using npm:

```sh
npm install -g elasticdump
```

## Download Mapping and Data Files

Use the following command to download the mapping and data files from Google Drive:

```sh
wget --no-check-certificate 'https://docs.google.com/uc?export=download&id=1hbmrSFUzo068EuLpYc1hFAneruIm-5Ge' -O chandigarh-5b7556b5-0779-4c47-9cf2-3f209779aa22-mapping.json
wget --no-check-certificate 'https://docs.google.com/uc?export=download&id=1rQc1cFAjwZbTZPoGltcTnrZtpbZWfl9_' -O chandigarh-5b7556b5-0779-4c47-9cf2-3f209779aa22-data.json
wget --no-check-certificate 'https://docs.google.com/uc?export=download&id=15zbAkp8pX0IMfuxxowVMQVj1PmynQp6E' -O surat-8b95ab80-2aaf-4636-a65e-7f2563d0d371-mapping.json
wget --no-check-certificate 'https://docs.google.com/uc?export=download&id=1GOEP5_O6ac7GkF0QkRnrM5kW8EEmLMaa' -O surat-8b95ab80-2aaf-4636-a65e-7f2563d0d371-data.json
```

Above commands will download Surat and Chandigarh mappings with data json files.

## Restoring the Indices

Replace `<TARGET_HOST>`, `<USERNAME>`, `<PASSWORD>`, and `<TARGET_INDEX>` accordingly.
Ensure the password is **URL-encoded**.

### Step 1: Restore Mappings

```sh
elasticdump \
  --input=https://<USERNAME>:<URLENCODED_PASSWORD>@<TARGET_HOST>/<TARGET_INDEX> \
  --output=<MAPPINGS-JSON-FILE-PATH> \
  --type=mapping
```

### Step 2: Restore Data

```sh
elasticdump \
  --input=https://<USERNAME>:<URLENCODED_PASSWORD>@<TARGET_HOST>/<TARGET_INDEX> \
  --output=<DATA-JSON-FILE-PATH> \
  --type=data
```

### Example Usage

```sh
elasticdump \
  --input=surat-8b95ab80-2aaf-4636-a65e-7f2563d0d371-mapping.json \
  --output=https://user:password@database.iudx.io:24034/surat-restore \
  --type=mapping

elasticdump \
  --input=surat-8b95ab80-2aaf-4636-a65e-7f2563d0d371-data.json \
  --output=https://user:password@database.iudx.io:24034/surat-restore \
  --type=data
```

Ensure that `<USERNAME>` and `<PASSWORD>` are **URL-encoded if it contains special characters** before use.



This should display the restored mappings and data.



## Frameworks and libraries used in the project

## Useful links

## LICENSE

Copyright 2024 IUDX Programme Unit, Society of Innovation and Development, Indian Institute of Science, Bangalore

The content of this repository and the files contained are released under the [Apache License](LICENSE) a
(Apache License 2.0).



# udx-compliance-specification

This repository contains the UDX NGSI-LD Test Suite, used to verify the compliance of Context Brokers(Data Plane) with
the UDX (Unified Data Exchange) NGSI-LD API Specification.

## Contents

<details>

<summary><strong>Details</strong></summary>

- [Data sets](#data-sets)
- [Importing the data](#importing-the-data)
- [Install the Test Suite](#install-the-test-suite)
- [Configure the test suite](#configure-the-test-suite)
- [Execute the NGSI-LD Test Suite](#execute-the-ngsi-ld-test-suite)
- [Frameworks and libraries used in the project](#frameworks-and-libraries-used-in-the-project)
- [Useful links](#useful-links)
- [LICENSE](#license)

</details>

## Data sets
#### Transit Management DataSet
**Example :-** 
```
{
  "trip_direction":"UP",
  "trip_id":"15308692",
  "route_id":"104U",
  "trip_delay":128,
  "last_stop_arrival_time":"14:40:45",
  "actual_trip_start_time":"2020-11-28T14:38:35+05:30",
  "vehicle_label":"M74",
  "observationDateTime":"2020-11-28T14:42:09+05:30",
  "speed":12,
  "license_plate":"GJ05BX3983",
  "last_stop_id":"1003",
  "location":{"coordinates":[72.843017,21.192156],"type":"Point"},
  "id":"83c2e5c2-3574-4e11-9530-2b1fbdfce832"
}
```
<u>**Description :-**</u>
| **Attribute**               | **Description**  |
|-----------------------------|-----------------|
| **trip_direction**          | **dataSchema:** Text — The direction in which the vehicle is travelling. ENUM[UP,DN]. |
| **trip_id**                 | **dataSchema:** Text — Trip ID/Trip name allotted to the bus corresponding to this observation. |
| **route_id**                | **dataSchema:** Text — Route ID assigned to the route on which the bus corresponding to this observation is plying on. |
| **trip_delay**              | **dataSchema:** Number — This can be positive and negative in seconds and shows how much the vehicle deviates from the planned one. **unitCode:** SEC, **unitText:** second. |
| **last_stop_arrival_time**  | **dataSchema:** DateTime — MM. |
| **vehicle_label**           | **dataSchema:** Text — User visible label, i.e., something that must be shown to the passenger to help identify the correct vehicle. |
| **actual_trip_start_time**  | **dataSchema:** DateTime — This field specifies the time at which bus service actually began for the trip corresponding to this observation. |
| **observationDateTime**     | **dataSchema:** DateTime — The time at which the vehicle was last tracked. |
| **speed**                   | **dataSchema:** Number — The Speed of the bus observed at the last tracked coordinates. **unitCode:** KMH, **unitText:** kilometre per hour. |
| **license_plate**           | **dataSchema:** Text — Vehicle registration number/license plate number of the bus corresponding to this observation. |
| **last_stop_id**            | **dataSchema:** Text — Stop ID/Stop name of the previous bus stop corresponding to the bus in this observation. |
| **location**                | **dataSchema:** Point — The coordinates for the current position of the bus corresponding to this observation. |



<u>**Queryable Attributes :-**</u> 
| **Attribute**               | **Description**  |
|-----------------------------|-----------------|
| **trip_direction**          | Used for attribute query|
| **trip_id**                 | Used for attribute query|
| **route_id**                | Used for attribute query| 
| **last_stop_arrival_time**  | Used for attribute query|
| **vehicle_label**           | Used for attribute query|
| **actual_trip_start_time**  | Used for attribute query|
| **observationDateTime**     | Used for temporal query|
| **speed**                   | Used for attribute query|
| **license_plate**           | Used for attribute query|
| **last_stop_id**            | Used for attribute query|
| **location**                | Used for spatial query |
---------------------------------------------------------

#### Air Quality Management DataSet
**Example :-** 
```
{
  "currentLevel":1.16,
  "measuredDistance":14.74,
  "referenceLevel":15.9,"id":"b58da193-23d9-43eb-b98a-a103d4b6103c","observationDateTime":"2020-09-22T18:30:00+05:30",
  "deviceInfo":
    {
      "deviceID":"FWR055"
    }
  }
```
<u>**Description :-**</u>
| **Attribute**           | **Description**  |
|-------------------------|-----------------|
| **currentLevel**        | **dataSchema:** Number — Current flooding level indicated by the sensing station corresponding to this observation, computed using referenceLevel and measuredDistance (currentLevel = referenceLevel - measuredDistance). **unitCode:** MTR, **unitText:** meter. |
| **measuredDistance**    | **dataSchema:** Number — The distance measured by the sensor, from the sensor tip to the upper surface of water. **unitCode:** MTR, **unitText:** meter. |
| **referenceLevel**      | **dataSchema:** Number — Reference setting used to compute the currentLevel. **unitCode:** MTR, **unitText:** meter. |
| **observationDateTime** | **dataSchema:** DateTime — Last reported time of observation. |




<u>**Queryable Attributes :-**</u> 
| **Attribute**           | **Description**  |
|-------------------------|-----------------|
| **currentLevel**        | Used for attribute query |
| **measuredDistance**    | Used for attribute query |
| **referenceLevel**      | Used for attribute query |
| **observationDateTime** | Used for temporal query |


## Importing the data
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
wget --no-check-certificate 'https://docs.google.com/uc?export=download&id=1AKFDYFUzlohFwE117irrPJAdjZwh_USl' -O chandigarh-5b7556b5-0779-4c47-9cf2-3f209779aa22-data.json
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


## Install the Test Suite

1. **Install Postman Application:**
    - On Windows
        - Open a web browser and visit the [Postman Download Page](https://www.postman.com/downloads/).
        - Click on the Download button for your system (e.g., Windows x64 ). The website usually detects your operating
          system automatically, but you can manually select the appropriate version if needed.
        - The Postman setup file (e.g., Postman-win64-setup.exe) will start downloading.
        - Once the download is complete, go to the folder where the file was saved (usually the Downloads folder).
        - Double-click the downloaded Postman-win64-setup.exe file to start the installation process.
        - The installer will launch, and Postman will start installing automatically. No manual steps are required
          during the installation.
        - Wait for the installation process to complete.
        - After installation, Postman will launch automatically. If it doesn’t, you can find it in the Start Menu or on
          your Desktop.
    - On Ubuntu
        - Most Ubuntu distributions come with Snap pre-installed.
        - To verify, run this command in your terminal:
          `snap --version `
        - If Snap is not installed, install it with:`sudo apt update` `sudo apt install snapd `
        - Run the following command in your terminal: `sudo snap install postman`
        - Once installed, you can check if Postman is available by running: `snap list postman`
        - Open Postman from your application menu, or run: `postman`
2. **Clone the Repo:**
    - Pre-requisites
        - Install Git:
            - If Git is not already installed, download and install it from Git's official website or use the following
              commands:
          ```
          $ sudo apt update         
          $ sudo apt install git
          ```
        - On Windows, install Git via the official installer or package manager.
        - Run the following command to check if Git is installed: `git --version`
3. **Clone a Repository**
    - Go to the repository on your Git hosting platform (
      i.e., https://github.com/datakaveri/udx-compliance-specification).
    - Click the Code or Clone button.
    - Copy the repository's HTTPS (
      i.e., https://github.com/datakaveri/udx-compliance-specification.git)
    - Open a Terminal or Command Prompt
    - Navigate to the directory where you want to clone the repository using the cd command (e.g.,
      `cd /path/to/your/desired/folder`).
    - Use the following command to clone the repository: `git clone <repository-url>`
        - Replace <repository-url> with the copied URL, i.e.:
          `git clone https://github.com/datakaveri/udx-compliance-specification.git`

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
        * Click on the **Environments** button (gear icon) in the top-left corner of the Postman interface.
        * Navigate to the **Import** Option
        * On the Postman home page, look for the **Import** button and click on it.
        * You can find it in the top-right corner of the interface, near the **New** button.
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

    * Go to the Collections Section
        * Click on the **Collections** button (gear icon) in the top-left corner of the Postman interface.
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

    * Once imported, the Collection will appear in the **Collections** tab on the left-hand side of the Postman
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




## Frameworks and libraries used in the project

## Useful links

## LICENSE

Copyright 2024 IUDX Programme Unit, Society of Innovation and Development, Indian Institute of Science, Bangalore

The content of this repository and the files contained are released under the [Apache License](LICENSE) a
(Apache License 2.0).



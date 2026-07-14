# Darea Mails Management

## Overview

**Darea Mails Management** is an engineering project built in **UiPath** for automating e-mail-driven operations in a Shopify-based e-commerce environment. The robot reads incoming e-mails, identifies the requested action, extracts the required data, and executes business operations such as product creation, product update, product deletion, order fulfillment, and status handling. The project is configured as a **Windows / C# UiPath process** with `Main.xaml` as the main entry point. 

The main goal of the solution is to reduce manual work related to handling store operations sent by e-mail and to improve process consistency, reporting, and error handling.

---

## Main Features

- Reading and classifying incoming e-mails
- Processing product-related requests received by e-mail
- Adding new products to the Shopify store
- Editing existing products
- Deleting products
- Fulfilling orders based on provided shipping data
- Updating processing status and generating reports
- Supporting retry logic for failed records
- Maintaining process traceability through reports

---

## Process Flow

The robot is organized as a state-based process with the following logical stages:

1. **Prepare Environment**  
   Initializes the process, loads configuration, prepares variables, and sets up required resources.

2. **Mail Management**  
   Reads messages from the configured mailbox, extracts message details and attachments, and builds the input structure for further processing.

3. **Mail Processing**  
   Executes the main business logic by running the appropriate workflow depending on the request type.

4. **Global Handling**  
   Handles exceptions, logs errors, and decides whether the process should retry or terminate.

5. **Final State**  
   Saves the results, updates reports, and closes the process safely.

---

## Project Structure

Example workflows used in the project:

- `Main.xaml` – main process entry point
- `Read_Config.xaml` – loads configuration values
- `Prepare_environment.xaml` – prepares the runtime environment
- `Mail_management.xaml` – reads and classifies e-mails
- `Read_input_file.xaml` – reads report or input file data
- `Add_New_Products.xaml` – adds products to Shopify
- `Edit_Products.xaml` – edits existing products
- `Delete_Products.xaml` – deletes products
- `Order_Fulfillment.xaml` – fulfills orders
- `Status_Process.xaml` – handles status-related operations
- `Final_State.xaml` – final reporting and process closing
- `Kill_All_Process.xaml` – closes selected applications/processes

---

## Technologies

- **UiPath Studio**
- **Windows project profile**
- **C# expressions**
- **Excel / Workbook activities**
- **Mail activities**
- **UI Automation**
- **Shopify Admin web interface**

The project currently uses UiPath packages such as Excel, Mail, Microsoft 365, System, UI Automation, and Integration Service activities. Some dependencies are configured as preview packages in the project metadata. :contentReference[oaicite:1]{index=1}

---

## Configuration

The process accepts the `in_config_Path` input argument, which points to the configuration file used by the robot. The entry-point metadata currently defines this as the main input for the process. 

Typical configuration areas include:

- mailbox settings
- folder names
- report paths
- input file paths
- Shopify credentials
- retry limits
- process names to kill
- error screenshot paths

### Important
Before running the robot, make sure to:
- update all local file paths,
- verify mailbox and Shopify credentials,
- avoid storing real passwords directly in project files if the project is shared publicly.

---

## How It Works

1. The robot starts from `Main.xaml`.
2. Configuration is loaded.
3. The mailbox is checked for new requests.
4. The message content is analyzed to determine the requested action.
5. Data is extracted from the message body and/or attachments.
6. The correct workflow is triggered depending on the scenario:
   - add product
   - edit product
   - delete product
   - fulfill order
   - update order/product status
7. A report is updated after processing each record.
8. The process ends with final reporting and cleanup.

---

## Reporting and Recovery

The project uses Excel-based reporting to track processed items and their statuses.  
This makes it easier to:

- identify completed records,
- retry failed records,
- avoid reprocessing items already handled successfully,
- continue work after an interruption.

A recommended approach is to treat the report as the current process state, updating record statuses after each processed item.

---

## Running the Project

1. Open the project in **UiPath Studio**.
2. Restore all dependencies.
3. Configure the path to the config file.
4. Verify that required folders, reports, and input files exist.
5. Run `Main.xaml`.

---

## Notes

- The project is intended for educational / engineering thesis purposes.
- It focuses on practical automation of e-commerce support processes.
- The solution can be extended with better retry handling, stronger checkpoint logic, and more secure credential management.

---

## Possible Improvements

- replace preview packages with stable versions
- move credentials to secure assets / credential manager
- improve checkpointing and recovery after failures
- standardize status values across all reports
- reduce duplicated UI logic between workflows
- add unit-like validation for input data before processing

---

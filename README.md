# Data Extraction from PDF Invoices

This project is for extracting data from pdfs and comparing them in csv format

## Overview

- `TestDataSet`folder contains the PDFs
- `Extracted_json_files`folder contains extracted .json files.
- `invoice.csv` file is the actual output.
- `extractalldata.py`  extracts the JSON files from the PDFs
- `jsontocsv_converter.py` generates the `invoice_data.csv` file containing the extracted invoice data from the json files

## Requirements

### To run this project, I have used the following dependencies:

- Python 3.9
- Adobe PDF Services API credentials (json file)
- Required Python packages (specified in the code)
- Sample Code SDK

## Installation

1. Clone the repository to your local machine:
```bash
  git clone https://github.com/Sayan2908/PapyrusH_Sayan.git
```


2. Navigate to the project directory:
```bash
  cd PapyrusH_Sayan
```


3. Install the required Python packages:
```bash
  pip install -r requirements.txt
```


## Usage

1. The PDF files are in the `TestDataSet` folder.

2. Update the `pdfservices-api-credentials.json` file with your Adobe PDF Services API credentials.

3. Run the below script to extract data from PDFs in the TestDataSet folder and generate JSON files:
```bash
  python extractalldata.py
```
This will extract the JSON files from the PDFs, process the data, and store it in the `Extracted_json_files` folder

4. Run the script to convert JSON files to CSV format:
```bash
  python jsontocsv_converter.py
```
This will generate the `invoice_data.csv` file containing the extracted invoice data from the json files.


## Algo:

- In `extractalldata.py` I have used the adobe PDF Extraction API to extract data from all the pdfs by looping through them one by one in the `TestDataSet` folder and containing them in a zip file I have also extracted the json internally cause it appears that the API returns a compressed version of the jsons.
- In `jsontocsv_converter.py` I have used different  ways to extract the data from json:
  1. Like the Invoice_description I got it using the **`Bounds`** attribute as it appeared to have similar bounds in all the json files
  2. I extracted the text data from the **`Text`** attribute of various elements
  3. Text data may have whitespaces so I removed them
  4. I defined proper variables to store the data as the column indexes
  5. Some things like the name of the shop and street were constant so I removed them and made a new list.
  6. According to the pattern the name was the first element so that got sorted out
  7. The text element containing '@' in it is the email
  8. The $ sign and address were also extracted in the similar way as above
  9. The date format and mobile number format helped in extracting texts with that same format using 're' library in python
  10. After removing the data already collected iterate through the filtered list to extract transaction items, quantities, and rates.

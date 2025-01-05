# generate_valid_rcode_list.py

# Overview

The generate_valid_rcode_list.py script generates a list of valid R-codes from PanelApp databases and keeps this list up to date. This list is critical for validating R-codes when running the main web application (app.py). Before launching the web application, you must ensure this script has been run at least once so that a fresh list of valid R-codes is available.

This script is located inside the PanelGeneMapper directory in the root of the project:
	
	root_directory/
	└── PanelGeneMapper/
	    └── generate_valid_rcode_list.py

## What Does generate_valid_rcode_list.py Do?

-	Locate the PanelApp Database: It searches the project’s directories for a subdirectory containing at least one PanelApp SQLite database file (named panelapp_v*.db).

-	Check for New Database Versions: It determines whether there’s a new (unprocessed) version of the database by comparing the file name to a record of previously processed databases.

-	Extract Relevant Disorders: If a new database is found, the script connects to it and retrieves all unique values from the relevant_disorders field in the panel_info table.

-	Append Disorders to the Output File: These unique values (valid R-codes) are appended to an output text file (avoiding duplicates).

-	Logs Activities: The script writes logs for both general INFO messages and ERROR messages to separate log files.

## Why Is It Run Periodically?

The script is designed to run in an infinite loop so it can periodically check for new database versions that might appear. When a new version is detected, it automatically updates the list of valid R-codes.
	
-	By default, the script sleeps for 1 month (2678400 seconds) between each run.

-	If a new version of the database appears in the meantime, the script will process it in the next iteration.

## How to Change the Run Frequency

The frequency is controlled by the line (line 491) in generate_valid_rcode_list.py:

	time.sleep(2678400)  # Wait for 1 month before the next iteration

To change how often it runs, modify the integer value (in seconds):

-	For example, to run every day, change it to time.sleep(86400).

-	For every hour, time.sleep(3600).

## Requirements

PanelApp Database

You must have at least one valid PanelApp SQLite database file named panelapp_v*.db somewhere within the project’s directory structure. The script will look for a directory containing these files.

## How to Run the Program

Open a Terminal in the root of your project (where the PanelGeneMapper folder resides).

Execute the script:

	python PanelGeneMapper/generate_valid_rcode_list.py


Once the program starts, your current terminal will be blocked as long as the script is running. It continuously loops, only sleeping between runs.

-	If you want to continue working on other tasks in your command line, open a new terminal.

-	To stop the script, press CTRL + C in the terminal where it’s running. This will terminate the process.

## Logs and Output Files

### Log Files:
	
-	logs/generate_valid_rcode_list.log (records INFO-level and above messages)
 
-	logs/generate_valid_rcode_list_error.log (records ERROR-level messages)
 
### Output Directory: output/

-	The main output file for valid R-codes is unique_relevant_disorders.txt. Each new unique R-code is appended here (duplicates are skipped).

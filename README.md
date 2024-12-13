# README for generate_valid_rcode_list.py

## Overview

The generate_valid_rcode_list.py script is designed to monitor a directory containing PanelApp database files (.db) for creation or modification events. It automatically generates a list of unique relevant disorders (R codes) from the database and appends them to an text output file. The script also processes any existing database in the directory upon startup.


## Usage

1.	Run the Script:

Start the script in the background:

	python /path/to/generate_valid_rcode_list.py &

Example:

	python /home/miladadmin/Y2_Genepanel_project/PanelGeneMapper/generate_valid_rcode_list.py &


2.	Stop the Script:

Find the process ID (PID) of the script:

	ps aux | grep generate_valid_rcode_list.py

Kill the process:

	kill -9 <PID>


3.	View Logs:

Logs are stored in the logs directory:

	/logs/generate_valid_rcode_list.log


4.	Output File:
   
The output file (unique_relevant_disorders.txt) is located in the generate_valid_rcodes_output directory.



## Example Output

•	Log File (generate_valid_rcode_list.log):

	2024-12-13 16:00:00 [INFO] Logging setup complete.
	2024-12-13 16:00:05 [INFO] Monitoring has started. You can continue using the terminal.
	2024-12-13 16:05:10 [INFO] New database detected: panelapp_v20241210.db
	2024-12-13 16:05:12 [INFO] Connected to the database.
	2024-12-13 16:05:12 [INFO] Found 150 unique disorders.
	2024-12-13 16:05:13 [INFO] Disorders appended to unique_relevant_disorders.txt.


•	Output File (unique_relevant_disorders.txt):

	R211
	R141
	R58
	...


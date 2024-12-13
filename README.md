# README for generate_valid_rcode_list.py

## Overview

The generate_valid_rcode_list.py script is designed to monitor a directory containing PanelApp database files (.db) for creation or modification events. It automatically generates a list of unique relevant disorders (R codes) from the database and appends them to an output file. The script also processes any existing database in the directory upon startup.

Features
	1.	Directory Monitoring:
	•	Watches the directory for new or modified PanelApp database files.
	•	Automatically processes any valid .db file detected.
	2.	Initial Run:
	•	Processes existing database files in the directory on the first run.
	3.	Output Management:
	•	Generates a file containing a list of unique relevant disorders (unique_relevant_disorders.txt).
	•	Appends new disorders to the output file without overwriting existing data.
	4.	Logging:
	•	Logs detailed events and errors to a log file (generate_valid_rcode_list.log).
	•	Logs are configurable and display warnings in the console for user awareness.
	5.	Background Monitoring:
	•	Runs in the background, allowing the user to continue using the terminal.


Usage
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

How It Works
	1.	Startup Behavior:
	•	On the first run, the script processes any existing database in the directory matching the pattern panelapp_v*.db.
	•	Generates the logs and generate_valid_rcodes_output directories if they do not exist.
	2.	Monitoring Behavior:
	•	Watches the directory for creation or modification of .db files.
	•	When a new or modified .db file is detected:
	•	Reads the database using sqlite3.
	•	Extracts unique relevant disorders from the panel_info table.
	•	Appends the disorders to the unique_relevant_disorders.txt file.
	3.	Logging:
	•	Logs all events (e.g., file detections, database connections, errors) to the generate_valid_rcode_list.log file.
	•	Displays warnings and errors in the console.

Error Handling
	1.	No Database Found:
	•	If no database is found at startup, the script waits for file creation/modification events.
	2.	File Locking:
	•	Ensures safe handling of files using FileLock to avoid conflicts during simultaneous operations.
	3.	Exception Logging:
	•	Errors are logged to the log file with detailed information.

Customization
	1.	Change the Monitored Directory:
	•	Update the find_panelapp_directory function to locate the target directory.
	2.	Log Levels:
	•	Modify the setup_logging function to adjust the verbosity of logs.
	3.	File Patterns:
	•	Update the PanelAppEventHandler.is_relevant_file method to monitor different file patterns.

Troubleshooting
	1.	Script Doesn’t Run:
	•	Ensure all dependencies are installed.
	•	Verify that the script has execution permissions:

chmod +x /path/to/generate_valid_rcode_list.py


	2.	No Output in unique_relevant_disorders.txt:
	•	Ensure there are valid .db files in the target directory.
	•	Check the log file for any errors.
	3.	Excessive Debug Logs:
	•	Adjust the logging level in setup_logging (set logger.setLevel(logging.INFO)).
	4.	Stopping a Background Process:
	•	Use ps aux to locate and terminate the process as explained in the Usage section.

Example Output
	•	Log File (generate_valid_rcode_list.log):

2024-12-13 16:00:00 [INFO] Logging setup complete.
2024-12-13 16:00:05 [INFO] Monitoring has started. You can continue using the terminal.
2024-12-13 16:05:10 [INFO] New database detected: panelapp_v20241210.db
2024-12-13 16:05:12 [INFO] Connected to the database.
2024-12-13 16:05:12 [INFO] Found 150 unique disorders.
2024-12-13 16:05:13 [INFO] Disorders appended to unique_relevant_disorders.txt.


	•	Output File (unique_relevant_disorders.txt):

Disorder1
Disorder2
Disorder3
...

This guide should cover all essential aspects of the script. If you have further questions, feel free to ask!

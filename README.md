## Guidance on how to setup update_valid_rcode_list to run every six month

The current working directory structure required to run the scripts generate_valid_rcode_list.py and update_valid_rcode_list.py is as follows:

        .
        ├── app.py
        ├── environment.yml
        ├── PanelApp_extract_data
        │   ├── archive_databases
        │   │   ├── panelapp_v20240918_185155.db.gz
        │   │   ├── panelapp_v20241018_184656.db.gz
        │   │   └── panelapp_v20241118_184158.db.gz
        │   ├── config.json
        │   ├── Extract_data_guidance.md
        │   ├── panelApp_extract_data.py
        │   └── panelapp_v20241218_185252.db
        ├── Patient_db
        │   ├── patient_database.db
        │   └── Patient_db_creation.py
        ├── requirement.txt
        ├── static
        │   ├── index.html
        │   ├── script.js
        │   └── style.css
        └── valid_rcodes
            ├── generate_valid_rcode_list.py
            ├── update_valid_rcode_list_guidance.md
            └── update_valid_rcode_list.py

### Note: After integration with the rest of the team’s code, this directory structure may change accordingly. Please ensure to update the directory structure in this documentation to reflect those changes.

### Step 1: Configure Environment Settings

1.	Disable automatic activation of the base environment:

        conda config --set auto_activate_base false

	-	This prevents Conda from automatically activating the base environment each time you open a new shell or source .bashrc.
	-	After running this command, reload the shell configuration to apply the changes:

        	source ~/.bashrc


2.	Set Nano as the default editor:

        echo 'export EDITOR=nano' >> ~/.bashrc

	-	This makes Nano the default editor, which is useful for editing files and crontab.

3.	Reload the configuration:

        source ~/.bashrc

### Step 2: Prepare for Cron Job Setup

1.	Locate the Python interpreter path:

        which python

	-	Note down the output, as you’ll need it for the cron job setup.

2.	Open the crontab editor:

        crontab -e

	-	The editor should open in Nano since we set it as the default editor.

### Step 3: Configure Cron Job for Automated Database Generation

1.	Add the following cron job to run the script every five minutes (for testing purposes):

        0 0 1 */6 * <path_to_python> <path_to_script>/update_valid_rcode_list.py

	-	Replace <path_to_python> with the path from which python.
	-	Replace <path_to_script> with the full path to update_valid_rcode_list.py

2.	Save and exit the crontab editor:
 
	-	Press Ctrl+X, then Y, then Enter to save.

### Step 4: Disable the Cron Job (if needed)

-	To stop the cron job without deleting it, open the crontab editor:

    	crontab -e


-	Add a # at the beginning of the cron job line to comment it out:

    	# 0 0 1 * * <path_to_python> <path_to_script>/panelApp_extract_data.py


-	Save and exit.


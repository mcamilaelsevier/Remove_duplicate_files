## RESEARCH OUTPUT DATA CLEANING SCRIPT

This Python script is designed to help clean up research output data by removing duplicate file information in the `electronicVersions` section for each research output in the Pure system.

### Adjusting the Script

The script can be adjusted to remove duplicate content information based on specific needs. In this case, it focuses on removing duplicate files associated with electronic versions of research outputs.

### Usage

1. **Prerequisites**:
   - Python installed on your system.
   - `requests` library installed (`pip install requests`).
   
2. **Script Overview**:
   - The script retrieves research output data in batches, processes each item, and removes duplicate file information for electronic versions.

3. **Adjusting for Duplicate Removal**:
   - To adjust the script for different duplicate removal needs:
     - Modify the filtering logic in the `update_research_output` function.
     - Update the `filtered_versions` list based on the specific criteria for removing duplicates.

4. **Running the Script**:
   - Replace the placeholder `Your URL` with your Pure URL in the script.
   - Run the script to clean up research output data and remove duplicate electronic version files.

### Note
This script focuses on removing duplicate files in the `electronicVersions` of research outputs. Adjust the filtering logic as needed to handle other types of duplicate content information.

import requests
import time

# API endpoint and headers
base_url = "https://<Your_URL>/ws/api" # Replace with your Pure URL
headers = {
    "api-key": "<Your_ApiKey>", # Replace with your API Key
    "Content-Type": "application/json"
}

# Function to update research outputs with filtered file names for 'FileElectronicVersion'
def update_research_output(uuid, filtered_versions):
    url = f"{base_url}/research-outputs/{uuid}"
    payload = {
        "electronicVersions": filtered_versions
    }
    response = requests.put(url, headers=headers, json=payload)

    if response.status_code == 200:
        print(f"Research output with UUID {uuid} successfully updated.")
    else:
        print(f"Failed to update research output with UUID {uuid}. Status code:", response.status_code)


# Make multiple GET requests to retrieve research outputs in smaller batches
offset = 101  # Initial offset
batch_size = 100  # Number of items to retrieve in each batch

while True:
    response = requests.get(f"{base_url}/research-outputs?size={batch_size}&offset={offset}", headers=headers)
    
    if response.status_code == 200:
        data = response.json()
        items = data.get('items', [])

        if not items:
            print("No more items to process. Exiting...")
            break

        for item in items:
            time.sleep(1)  # Introduce a delay of 1 second between processing each item
            if item is None:
                print("Found a None item. Printing JSON:")
                print(item)
                print(f"{base_url}/research-outputs?size={batch_size}&offset={offset}")
                print("Skipping...")
                continue

            if 'uuid' not in item:
                print("Research output does not have a UUID. Skipping...")
                continue

            uuid = item.get('uuid')
            electronic_versions = item.get('electronicVersions', [])
            
            filtered_versions = []
            file_names_set = set()

            for version in electronic_versions:
                if version.get('typeDiscriminator') == 'FileElectronicVersion':
                    if 'fileName' in version.get('file', {}):
                        file_name = version['file'].get('fileName')
                        if file_name not in file_names_set:
                            file_names_set.add(file_name)
                            filtered_versions.append(version)
                else:
                    filtered_versions.append(version)

            if len(filtered_versions) < len(electronic_versions):  # Check if duplicates were removed
                update_research_output(uuid, filtered_versions)

        offset += batch_size  # Update offset for the next batch

    else:
        print("Failed to retrieve research outputs. Status code:", response.status_code)
        break

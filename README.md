# pyzamzar

Python SDK for the Zamzar file conversion API

## Installation

```bash
pip install pyzamzar
```

## Usage

### Obtain your API key

[Create an account](https://developers.zamzar.com/pricing), [log in](https://developers.zamzar.com/login) and obtain your API key [here](https://developers.zamzar.com/user)

### Initialize Zamzar client

```python
from zamzar import ZamzarClient

client = ZamzarClient('YOUR_API_KEY')
```

### Start conversion job

Example:

```python
job_info = client.start_conversion_job('README.md', 'pdf')
job_id = job_info['id']
```

### Poll job status until its completion

Example:

```python
while True:
    job_status = client.get_job_status(job_id)
    if job_status['status'] == 'successful':
        break
    elif job_status['status'] == 'failed':
        print("Conversion failed.")
        return
    else:
        print("Conversion in progress. Please wait...")
```

### Download converted file(s)

Example:

```python
file_id = job_status['target_files'][0]['id']
client.download_converted_file(file_id, 'readme.pdf')
print("File downloaded successfully as 'readme.pdf'.")
```

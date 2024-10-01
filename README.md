# Flash Downloader - A Multi-Threaded File Downloader

A command-line interface (CLI) tool that enables fast and efficient downloading of files through multithreading. This tool is designed to optimize download speeds by concurrently downloading different segments of the file, and provides an easy method to transfer files across devices using a QR code.

## Key Features

- **Multithreading:** Downloads different parts of the file simultaneously, significantly reducing overall download time.
- **Network Resilience:** Automatically detects unstable network connections, with capabilities to pause and resume downloads as needed.
- **Device Transfer via QR Code:** Easily transfer downloaded files to other devices within the same network by scanning a QR code.
- **Progress Tracking:** Includes a visual progress bar to monitor download status in real-time.

## Installation

Clone the repository and set up the downloader:

```bash
git clone https://github.com/manavukani/flash-downloader
cd flash-downloader
pip3 install -r requirements.txt
chmod +x downloader.py
```

## How to Use

Run the tool using the following command format:

```bash
./downloader.py <URL> -c <nThreads> --filename <fileName>
```

- `nThreads` and `fileName` are optional arguments.

### Example Usage

```bash
./downloader.py "https://farm8.staticflickr.com/7281/8874270432_8f4a146b57_o.jpg"
```

- If `--filename` is not specified, the script automatically determines the file extension from the URL.

Alternatively, you can simplify the command syntax by renaming `downloader.py` to `downloader`:

```bash
./downloader <URL> -c <nThreads> --filename <fileName>
```

Note: Renaming the script might affect the ability to run predefined unit tests.

## Unit Tests

Execute the following command to run unit tests:

```bash
python3 test_downloader.py
```

## Implementation Details

The downloader implements a consumer-producer model using a synchronized queue. Tasks are divided among threads, each responsible for downloading and assembling a specific segment of the file to ensure efficient use of network resources and quick recovery in case of interruptions.

- **Task Allocation:** Tasks are assigned coalesced file regions to optimize data continuity in case of interrupted downloads.
- **Resilience to Network Issues:** If a thread encounters a network issue, the task is requeued for another attempt, ensuring robustness against network instability.
- **Progress Bar Synchronization:** A shared progress bar updates through a semaphore, allowing accurate and thread-safe reporting.

## Credits

File transfer feature is implemented using [qr-filetransfer].
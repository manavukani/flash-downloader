# **Multithreaded File Downloader (I call it Flash ⚡)**

A Python-based CLI tool for downloading files using multiple threads. This tool supports fast and efficient downloads by splitting files into chunks and downloading them concurrently. It also includes an optional feature to generate a QR code for transferring the downloaded file to an external device over a local network.

---

## **Features**
- **Multithreaded Downloads**: Download files faster by using multiple threads.
- **Resilience to Network Errors**: Automatically retries failed chunks due to network interruptions.
- **Progress Bar**: Visual feedback on download progress.
- **QR Code Transfer**: Generate a QR code to transfer the downloaded file to your phone or another device (optional).
- **Customizable**: Set the number of threads, output filename, and more via command-line arguments.

---

## **Installation**

1. **Prerequisites**:
   - Python 3.x
   - Required Python libraries: `requests`, `progress`, `mimetypes`

   Install the required libraries using pip:
   ```bash
   pip install -r requirements.txt
   ```

2. **Download the Script**:
   - Clone this repository or download the script:
     ```bash
     git clone https://github.com/manavukani/flash-downloader.git
     cd flash-downloader
     ```

---

## **Usage**

### **Basic Usage**
```bash
./downloader.py <URL> [-c N_THREADS] [--filename OUTPUT_FILE]
```

- **`<URL>`**: The URL of the file to download.
- **`-c N_THREADS`**: Number of threads to use (default: 4).
- **`--filename OUTPUT_FILE`**: Name of the output file (optional).

#### Example:
```bash
./downloader.py https://example.com/largefile.zip -c 8 --filename myfile.zip
```

### **QR Code Transfer**
To enable the QR code feature, set `ENABLE_QR_CODE_DOWNLOADS = 1` in the script. After the download completes, a QR code will be generated for transferring the file to your phone.

---

## **How It Works**
1. **File Splitting**:
   - The file is divided into chunks of size `CHUNK_SIZE` (default: 1 MB).
   - Each chunk is assigned to a thread for downloading.

2. **Multithreaded Download**:
   - Multiple threads download their assigned chunks concurrently.
   - If a thread encounters a network error, it retries the chunk.

3. **Progress Tracking**:
   - A progress bar shows the download progress in real-time.

4. **File Assembly**:
   - Downloaded chunks are written to the correct locations in the output file.

5. **QR Code Generation** (optional):
   - After the download completes, a QR code is generated for transferring the file.

---

## **Limitations**
- No support for resuming user interrupted downloads.
- Limited error handling for disk space, permissions, and invalid URLs.
- QR code feature depends on the external `qr-filetransfer` tool.
- Hardcoded constants may not be optimal for all use cases.

---

## **Contributing**
Contributions are welcome! If you'd like to contribute, please:
1. Fork the repository.
2. Create a new branch for your feature or bug fix.
3. Submit a pull request.

#                                            **InternSG Scraper**

This manual is to guide the users through how to use the internsg.com_search to generate an Internsg job list.


### 1. Set up all essential tools

Before running the code, please follow the demo to complete the steps below to set up all necessary tools.

*Visual Studio Code (VS Code)* → This is a platform that we will use to run the code.

1. [Download Visual Studio Code](https://code.visualstudio.com/download) and open it.
2. Inside the software, download Jupyter and Python in the Extensions view
3. Open the InternSG Job List folder and rename it to InternSG_Job_List
4. Enter the following command into the terminal to create a virtual environment:
   
         python -m venv ./venv.\venv\Scripts\activate
   
6. Click “Select Kernel” and “Python Environments” to choose the kernel called “venv”.
7. Add a code cell. Type print("Hello World!") and run the code.
8. You will see a pop up message. Click “Install” to install the ipykernel package for running the Jupyter notebook in VS Code.
9. Type 'pip install selenium' in the terminal to install Selenium.


*Chrome driver*

Selenium and Chrome Driver are useful for scraping information from the Internet.

- Make sure your Chrome is up to date.
- Download [Chrome Driver](https://googlechromelabs.github.io/chrome-for-testing/#stable).
- If you are using Windows, copy the URL for the *chromedriver win32* or *win64*.
- If you are using a Mac, copy the URL for the *chromedriver mac-x64*.
- Paste the URL in your browser, and a ZIP file will be downloaded automatically.
- Unzip the file and place the entire folder into your C drive.

### 2. Gain a basic understanding of the code

There are seven functions inside the first code cell. The introduction to each function is as follows:

- **create_chrome_driver(headless=True)**
  This function is used to set up Chrome options. It will return a Chrome Driver
  in headless mode. This mode enables the fetching process to be faster.

- **extract_contact_info(detail_soup)**
       


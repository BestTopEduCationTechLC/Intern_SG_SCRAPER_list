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

  This function is used to set up Chrome options. It will return a Chrome Driver in headless mode. This mode enables the fetching process to be faster.

- **extract_contact_info(detail_soup)**

  ![Application instruction](Application_Instructions_figure_1.jpg)

  This function is used to extract the contact information under the Application Instructions section of the job description page. If an email address is found in
  this section, the code will store the email (careers@plexxie.com). Additionally, if there are any links provided in this section, they will be stored for later use.     

-**extract_company_name(detail_soup)**

   ![Application instruction](Application_Instructions_figure_2.jpg)

  This function is used to extract the company name (The Plexxie Global Company Pte Ltd) and its email domain (plexxie.com). 

-**search_for_email(company_name, domain)**

   ![Application instruction](Application_Instructions_figure_8.jpg)

  If the job description page does not contain any email address in the Application Instructions
section, this function will be used. The code will type some keywords, including the company
name and its domain extracted beforehand, to search for the potential emails on Google.
For example, “IGG Singapore Pte Ltd igg.com contact email”. After entering the keywords, there are two ways to fetch the potential email addresses:

1. In the search results, the code will directly extract every email shown, such as “cooperation@igg.com”.

2. The code will select links that contain words such as "Contact", "About", or "Privacy" in the title. For example, the link containing the title “Contact US - GAMERS AT HEART” will be saved. If no relevant links are found, the code will automatically select and store the first three result links. After storing the links, each of them will be visited by the code to search for any email addresses on the page. All found emails will be checked to ensure they belong to the correct domain, such as “@igg.com”. Only the emails that fulfill this requirement will be stored.

-**choose_best_email(email_addresses_list)**

   Now that we have a list of found emails, this function helps select the most appropriate one. There are three situations to determine the best email:
   
   1. If the list contains only one found email, this email will be selected as the best email.
   
   2. A list of around 15 job-related keywords is defined within this function, ranging from most relevant to least relevant, such as “careers”, “jobs”, and “hr”. If the          list has multiple found emails, the code will choose the most relevant one based on these predefined keywords. For example, “jobs.sg@igg.com” would be chosen due to         the presence of the keyword “jobs”.
     
   3. If no email matches any of the keywords, you may need to manually select the most appropriate email from the list of the found emails.

-**save_to_excel(data, filename='Joblist updated to 2025.1.XX.xlsx')**

   ![Application instruction](Application_Instructions_figure_3.jpg)

   This function saves every extracted record into an Excel file. The file includes the above seven columns, which are populated with the extracted data. If the Excel file      “Joblist updated to 2025.1.XX.xlsx” does not exist on your computer, the code will create a new one. Otherwise, it will append new records to the last row of the        existing file.

-**process_batch(start_page, end_page)**
   This is the most important function, utilizing the six previously introduced functions to carryout the entire fetching process. The following outlines the two main       scrapping steps, which will loop until all posts on a specific page are handled.

  ![Application instruction](Application_Instructions_figure_4.jpg) 

   **step 1:** Visit a specific page (e.g., page 66).
            - For each post, check if it is still open for applications.
            - If it is open, check if the position title contains the word “intern” (e.g., “Creative Marketing Intern”).
            - If the title contains “intern”, obtain the post date (for instance, 18 Nov).
            
   **step 2:** If the post fulfils all the requirements mentioned in Step 1, visit the job description page. (For this example, use the link to “Creative Marketing Intern” with the function `create_chrome_driver(headless=True)`.)

   On the job description page:
   
               - Obtain the company name and its domain using the function `extract_company_name(detail_soup)`.
               
               - Check if there is any email provided by the company under the Application Instructions section using the function `extract_contact_info(detail_soup)`.

                  - If an email is found, it will be stored. If no email is available, search for email addresses on Google using the function `search_for_email(company_name, domain)`.
               
               - If emails are found on the Internet, select the most relevant email using the function choose_best_email(email_addresses_list).

               - Finally, append the extracted data to the list and save it into the Excel file using the function save_to_excel(data, filename='Joblist updated to 2025.1.XX.xlsx').

 ### 3. Gain a basic understanding of the code

    To execute the code, click on “Execute Cell”. By default, the code is configured to fetch data from pages 66 and 67: batch_data = process_batch(66, 67).
    
    The entire scraping process takes approximately 6 minutes to complete.

   If your network is fast and your computer has sufficient RAM and CPU power, you may adjust the page load time. The line time.sleep(4) indicates a 4-second wait for the page to load.

      - If you reduce this to time.sleep(1), the fetching process may complete in roughly 4 minutes.
      
         If you want to rerun this code cell, it is advisable to restart the kernel to avoid any interruptions during the next fetching process.

### 4. Understand limitations of the code and possible solutions

   There are three notable limitations in the code:
   
   1. It is possible that sometimes, even if the code can search for email addresses on the Internet, it fails to choose the most relevant one as the best email (the yellow cell) because no email matches the predefined keywords.

       ![Application instruction](Application_Instructions_figure_5.jpg)

   2. There is a chance that no relevant email (the green cell) is found on Google. This can be because the corresponding company does not disclose its emails on the Internet or does not have an official website or social media accounts.

      ![Application instruction](Application_Instructions_figure_6.jpg)
      
   3. In some rare cases, the domain provided on the job description page does not belong to the company (the blue cells), which can lead to incorrect email scraping.
     
      ![Application instruction](Application_Instructions_figure_7.jpg)

   If we encounter these situations, it may be necessary to choose, search for, or double-check the emails ourselves. If you do not want to work manually on this, you may choose to simply delete all the records that contain nothing in the E-mail column by running the second code cell. While this method can save you time, it may result in the loss of part of the records in the job list.

   *made 16 Jan 2025*

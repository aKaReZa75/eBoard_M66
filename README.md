# Quectel M66 GSM Educational Shield

This repository contains all the resources and files related to a custom-designed educational shield based on the **Quectel M66 GSM module**, fully compatible with the **Arduino UNO**.  
The board is tailored for developers and students who want to **learn GSM-based communication**, explore **AT commands**, and work on embedded projects using **C/C++**.

![Quectel M66 Shield](Images/Quectel_M66.png)

> [!IMPORTANT]
> Before sending the board files for PCB fabrication, **always make sure you are using the latest released version** of the project.
> Hardware issues or design flaws might exist in earlier versions and could be fixed in newer releases.
> To avoid costly mistakes and ensure the best performance, always refer to the **[Releases](../../releases)** section, where all known issues, updates, and version-specific notes are clearly documented.

### **M66 GSM Module Pin Mapping**

| **M66 Module** | **Arduino Pin** | **Functionality**                                     |
| :------------: | :-------------: | :---------------------------------------------------- |
|    `Reg_EN`    |        A0       | Enables external 4V regulator powering the GSM module |
|    `GSM_PWR`   |        A1       | Turns the GSM module ON via power key logic           |
|    `GSM_TX`    |        D0       | UART Receive line on microcontroller (GSM Transmit)   |
|    `GSM_RX`    |        D1       | UART Transmit line on microcontroller (GSM Receive)   |

<table>
  <tr>
  <td valign="top">
  
  > [!TIP]  
  > If you're looking to better understand how to navigate and use my GitHub repositories — including exploring their structure, downloading or cloning projects, submitting issues, and asking questions,  
  > everything you need is clearly explained in this video:  
  > [aKaReZa 95 - Programming, Git - PART B](https://youtu.be/zYiUItVFRqQ)  
  > Make sure to check it out!
  
  </td>
    <td width="360" valign="middle" style="padding: 0;">
      <a href="https://youtu.be/zYiUItVFRqQ">
       <img src="https://img.youtube.com/vi/zYiUItVFRqQ/maxresdefault.jpg"
             width="360"
             alt="aKaReZa 95 - Programming, Git - PART B Thumbnail"/>
      </a>
    </td>

  </td>
  </tr>
  <tr>
  <td colspan="2">

  > [!CAUTION]
  > It is absolutely critical that you carefully read every single word of this document, line by line, to ensure you don't miss any details. Nothing can be overlooked.
      
  </td>
  </tr>  
</table>

## Detailed Description
| Aspect               | Description                  |
|----------------------|------------------------------|
| PCB Design Software  | Altium  V24.2.2              |
| PCB Layers           | 2-Layer FR4                  |
| GSM Module           | Quectel M66-FB-03            |

# Resources

> [!TIP]
> The resources are detailed in the sections below.  
> To access any of them, simply click on the corresponding blue link.

- [Altium Library](https://github.com/aKaReZa75/Altium-Library)  
  ---  
   All PCB designs across all repositories and projects are built using this Altium Designer component library. It contains a wide range of verified footprints, schematic symbols, and 3D models, ensuring consistency and accuracy in PCB designs. If you're working on a new PCB, using this library will save you time and minimize errors.

- [PCB & Electronics Design Training](https://github.com/aKaReZa75/PCB)  
  ---  
  This repository is dedicated to **learning PCB design and electronics from scratch**. It covers everything from circuit theory to practical PCB layout techniques, including routing strategies, best practices, and component placement. Whether you're a beginner or an experienced designer, this resource will help you **improve your PCB design skills and create professional-quality boards**.

- [Microcontroller Training](https://github.com/aKaReZa75/Microcontroller)  
  ---  
  This repository offers a comprehensive guide to learning **various microcontrollers** and how to interface them with different shields. You’ll find tutorials on **using and configuring shields**, along with hands-on projects to help you **get your microcontrollers up and running**. Whether you're working with **Arduino, STM32, ESP32**, or others, this resource will help you understand how to integrate these platforms effectively for your projects.

- [AT Commands Guide](./ATCommands.md)
  ---  
  This repository is your go-to reference for working with **AT commands** across GSM communication modules. It features a categorized and searchable collection of common and advanced AT commands with **descriptions, sample responses, and usage scenarios**. Whether you're debugging a modem, sending SMS, or configuring network settings, this guide helps you **master AT commands and streamline module communication in your embedded projects**.

- [Shopping Link](./ShoppingLink.md)  
  ---
  This document provides links to trusted suppliers where you can purchase all the essential components for this project, ensuring quality and reliability.

## Project Videos

```plaintext
Quectel M66
    └── [aKaReZa 110 - GSM Modems]
          ├─ Intro — Mobile networks (2G–4G) and module overview.
          ├─ Modules — Quectel M66, SIMCom features.
          ├─ AT Commands — Setup, communication, signal check.
          ├─ SMS — Sending, receiving, error reporting via AT+CMEE.
          ├─ Voice — Call functionality through AT command set.
          └─ Syntax — `CR`, `NL` role and command sequencing tips.
```
<table style="border-collapse: collapse;">
  <tr>
    <td valign="top" style="padding: 0 10px;">
      <h3 style="margin: 0;">
        <a href="https://youtu.be/w70hpMyDvRU">aKaReZa 110 – Microcontroller, GSM Modems</a>
      </h3>
      <p style="margin: 8px 0 0;">
        Discover how to work with GSM modules and microcontrollers to send SMS, make calls, and connect to mobile networks. This video covers Quectel and SIMCom modules, AT command sequences, SIM status checks, signal strength readings, and voice call setup—ideal for mastering GSM communication in embedded systems.
      </p>
    </td>
    <td width="360" valign="top">
      <a href="https://youtu.be/w70hpMyDvRU">
        <img src="https://img.youtube.com/vi/w70hpMyDvRU/maxresdefault.jpg"
             width="360"
             alt="aKaReZa 110 – Microcontroller, GSM Modems Thumbnail"/>
      </a>
    </td>
  </tr>
</table>
  
# 💻 How to Use Git and GitHub
To access the repository files and save them on your computer, there are two methods available:
1. **Using Git Bash and Cloning the Repository**
   - This method is more suitable for advanced users and those familiar with command-line tools.
   - By using this method, you can easily receive updates for the repository.

2. **Downloading the Repository as a ZIP file**
   - This method is simpler and suitable for users who are not comfortable with command-line tools.
   - Note that with this method, you will not automatically receive updates for the repository and will need to manually download any new updates.

## Clone using the URL.
First, open **Git Bash** :
-  Open the folder in **File Explorer** where you want the library to be stored.
-  **Right-click** inside the folder and select the option **"Open Git Bash here"** to open **Git Bash** in that directory.

![open Git Bash](Images/Step0.png)

> [!NOTE] 
> If you do not see the "Open Git Bash here" option, it means that Git is not installed on your system.  
> You can download and install Git from [this link](https://git-scm.com/downloads).  
> For a tutorial on how to install and use Git, check out [this video](https://youtu.be/BsykgHpmUt8).
  
-  Once **Git Bash** is open, run the following command to clone the repository:

 ```bash
git clone https://github.com/aKaReZa75/eBoard_M66.git
```
- You can copy the above command by either:
- Clicking on the **Copy** button on the right of the command.
- Or select the command text manually and press **Ctrl + C** to copy.
- To paste the command into your **Git Bash** terminal, use **Shift + Insert**.

![Clone the Repository](Images/Step1.png)

- Then, press Enter to start the cloning operation and wait for the success message to appear.

![Open the Library File](Images/Step2.png)

> [!IMPORTANT]
> Please keep in mind that the numbers displayed in the image might vary when you perform the same actions.  
> This is because repositories are continuously being updated and expanded. Nevertheless, the overall process remains unchanged.

> [!NOTE]
> Advantage of Cloning the Repository:  
> - **Receiving Updates:** By cloning the repository, you can easily and automatically receive new updates.  
> - **Version Control:** Using Git allows you to track changes and revert to previous versions.  
> - **Team Collaboration:** If you are working on a project with a team, you can easily sync changes from team members and collaborate more efficiently.  

## Download Zip
If you prefer not to use Git Bash or the command line, you can download the repository directly from GitHub as a ZIP file.  
Follow these steps:  
1. Navigate to the GitHub repository page and Locate the Code button:
- On the main page of the repository, you will see a green Code button near the top right corner.

2. Download the repository:
- Click the Code button to open a dropdown menu.
- Select Download ZIP from the menu.

  ![Download Zip](Images/Step7.png)  

3. Save the ZIP file:
- Choose a location on your computer to save the ZIP file and click Save.

4. Extract the ZIP file:
- Navigate to the folder where you saved the ZIP file.
- Right-click on the ZIP file and select Extract All... (Windows) or use your preferred extraction tool.
- Choose a destination folder and extract the contents.

5. Access the repository:
- Once extracted, you can access the repository files in the destination folder.

> [!IMPORTANT]
> - No Updates: Keep in mind that downloading the repository as a ZIP file does not allow you to receive updates.    
>   If the repository is updated, you will need to download it again manually.  
> - Ease of Use: This method is simpler and suitable for users who are not comfortable with Git or command-line tools.

# 📝 How to Ask Questions
If you have any questions or issues, you can raise them through the **"Issues"** section of this repository. Here's how you can do it:  

1. Navigate to the **"Issues"** tab at the top of the repository page.  

  ![Issues](Images/Step3.png)

2. Click on the **"New Issue"** button.  
   
  ![New Issue](Images/Step4.png)

3. In the **Title** field, write a short summary of your issue or question.  

4. In the "Description" field, detail your question or issue as thoroughly as possible. You can use text formatting, attach files, and assign the issue to someone if needed. You can also use text formatting (like bullet points or code snippets) for better readability.  

5. Optionally, you can add **labels**, **type**, **projects**, or **milestones** to your issue for better categorization.  

6. Click on the **"Submit new issue"** button to post your question or issue.
   
  ![Submeet New Issue](Images/Step5.png)

I will review and respond to your issue as soon as possible. Your participation helps improve the repository for everyone!  

> [!TIP]
> - Before creating a new issue, please check the **"Closed"** section to see if your question has already been answered.  
>   ![Closed section](Images/Step6.png)  
> - Write your question clearly and respectfully to ensure a faster and better response.  
> - While the examples provided above are in English, feel free to ask your questions in **Persian (فارسی)** as well.  
> - There is no difference in how they will be handled!  

> [!NOTE]
> Pages and interfaces may change over time, but the steps to create an issue generally remain the same.

# 🤝 Contributing to the Repository
To contribute to this repository, please follow these steps:
1. **Fork the Repository**  
2. **Clone the Forked Repository**  
3. **Create a New Branch**  
4. **Make Your Changes**  
5. **Commit Your Changes**  
6. **Push Your Changes to Your Forked Repository**  
7. **Submit a Pull Request (PR)**  

> [!NOTE]
> Please ensure your pull request includes a clear description of the changes you’ve made.
> Once submitted, I will review your contribution and provide feedback if necessary.

# 🌟 Support Me
If you found this repository useful:
- Subscribe to my [YouTube Channel](https://www.youtube.com/@aKaReZa75).
- Share this repository with others.
- Give this repository and my other repositories a star.
- Follow my [GitHub account](https://github.com/aKaReZa75).

# 📜 License
This project is licensed under the GPL-3.0 License. This license grants you the freedom to use, modify, and distribute the project as long as you:
- Credit the original authors: Give proper attribution to the original creators.
- Disclose source code: If you distribute a modified version, you must make the source code available under the same GPL license.
- Maintain the same license: When you distribute derivative works, they must be licensed under the GPL-3.0 too.
- Feel free to use it in your projects, but make sure to comply with the terms of this license.
  
# ✉️ Contact Me
Feel free to reach out to me through any of the following platforms:
- 📧 [Email: aKaReZa75@gmail.com](mailto:aKaReZa75@gmail.com)
- 🎥 [YouTube: @aKaReZa75](https://www.youtube.com/@aKaReZa75)
- 💼 [LinkedIn: @akareza75](https://www.linkedin.com/in/akareza75)

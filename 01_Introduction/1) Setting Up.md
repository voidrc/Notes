A key factor in maintaining happiness and motivation is the quality of the working environment. Organizing your workspace to minimize fatigue is essential in any role. Below are some examples of how I have customized my own workspace to better suit my needs.

## **Operating System**
Given my strong interest in gaming, Linux customization (ricing), and my career in cybersecurity, I needed a system that delivers excellent gaming performance out of the box, offers extensive customization options, and supports hacking tools seamlessly.

I chose **CachyOS**, an Arch-based distribution designed with gamers in mind. Thanks to its Arch foundation, it provides access to a vast selection of packages for ricing and customization. Additionally, you can easily add the **BlackArch** repository to Pacman, unlocking over 2,000 hacking and security tools with minimal effort.

## **Browser**
When it comes to web browsers, I personally choose **Firefox** for its robust feature set and reliability. One of its standout advantages is the ability to seamlessly sync bookmarks, extensions, settings, and more across multiple devices. This makes it an excellent choice for maintaining a consistent and personalized browsing experience wherever you go.

#### **Extensions**:

| Name                               | Description                                                                                     |
| ---------------------------------- | ----------------------------------------------------------------------------------------------- |
| `ClearURLs`                        | Removes tracking elements from URLs                                                             |
| `CookieManager`                    | Edit cookies related to the current page and all its CORS frames right from the popup interface |
| `DuckDuckGo Privacy Essantials`    | Enhance your privacy while browsing with DuckDuckGo                                             |
| `Firefox Multi-Account Containers` | Multi-Account Containers helps you keep your online identities separate                         |
| `FoxyProxy`                        | Easy to use advanced Proxy Management tool                                                      |
| `Hack-Tools`                       | The all in one Red Team extensions for web pentesters                                           |
| `OWASP Penetration Testing Kit`    | As name implies testing kit                                                                     |
| `Privacy Badger`                   | Automatically blocks invisible trackers                                                         |
| `Proton Pass`                      | Encrypted Password managment                                                                    |
| `Proton VPN`                       | For secure browsing                                                                             |
| `To Google Translate`              | Highlight text and sent it to translator                                                        |
| `uBlock Origin`                    | An efficient blocker. Easy on CPU and memory                                                    |
| `Wappalyzer`                       | Identifies web technologies                                                                     |
| `Wavback Machine`                  | Time travel                                                                                     |

## **Noting, Logging & Reporting**
Note-taking is an essential aspect of penetration testing, as the process generates a large volume of information, results, and ideas that can be difficult to retain without proper documentation.

1. **Information Gathering and Note-Taking**  
    During penetration testing engagements, we inevitably gather large volumes of diverse information. This requires an adaptable approach, as the data we collect may suggest next steps or reveal new avenues for investigation. At the same time, vulnerabilities or misconfigurations can be easily overlooked if not properly documented. It is therefore essential to develop the habit of recording everything that warrants further examination. Tools such as **Obsidian** and **Xmind** are well suited for organizing and managing these notes effectively.

2. **Managing and Analyzing Results**  
    The outputs from scans and penetration testing activities are often extensive and produced in a short period, which can quickly become overwhelming. Initially, filtering out the most critical findings is challenging and requires practice to develop the ability to identify the essential fragments of information. Despite this, it is important to retain all collected data and results to avoid missing anything significant and to ensure information is available for later analysis. Additionally, these results often serve as the foundation for documentation. Tools like **GhostWriter** and **Pwndoc** can help streamline the documentation process and provide a clear overview of the steps taken during an engagement.

3. **Logging for Documentation and Accountability**  
    Comprehensive logging is vital both for thorough documentation and for legal protection. In the event that a third party attacks the client organization during a penetration test and damage occurs, logs can demonstrate that the activity in question was not related to our testing. Utilities such as `date` and `script` are invaluable here: `date` records precise timestamps for each command, while `script` captures all commands and their output to a background file. I have developed a dedicated script for this purpose, which can be found in the **Scripts** folder under the name **RedLogs**.

4. **Screenshots and Proof of Concept**  
    Screenshots provide clear, moment-in-time evidence of results and are essential for proof-of-concept demonstrations and documentation. However, some processes cannot be fully captured in static images. In these cases, using an application like **Peek** to create animated GIFs offers an effective way to record and present all necessary steps in a concise and accessible format.

## **Virtualization**
Even if we were trained by _Mr. Robot_ himself, we can't expect to be effective in the field without hands-on experience. You might wonder: _If we don’t test in the real world, how do we gain that experience?_ Welcome to the world of **Home Labs**. _(For reference, see the **Home-Lab** folder for a useful tips.)_
  
Home labs play a critical role in cybersecurity training and development. They provide a safe, controlled environment to practice techniques, test tools, and refine workflows without risking unintended consequences on production systems. By building and maintaining a home lab, security professionals can develop practical skills, experiment freely, and deepen their understanding of real-world scenarios.

To get started with a basic home lab setup, you’ll need virtualization software such as **VirtualBox** and/or **Proxmox VE**. Installation guides for these platforms are widely available online for all operating systems.

If you're using **CachyOS** or any other Arch-based distribution, here is a dedicated installation guide for [VirtualBox](VirtualBox.md).

## **Backups and Recovery**
Backups and recovery mechanisms are among the most critical safeguards against data loss, system compromise, and business disruption.

In penetration testing and cyberattack simulations, these systems are evaluated from two perspectives:

- **Protective measures** that can mitigate damage and enable recovery.
    
- **High-value targets** that attackers may attempt to compromise or disable.
    

Assessing their importance means examining how they perform under pressure, the role they play in incident response, and how they have influenced real-world security outcomes—both positively and negatively. The most effective way to gain this understanding is by developing and testing our own backup and disaster recovery strategies.

Recovery processes are equally vital, as they determine how quickly operations can return to normal after an intrusion. As penetration testers, we can simulate scenarios in which systems are locked down or data is stolen, then evaluate both the detection and the speed of recovery. Weak recovery planning can worsen an incident’s impact.

With this in mind, let’s examine a few solutions for implementing effective system backups and reliable recovery methods:

### Pika Backup
Pika Backup is a user-friendly backup solution with a GUI which allows us to create backups locally and remotely. A big advantage is that it doesn’t copy files it already copied. It copies only new files or files that have been modified since the last backup. Additionally it supports encryption which adds another layer of security and its easy to set up.
```bash
# Update
sudo pacman -Syu

# Install Pika Backup
sudo pacman -S pika-backup
```

Once we have started Pika Backup we can setup the backup process and configure it the way we need.

Pika Backup screen showing 'No Backup Configured' with a button to 'Setup Backup'.

Pika Backup uses BorgBackup repositories, which are directories containing (encrypted and) deduplicated archives. Deduplicated archives is a type of data archive where redundant copies can be identified and removed to reduce storage space and improve efficiency. Each data in an archive is split into a smaller chunk and based on its content it is assigned to a unique hash. If a chunk’s hash matches an existing one it will be discarded. In production environments where the host can be access through the internet (e.g. web server) it is recommended to follow the 3-2-1 rule:

    3 copies of your data
    2 on different devices
    1 offsite

Pika Backup setup screen with options to create or use existing repository, showing 'Location on Disk' and 'Remote Location' for both.

We can specify the location where the local repository can be created. In this example, we will use a connected HDD with a directory called backup.

Pika Backup location selection screen showing 'Repository Base Folder' set to 'backup' and 'Repository Name' as 'backup-ubuntu-cry0l1t3' with a 'Continue' button.

Once the directory for the repository is specified, we can setup the encryption phrase that Pika Backup uses in order to encrypt all our archives. The same way as BorgBackup, Pika Backup employs AES-256-CTR encryption which provides high security.

Pika Backup encryption setup screen with 'Use Encryption' toggled to 'Encrypted', showing password fields for new and repeated password, and a 'Create' button.

After the encryption has been set, we can move on and initiate the first backup or dive deeper into the configuration—exploring things such as the schedule, included, and excluded files and directories. In this example, we’re going to backup just the home directory as you can see in the Files to Back up section and exclude all Caches.

Pika Backup screen showing 'Backup Never Ran' with options to back up 'Home' folder and exclude 'Caches', and a 'Back Up Now' button.

For the archives we can specify an archive index of our choice. We also can run the Data Integrity Check manually which checks the latest backup archives with the current status and makes updates if any files has been modified since the last backup.

Pika Backup archives screen showing 'home' directory with 20.4 GB available of 52.5 GB total, options for 'Archive Prefix' and 'Cleanup Archives', and 'No Integrity Check' performed. No archives available.

In the Schedule tab we can specify how often a backup needs to be created. The recommended schedule is to do a backup daily for 2 weeks period.

Pika Backup schedule screen showing 'Waiting for Backup to Start', with options to regularly create backups daily at 21:00, and to regularly clean up archives. 'Save Configuration' button is present.

Once everything is set up, we can launch the backup process and wait until its finished.

Pika Backup screen showing 'Backup Running' at 4.0% for 'home' directory, with options to abort, and lists of files to back up and exclude.

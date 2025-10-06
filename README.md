# Project: Linux Backup and Restore System

A hands-on project demonstrating a complete backup and restore procedure for critical data within a Linux environment. This project uses fundamental Linux commands and archives to ensure data integrity and provide a straightforward recovery path.

## Table of Contents

  * [1. Overview](#1-overview)
    * [Key Objectives:](#key-objectives)
  * [2. Project Files and Structure](#2-project-files-and-structure)
  * [3. Prerequisites](#3-prerequisites)
  * [4. Commands & Implementation](#4-commands--implementation)
    * [1. Setup and Sample Data Creation](#1-setup-and-sample-data-creation)
    * [2. Backup Creation](#2-backup-creation)
    * [3. Data Loss Simulation and Restoration](#3-data-loss-simulation-and-restoration)
    * [4. Verification](#4-verification)
  * [5. Documentation](#5-documentation)
  * [6. Author](#6-author)


## 1. Overview

This repository documents and contains artifacts from a system administration project focused on data protection. The primary goal was to successfully archive a set of critical files, simulate a data loss scenario, and then perform a full data restoration, followed by verification.

### Key Objectives:

* Demonstrate competence in Linux file system navigation and archiving.
* Successfully create full backups using standard Linux tools.
* Verify the integrity and completeness of the restored data.

## 2. Project Files and Structure

The repository contains the data and artifacts generated during the backup and restore process:

| File/Folder                         | Description                                                                                                                          |
|:------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------|
| **`Linux Project Manual.docx`**     | Comprehensive project documentation, including objectives, methods, step-by-step commands, and conclusion. **(Recommended Reading)** |
| **`project_data/`**                 | The simulated **original source directory** containing the files to be backed up.                                                    |
| **`backup_location/project_data/`** | The simulated **backup target directory** where backup archives are stored.                                                          |
| **`project_backup_full.tar.gz`**    | The final, compressed archive of the original source data. This is the complete backup file.                                         |
| **`text_files.tar.gz`**             | A smaller, potentially older or partial backup archive of text-only files.                                                           |
| **`restore_verification.txt`**      | A file created post-restoration to document and verify that the restoration process was successful and the data is intact.           |
| **`home/user/project_data/`**       | A folder created automatically after syncing the backup to the original file after the command rsync.                                |

## 3. Prerequisites

To execute or fully understand the concepts in this project, you need:

* A machine running a **Linux distribution** (e.g., Ubuntu, CentOS, Debian).
* Familiarity with the **Linux command line interface (CLI)**.
* The **`tar`** utility, which is standard on most Linux systems.
* Basic understanding of file permissions and directory structures.

## 4. Commands & Implementation

The project implementation uses standard Linux/Bash commands to complete the backup and restore workflow.

### 1. Setup and Sample Data Creation

This section creates the sample project data structure (~/project_data/) and with various files.

- mkdir -p ~/project_data/{docs, images,config} - Creates the nested directories. 
- echo "..." > ~/project_data/docs/document1.txt - Creates a sample text file. 
- echo "..." > ~/project_data/config/server.conf - Creates a sample configuration file.
- echo "..." > ~/project_data/images/picture1.img - Creates a sample image file placeholder.

### 2. Backup Creation

This section demonstrates three different backup methods.

- tar -czvf project_backup_full.tar.gz ~/project_data/ - Creates a full backup of the project directory, compressing it with gzip (create, zip/gzip, verbose, file). 
- find ~/project_data/ -name "*.txt" -exec tar rvf text_files.tar {} \; - Finds all .txt files and adds them selectively to a new tar archive (remove, verbose, file). 
- gzip text_files.tar - Compresses the selective archive.
- mkdir ~/backup_location - Creates the destination directory for the rsync backup. 
- rsync -av ~/project_data/ ~/backup_location/ - Creates a local mirrored backup (used for incremental strategies) with archive and verbose options.

### 3. Data Loss Simulation and Restoration

This section simulates a data loss and then restores the files from the full backup.

- rm -rf ~/project_data/docs/ - Simulates data loss by force-removing the docs directory recursively.
- tar -xzvf project_backup_full.tar.gz -C ~/ - Restores the full backup archive (xtract, zip/gzip, verbose, file) to the home directory (-C ~/).

### 4. Verification

The final step verifies that the data was successfully restored.

- ls -la ~/project_data/ > ~/restore_verification.txt - Verifies restoration by listing the contents of the restored directory and saving the output to a file for review. 

## 5. Documentation

For a detailed, step-by-step walkthrough, including specific commands, rationales, and output verification, please refer the project manual:
- Linux Project Manual.docx

## 6. Author

- Name: Harika Kada
- Contact: harikakada10@gmail.com
<a name="top"></a>
<div align="center">

# Job Search Assistant

<!-- for testing purpose on vs code -->
<!-- <video src="docs/Job Search Assistant demo.mp4" 
       width="1280" 
       height="720" 
       controls 
       onloadeddata="this.playbackRate = 2">
</video> -->

[job search assistant demo](https://github.com/user-attachments/assets/3cb23ee2-5128-4045-adfb-c90ad5b16611)


**🤖🔍 Your AI-powered job search assistant. Automate applications, get personalized recommendations, and land your dream job faster.**

</div>

[Special thanks](#special-thanks) 
The 
job search assistant is continuously evolving, and your feedback, suggestions, and contributions are highly valued. Feel free to open issues, suggest enhancements, or submit pull requests to help improve the project. Let's work together to make job search assistant a powerful tool for job seekers worldwide.

[Project Management Documentation](docs/project_management.md)
 

## Table of Contents

1. [Introduction](#introduction)
2. [Features](#features)
3. [Installation](#installation)
4. [Configuration](#configuration)
5. [Usage](#usage)
6. [Documentation](#documentation)
7. [Troubleshooting](#troubleshooting)
8. [Conclusion](#conclusion)
9. [Contributors](#contributors)
10. [License](#license)
11. [Disclaimer](#disclaimer)

## Introduction

Job Search Assistant is a cutting-edge, automated tool designed to revolutionize the job search and application process. In today's fiercely competitive job market, where opportunities can vanish in the blink of an eye, this program offers job seekers a significant advantage. By leveraging the power of automation and artificial intelligence, a job search assistant enables users to apply to a vast number of relevant positions efficiently and in a personalized manner, maximizing their chances of landing their dream job.

### The Challenge of Modern Job Hunting

In the digital age, the job search landscape has undergone a dramatic transformation. While online platforms have opened up a world of opportunities, they have also intensified competition. Job seekers often find themselves spending countless hours scrolling through listings, tailoring applications, and repetitively filling out forms. This process can be not only time-consuming but also emotionally draining, leading to job search fatigue and missed opportunities.

### Enter job search assistant: Your Personal Job Search Assistant

Job Search Assistant steps in as a game-changing solution to these challenges. It's not just a tool; it's your tireless, 24/7 job search partner. By automating the most time-consuming aspects of the job search process, it allows you to focus on what truly matters - preparing for interviews and developing your professional skills.

## Features

1. **Intelligent Job Search Automation**
   - Customizable search criteria
   - Continuous scanning for new openings
   - Smart filtering to exclude irrelevant listings

2. **Rapid and Efficient Application Submission**
   - One-click applications
   - Form auto-fill using your profile information
   - Automatic document attachment (resume, cover letter)

3. **AI-Powered Personalization**
   - Dynamic response generation for employer-specific questions
   - Tone and style matching to fit company culture
   - Keyword optimization for improved application relevance

4. **Volume Management with Quality**
   - Bulk application capability
   - Quality control measures
   - Detailed application tracking

5. **Intelligent Filtering and Blacklisting**
   - Company blacklist to avoid unwanted employers
   - Title filtering to focus on relevant positions

6. **Dynamic Resume Generation**
   - Automatically creates tailored resumes for each application
   - Customizes resume content based on job requirements

7. **Secure Data Handling**
   - Manages sensitive information securely using YAML files

## Installation

**Confirmed successful runs on the following:**

- Operating Systems:
  - Windows 10
  - Ubuntu 22
  - macOS
- Python versions:
  - 3.13

## Prerequisites

Before you begin, ensure you have met the following requirements:

### Download and Install Python

Ensure you have the latest Python version installed (Python 3.11 or higher is required for this project). If not, download and install it from Python's official website. For detailed instructions, refer to the tutorials:
- [How to Install Python on Windows](https://docs.python.org/3/using/windows.html)
- [How to Install Python on Linux](https://docs.python.org/3/using/unix.html)
- [How to Download and Install Python on macOS](https://docs.python.org/3/using/mac.html)

### Download and Install Google Chrome

Download and install the latest version of Google Chrome in its default location from the [official website](https://www.google.com/chrome/).

### Install Poetry

Follow the instructions provided on Poetry's [official installation page](https://python-poetry.org/docs/#installation).

### Clone the Repository

```bash
git clone https://github.com/surapuramakhil-org/Job_hunt_assistant.git
cd Job_hunt_assistant
```

#### switching to stable versions

place to find release tags: https://github.com/surapuramakhil-org/Job_search_assistant/releases

```bash
git checkout <tag_name>
```

example:
```bash
git checkout v0.1.0-beta
```

### Setting Up the Project with Poetry

Since the project already includes a `pyproject.toml` file, follow these steps:

#### Install Dependencies

Run the following command in the project directory to install all dependencies specified in `pyproject.toml`:

```bash
poetry install
```

### Create `.env` File

To configure environment variables for the project, create a `.env` file by copying the `.env.template` file provided in the repository. This file will store sensitive information such as API keys and other configuration settings.

```bash
cp .env.template .env
```

After copying, open the `.env` file and fill in the required values. Ensure you do not share this file or commit it to version control, as it contains sensitive information.

### Usage 

0. **Account language**
   To ensure the bot works, your account language must be set to English.

1. **Data Folder:**
   Ensure that your data_folder contains the following files:
      - `secrets.yaml`
      - `work_preferences.yaml`
      - `plain_text_resume.yaml`

   Also, make sure you fill all placeholders. This is important!.

### Configuration
- For basic configuration, refer to [configuration.md](/docs/configuration.md)
- For TensorZero gateway setup, see [tensorzero_setup.md](/docs/tensorzero_setup.md)

2. **Output Folder:**
    Contains the output of the bot.
    - `data.json` results of the --collect mode
    - `failed.json` failed applications
    - `open_ai_calls.json` all the calls made to the LLM model
    - `skipped.json` applications that were skipped
    - `success.json` successful applications

    **Note:** `answers.json` is not part of the output folder and can be found in the root of the project. It is used to store the answers of the questions asked to the user. Can be used to update the bot with corrected answers. Search for `Select an option`, `0`, `Authorized`, and `how many years of` to verify correct answers.

3. **Start Required Services (if applicable):**
    Start TensorZero using Docker Compose before running the main application. Make sure you have added your `OPENAI_API_KEY` to your `.env` file first.
   ```bash
   # Start TensorZero gateway service
   docker compose -f docker-compose-tensorzero.yml up -d
   ```
   Note: The TensorZero gateway handles all LLM connections. See [tensorzero_setup.md](/docs/tensorzero_setup.md) for configuration details.
   Ensure these services are running before proceeding to the next step.

4. **Run the Bot:**

   job search assistant offers flexibility in how it handles your pdf resume:

- **Dynamic Resume Generation:**
  If you don't use the `--resume` option, the bot will automatically generate a unique resume for each application. This feature uses the information from your `plain_text_resume.yaml` file and tailors it to each specific job application, potentially increasing your chances of success by customizing your resume for each position.

   ```bash
   poetry run python src/main.py
   ```

- **Using a Specific Resume:**
  If you want to use a specific PDF resume for all applications, place your resume PDF in the `data_folder` directory and run the bot with the `--resume` option:

  ```bash
  poetry run python src/main.py --resume /path/to/your/resume.pdf
  ```

- **Using the collect mode:**
  If you want to collect job data only to perform any type of data analytics you can use the bot with the `--collect` option. This will store in output/data.json file all data found,

  ```bash
  poetry run python src/main.py --collect
  ```
  
### For troubleshooting refer [this docs](/docs/troubleshooting.md)

### For Developers

- [Lang Chain Developer Documentation](https://python.langchain.com/v0.2/docs/integrations/components/)

- [Workflow diagrams](docs/workflow_diagrams.md)

[Back to top 🚀](#top)

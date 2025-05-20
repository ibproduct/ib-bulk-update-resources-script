# Resource Update Script

This script helps you update resources in IntelligenceBank by reading IDs from a CSV file. It's designed to be easy to use, even if you've never used Python before.

## First Time Setup

### 1. Install Python

#### Windows:
1. Go to [Python Downloads](https://www.python.org/downloads/)
2. Click the big yellow "Download Python" button
3. Run the downloaded installer
4. **Important**: Check the box that says "Add Python to PATH" during installation
5. Click "Install Now"

#### Mac:
1. Open Terminal (press Cmd + Space, type "Terminal", press Enter)
2. Install Homebrew if you don't have it:
   Copy and paste this command:
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

3. Install Python by typing this command:
   brew install python

### 2. Download and Extract the Script
1. Download this script package as a ZIP file
2. Extract it to a folder on your computer (e.g., Desktop)

### 3. Open Terminal/Command Prompt in the Script Folder

#### Windows:
1. Open the folder containing the script
2. Hold Shift and right-click in the folder
3. Select "Open PowerShell window here" or "Open command window here"

#### Mac:
1. Open Terminal (Cmd + Space, type "Terminal", press Enter)
2. Type `cd ` (with a space after cd)
3. Drag the folder containing the script into the Terminal
4. Press Enter

### 4. Install Required Packages
In the Terminal/Command Prompt, run:
Type or copy this command:
pip install -r requirements.txt

### 5. Set Up Configuration
1. Create a copy of the example configuration file:
   For Windows, type:
   copy .env.example .env

   For Mac, type:
   cp .env.example .env

2. Edit the `.env` file with your IntelligenceBank credentials:
   Add your IntelligenceBank login details:
   PLATFORM_URL=your_platform_url
   EMAIL=your_email
   PASSWORD=your_password
   API_V2_URL=your_api_v2_url

   Note: The script will automatically handle getting and updating other required values (API_V3_URL, CLIENT_ID, SID) when you run it.

### 6. Prepare Your Resource IDs
1. Create a file named `list.csv`
2. Add your resource IDs to this file, one per line

## Running the Script

1. Open Terminal/Command Prompt in the script folder (see step 3 above if you closed it)

2. Run the script:
   Type this command:
   python update_resources.py

3. The script will:
   - Log in to IntelligenceBank using your credentials
   - Process your resource IDs (10 at a time)
   - Show progress in the Terminal window
   - Create log files for tracking

## Understanding the Output

### Files Created:
- `update_resources_[date_time].log`: Detailed log of what happened
- `processed_ids.txt`: List of successfully processed IDs
- `errored_ids.txt`: List of IDs that had errors

### Progress Information:
The script shows:
- Number of resources processed
- Current processing speed
- Success and error counts
- Total time taken

## Troubleshooting

### Common Issues:

1. "Python not found" or similar:
   - Make sure you checked "Add Python to PATH" during installation
   - Try restarting your computer

2. "Module not found" errors:
   - Make sure you're in the correct folder
   - Run the pip install command again:
     Type this command again:
     pip install -r requirements.txt

3. Login errors:
   - Double-check your credentials in the .env file
   - Make sure there are no extra spaces
   - Verify your platform URL and API URL

4. "File not found" errors:
   - Make sure list.csv exists in the same folder as the script
   - Make sure it contains resource IDs, one per line

### Need Help?
If you encounter any issues:
1. Check the log file for error details
2. Make sure all credentials in .env are correct
3. Contact support with the log file attached

## Features

- Automatically handles login and session management
- Processes multiple resources at once (10 at a time)
- Limits requests to avoid overloading (600 per minute)
- Can resume if stopped or interrupted
- Tracks errors for easy retry
- Shows real-time progress
- Creates detailed logs

## Security Note

The `.env` file contains your login credentials. Keep it secure:
- Don't share it with others
- Don't commit it to version control
- Keep a backup in a secure location
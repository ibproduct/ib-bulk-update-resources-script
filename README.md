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
   Copy and paste this command into Terminal:
   ```
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```
   
   After installation completes, copy and paste these two commands:
   ```
   (echo; echo 'eval "$(/opt/homebrew/bin/brew shellenv)"') >> ~/.zprofile
   eval "$(/opt/homebrew/bin/brew shellenv)"
   ```

3. Check Python installation:
   ```
   python3 --version
   ```
   If Python is not installed or you see an old version, install/update it:
   ```
   brew install python
   ```
   If you see "python3 is already installed", that's fine - continue to the next step.

4. Install pip:
   First check if pip is already installed:
   ```
   pip3 --version
   ```

   If pip is not found, install it using one of these methods:

   Method 1 - Using easy_install:
   ```
   curl https://bootstrap.pypa.io/ez_setup.py -o ez_setup.py
   python3 ez_setup.py
   easy_install pip3
   ```

   Method 2 - If Method 1 fails with network errors:
   ```
   brew install python3-pip
   ```

   Method 3 - If both above methods fail:
   ```
   sudo python3 -m ensurepip --upgrade
   sudo ln -s /usr/local/bin/pip3 /usr/local/bin/pip
   ```

   Important: On Mac, always use pip3 instead of pip. They are different:
   - pip3 = Python 3.x package installer (what we need)
   - pip = Python 2.x package installer (outdated, don't use)

5. Add pip to your PATH (if needed):
   ```
   echo 'export PATH="$HOME/Library/Python/3.11/bin:$PATH"' >> ~/.zshrc
   source ~/.zshrc
   ```
   Note: Replace 3.11 with your Python version from step 3.

6. Verify installations:
   ```
   python3 --version
   pip3 --version
   ```
   Both commands should show version numbers.

7. If you get network errors:
   Try these fixes:
   - Check your internet connection
   - Try using a different DNS:
     ```
     networksetup -setdnsservers Wi-Fi 8.8.8.8 8.8.4.4
     ```
   - If behind a corporate firewall, you may need to configure proxy settings

### 2. Download and Extract the Script
1. Download this script package as a ZIP file
2. Extract it to a folder on your computer (e.g., Desktop)

### 3. Show Hidden Files

You'll need to see hidden files (like .env) to configure the script.

#### Windows:
1. Open File Explorer
2. Click the "View" tab at the top
3. Check the box for "Hidden items" in the "Show/hide" section

#### Mac:
1. In Finder, press: Command + Shift + . (dot)
   This toggles hidden files on/off
2. You should now see files that start with a dot (.)

### 4. Install a Text Editor

You'll need a good text editor to modify configuration files. We recommend:

- [Visual Studio Code](https://code.visualstudio.com/) (recommended)
  - Free, user-friendly
  - Great for both configuration and Python files
  - Syntax highlighting for better readability
  
- Alternative options:
  - [Sublime Text](https://www.sublimetext.com/)
  - [Notepad++](https://notepad-plus-plus.org/) (Windows only)

Do NOT use:
- Windows Notepad
- TextEdit (Mac)
These basic editors can cause formatting issues.

### 5. Open Terminal/Command Prompt in the Script Folder

#### Windows:
1. Open the folder containing the script
2. Hold Shift and right-click in the folder
3. Select "Open PowerShell window here" or "Open command window here"

#### Mac:
1. Open Terminal (Cmd + Space, type "Terminal", press Enter)
2. Type cd followed by a space
3. Drag the folder containing the script into the Terminal
4. Press Enter

### 6. Install Required Packages

In your terminal window, copy and paste this command:
```
pip3 install -r requirements.txt
```

If you get a permissions error, try:
```
pip3 install --user -r requirements.txt
```

### 7. Configure Your Settings

1. Using your text editor (VS Code recommended):
   - Open the .env.example file
   - Copy its contents
   - Create a new file named .env
   - Paste the contents into .env

2. In the .env file, replace these values with your IntelligenceBank credentials:
   ```
   PLATFORM_URL=your_platform_url
   EMAIL=your_email
   PASSWORD=your_password
   API_V2_URL=your_api_v2_url
   ```

   Note: The script will automatically handle getting and updating other required values.

### 8. Prepare Your Resource IDs
1. Create a file named list.csv
2. Add your resource IDs to this file, one per line

## Running the Script

1. Open Terminal/Command Prompt in the script folder (see step 5 above if you closed it)

2. Copy and paste this command:
   python update_resources.py

3. The script will:
   - Log in to IntelligenceBank using your credentials
   - Process your resource IDs (10 at a time)
   - Show progress in the Terminal window
   - Create log files for tracking

## Understanding the Output

### Files Created:
- update_resources_[date_time].log: Detailed log of what happened
- processed_ids.txt: List of successfully processed IDs
- errored_ids.txt: List of IDs that had errors

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
   - Run the pip3 install command again:
     Copy and paste: pip3 install -r requirements.txt
   - If pip3 is not found, try closing and reopening your terminal

3. Login errors:
   - Double-check your credentials in the .env file
   - Make sure there are no extra spaces
   - Verify your platform URL and API URL

4. "File not found" errors:
   - Make sure list.csv exists in the same folder as the script
   - Make sure it contains resource IDs, one per line

5. Can't see .env file:
   - Make sure you've enabled hidden files (see step 3 above)

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

## Customizing Resource Updates

The script's default configuration is set up to:
1. Clear out auto-generated tags
2. Enable facial recognition
3. Disable other auto-tagging features

You can customize what gets updated by modifying the `payload` variable in `update_resources.py`. Look for this section:

```python
# Payload for the PUT request - THIS IS WHERE YOU CAN MAKE ADJUSTMENTS TO WHAT IS INCLUDED
payload = {
    "data": {
        "tags": [], # Only include as empty if you want to clear out existing tags
        "amaTags": {
            "objects": {
                "autoGen": False,
                "autoGeneratedTags": [], # Only include as empty if you want to clear out existing tags
            },
            "keywords": {
                "autoGen": False,
                "autoGeneratedTags": [] # Only include as empty if you want to clear out existing tags
            },
            "landmarks": {
                "autoGeneratedTags": [], # Only include as empty if you want to clear out existing tags
                "autoGen": False,
            },
            "faces": {
                "autoGeneratedTags": [], # Only include as empty if you want to clear out existing tags
                "autoGen": True
            }
        }
    }
}
```

For full details on available options, see the [IntelligenceBank API Documentation](https://apidoc.intelligencebank.com/#62ff46b9-46ab-4460-a902-427168ab2742).

Common customizations include:
- Setting metadata fields
- Updating permissions
- Modifying tags
- Configuring auto-tagging features
- Setting resource attributes

## Security Note

The .env file contains your login credentials. Keep it secure:
- Don't share it with others
- Don't commit it to version control
- Keep a backup in a secure location
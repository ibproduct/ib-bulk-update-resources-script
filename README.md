# Resource Update Script

This script efficiently updates resources using the provided API endpoint by reading resource IDs from a CSV file. It features concurrent processing, rate limiting, and resume capability.

## Features

- Concurrent processing (10 requests at a time)
- Rate limiting (600 requests/minute)
- Resume capability (tracks processed IDs)
- Error tracking (saves failed IDs for easy retry)
- Progress tracking and performance metrics
- SSL certificate handling for self-signed certificates
- Environment-based configuration

## Prerequisites

- Python 3.x
- Required packages (install using `pip install -r requirements.txt`):
  - aiohttp
  - python-dotenv

## Setup

1. Copy the example environment file and update with your values:
   ```bash
   cp .env.example .env
   ```

2. Edit `.env` with your configuration:
   ```env
   API_V3_URL=your_api_url
   CLIENT_ID=your_client_id
   SID=your_session_id
   ```

3. Place your resource IDs in `list.csv` (one ID per line)

## Usage

1. Run the script:
   ```bash
   python update_resources.py
   ```

2. The script will:
   - Load configuration from .env file
   - Process resource IDs concurrently (10 at a time)
   - Maintain rate limit of 600 requests/minute
   - Create a log file with timestamp (e.g., `update_resources_20250509_123000.log`)
   - Display real-time progress in the console
   - Track successful IDs in `processed_ids.txt`
   - Track failed IDs in `errored_ids.txt`
   - Handle SSL certificate verification automatically

## Environment Variables

Required variables in `.env`:
- `API_V3_URL`: Your API base URL
- `CLIENT_ID`: Your client ID
- `SID`: Your session ID

The script will validate these variables on startup and exit if any are missing.

A `.env.example` file is provided as a template. Never commit your actual `.env` file to version control.

## Tracking Files

1. `processed_ids.txt`:
   - Contains successfully processed resource IDs
   - One ID per line
   - Used to skip already processed IDs on restart

2. `errored_ids.txt`:
   - Contains failed resource IDs
   - One ID per line
   - Can be directly copied into list.csv for retry
   - Error details available in the log file

## Progress Tracking

The script shows real-time progress including:
- Number of resources processed
- Current processing rate (requests/second)
- Success and error counts
- Total elapsed time and average rate

## Log File

The timestamped log file (`update_resources_[timestamp].log`) contains:
- Successful updates (200 OK) with resource IDs
- Errors with resource IDs, status codes, and error responses
- Progress updates with performance metrics
- Summary of total successful updates and errors

## Error Handling

The script handles:
- Missing or invalid environment variables
- SSL certificate verification
- Missing list.csv file
- API request errors
- Rate limiting
- Network issues
- Connection timeouts (30-second timeout per request)

All error details are logged in the main log file, while errored_ids.txt contains only the IDs for easy reprocessing.

## Git Integration

The following files are ignored in .gitignore:
- `.env` (contains sensitive configuration)
- `*.log` (log files)
- `processed_ids.txt` (processing state)
- `errored_ids.txt` (error state)

The `.env.example` file is tracked in git as a template for configuration.
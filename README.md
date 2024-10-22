# Google Sheets to PDF Converter

A Simple App by Jonika Griffin

This tool is part of our mission to improve small business owners' results by 1% with tools that simplify the admin-y stuff. 

By automating the conversion of Google Sheets to PDFs, we help you spend less time on administrative tasks and more time growing your business.

## Features

- Batch processing of Google Sheets files
- Automatic PDF generation with customizable settings
- Progress tracking with time estimates
- Kill switch for stopping long-running processes
- Maintenance routines for log management
- Error handling with automatic retries
- Rate limiting to prevent API quota issues
- Cache management to avoid reprocessing files
- Detailed logging and execution summary

## Prerequisites

Before using this script, you need:

1. A Google account with access to Google Drive and Google Sheets
2. Basic familiarity with Google Apps Script
3. Necessary permissions to access and modify target spreadsheets

## Installation

1. Open [Google Apps Script](https://script.google.com)
2. Create a new project
3. Copy the entire script content into the script editor
4. Save the project with a memorable name (e.g., "Spreadsheet to PDF Exporter")

## Required Manual Setup

You must enable the Drive API before running the script:

1. In the Apps Script editor, look for "Services" in the left sidebar
2. Click the "+" button next to "Services"
3. In the "Add a service" dialog:
   - Search for "Drive API"
   - Select "Drive API" from the list
   - Click "Add"

## Usage

1. Run the initialization:
   ```javascript
   function initializeEverything()
   ```
   This will:
   - Set up required script properties
   - Verify permissions
   - Create necessary log sheets
   - Test API access

2. Once initialization is complete, run the main function:
   ```javascript
   function exportMultipleSheetsToPDF()
   ```

3. Monitor progress in the generated log sheet, which shows:
   - Real-time progress percentage
   - Estimated time remaining
   - Process status
   - Any errors encountered

## Configuration

The script uses these default settings, which can be modified in the script properties:

```javascript
{
    BATCH_SIZE: '10',           // Number of files to process in each batch
    MAX_RETRIES: '3',           // Maximum retry attempts for failed operations
    RETRY_DELAY_MS: '5000',     // Delay between retries (milliseconds)
    CACHE_EXPIRATION: '21600',  // Cache duration (seconds)
    MAX_EXECUTION_TIME: '330000', // Maximum runtime before graceful stop (milliseconds)
    MAX_FILES_TO_PROCESS: '1000', // Maximum files to process in one run
    RATE_LIMIT: '100'          // API calls per minute limit
}
```

## Features Explained

### Kill Switch
- A button in the log sheet allows you to safely stop the script
- Progress is saved when stopped
- Can resume from last processed file

### Progress Tracking
- Real-time progress percentage
- Estimated time remaining
- Color-coded progress indicators
- Detailed logs of processed files

### Error Handling
- Automatic retries with exponential backoff
- Detailed error logging
- Aggregated error reporting
- Maintenance of original file permissions

### Log Management
- Automatic log rotation
- Archive of old logs
- Detailed execution summaries
- Performance metrics

## Limitations

- Maximum execution time of 6 minutes per run (Google Apps Script limitation)
- Default limit of 1000 files per execution (configurable)
- Requires manual Drive API enablement
- Must be run from a Google Apps Script project

## Troubleshooting

Common issues and solutions:

1. **"Drive API is not enabled" Error**
   - Follow the manual setup instructions above to enable the Drive API

2. **Script times out before completion**
   - Reduce `BATCH_SIZE` in script properties
   - Process files in smaller groups
   - Use the resume feature for large sets of files

3. **Permission errors**
   - Ensure you have access to all target files
   - Run `initializeEverything()` to verify permissions

4. **Rate limit errors**
   - Adjust `RATE_LIMIT` in script properties
   - Increase `RETRY_DELAY_MS` for more spacing between retries

## Support

If you encounter issues:
1. Check the execution log in Apps Script
2. Review the generated log sheet
3. Verify all prerequisites are met
4. Ensure the Drive API is enabled

## Contributing

Feel free to fork this script and modify it to suit your needs. If you develop improvements that could benefit others, please consider submitting a pull request.

## License

This project is available under the MIT License.

## Disclaimer

This script is provided "as is", without warranty of any kind. Always test with a small set of files before processing important documents.

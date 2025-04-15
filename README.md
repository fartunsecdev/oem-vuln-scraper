# OEM Vulnerability Scraper

A powerful tool for monitoring critical and high severity vulnerabilities across multiple IT and OT equipment manufacturers. This scraper automatically tracks security advisories from various OEM websites and provides real-time notifications.

## Features

- 🔍 **Multi-OEM Support**: Scrapes security advisories from multiple manufacturers
- ⚠️ **Severity Focus**: Tracks Critical and High severity vulnerabilities
- 📧 **Real-time Notifications**: Sends email alerts for new vulnerabilities
- 📊 **Detailed Reports**: Provides comprehensive vulnerability information
- 💾 **Database Storage**: Maintains historical vulnerability data
- 📝 **CSV Export**: Enables easy reporting and analysis
- ⏰ **Scheduled Scanning**: Runs automatically at configurable intervals
- 🔒 **Secure**: Handles authentication and session management
- 📋 **Logging**: Detailed logging for monitoring and troubleshooting

## Supported OEMs

- Cisco
- Microsoft
- Google (Chrome)
- Siemens
- Schneider Electric
- Rockwell Automation
- ABB
- HPE

## Prerequisites

- Python 3.7 or higher
- pip package manager
- Internet connection
- Email account (for notifications)

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/oem-vulnerability-scraper.git
   cd oem-vulnerability-scraper
   ```

2. Create and activate a virtual environment (recommended):
   ```bash
   python -m venv venv
   # On Windows
   .\venv\Scripts\activate
   # On Linux/Mac
   source venv/bin/activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Configure the environment:
   ```bash
   cp .env.example .env
   # Edit .env with your settings
   ```

## Configuration

Edit the `.env` file with your settings:

```ini
# Email Configuration
SMTP_SERVER=smtp.gmail.com
SMTP_PORT=587
EMAIL_USERNAME=your_email@gmail.com
EMAIL_PASSWORD=your_app_password
RECIPIENT_EMAILS=recipient1@example.com,recipient2@example.com

# Scraping Configuration
SCRAPE_INTERVAL_HOURS=6
LOG_LEVEL=INFO

# Database Configuration
DB_PATH=./vulnerabilities.db
```

### Gmail Setup

For Gmail users:
1. Enable 2-Step Verification in your Google Account
2. Generate an App Password:
   - Go to Google Account > Security > App passwords
   - Select "Mail" and your device
   - Use the generated password in `EMAIL_PASSWORD`

## Usage

### Run as a Service

Start the scraper as a continuous service:
```bash
python main.py
```

### Run Once

Perform a single scan:
```bash
python main.py --run-once
```

### Test Email Configuration

Verify email settings:
```bash
python main.py --test-email
```

### Export to CSV

Export vulnerability data:
```bash
python main.py --export-csv vulnerabilities.csv
```

### Change Scanning Interval

Modify the scanning frequency:
```bash
python main.py --interval 12
```

## Adding New OEM Scrapers

1. Create a new class in `oem_scraper.py`:
   ```python
   @ScraperRegistry.register
   class NewOEMScraper(OEMScraper):
       def __init__(self):
           super().__init__("New OEM", "https://newoem.com/security")
           
       def scrape(self):
           # Implement scraping logic
           return vulnerabilities
   ```

2. Implement the scraping logic:
   - Fetch advisory pages
   - Parse vulnerability data
   - Create Vulnerability objects
   - Handle errors and rate limiting

## Troubleshooting

### Common Issues

1. **No Emails Being Sent**
   - Verify SMTP settings
   - Check email credentials
   - Ensure 2-Step Verification is enabled for Gmail

2. **No Vulnerabilities Found**
   - Check network connectivity
   - Verify OEM websites are accessible
   - Review log files for errors

3. **Scraper Errors**
   - Check `vuln_scraper.log`
   - Verify website structure hasn't changed
   - Ensure all dependencies are installed

### Log Files

- Main log: `vuln_scraper.log`
- Error log: `error.log`
- Database: `vulnerabilities.db`

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

For support, please:
1. Check the [documentation](docs/)
2. Review the [issues](https://github.com/yourusername/oem-vulnerability-scraper/issues)
3. Create a new issue if needed

## Acknowledgments

- Thanks to all contributors
- Inspired by the need for automated vulnerability monitoring
- Built with Python and open-source libraries 

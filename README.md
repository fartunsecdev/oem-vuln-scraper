# oem-vuln-scraper
Automated monitoring of OEM vulnerabilities with compliance mapping


# OEM Vulnerability Scraper

A tool for monitoring critical and high severity vulnerabilities of OEM equipment (IT and OT) published at respective OEM websites and other relevant web platforms.

## Overview

This vulnerability scraper monitors websites of various IT and OT equipment manufacturers for critical and high severity vulnerabilities, reporting them via email in near real-time. The tool helps organizations stay informed about security vulnerabilities in their equipment, allowing for faster response and mitigation.

## Features

- Scrapes multiple OEM websites for vulnerability information
- Focuses on critical and high severity vulnerabilities
- Sends email notifications when new vulnerabilities are discovered
- Provides detailed vulnerability information including mitigation strategies
- Maintains a database of discovered vulnerabilities
- Supports CSV export for reporting
- Runs as a scheduled service or one-time scan

## Supported OEMs

The current version includes scrapers for:

- Cisco
- Microsoft
- Google (Chrome)
- Siemens
- Schneider Electric
- Rockwell Automation
- ABB
- HPE

Additional OEM scrapers can be easily added by creating new classes in the `oem_scrapers.py` file.

## Installation

### Prerequisites

- Python 3.7 or higher
- pip package manager

### Steps

1. Clone this repository:
   ```
   git clone https://github.com/fartunsecdev@gmail.com/oem-vulnerability-scraper.git
   cd oem-vulnerability-scraper
   ```

2. Install the required dependencies:
   ```
   pip install -r requirements.txt
   ```

3. Run the setup script:
   ```
   python setup.py
   ```

4. Configure the `.env` file with your settings (see Configuration section below)

## Configuration

Edit the `.env` file to configure the scraper:

```
# Email configuration
SMTP_SERVER=smtp.gmail.com
SMTP_PORT=587
EMAIL_USERNAME=your_email@gmail.com
EMAIL_PASSWORD=your_app_password
RECIPIENT_EMAILS=recipient1@example.com,recipient2@example.com

# Scraping configuration
SCRAPE_INTERVAL_HOURS=6

# Logging
LOG_LEVEL=INFO
```

### Email Configuration

For Gmail, you'll need to create an App Password:
1. Go to your Google Account settings
2. Enable 2-Step Verification if not already enabled
3. Go to Security > App passwords
4. Create a new app password for "Mail"
5. Use this password in the `EMAIL_PASSWORD` field

## Usage

### Run as a Service

To run the scraper as a continuous service that checks for vulnerabilities at specified intervals:

```
python main.py
```

The scraper will start and run according to the interval specified in the `.env` file or command line arguments.

### Run Once

To run the scraper once and exit:

```
python main.py --run-once
```

### Test Email Configuration

To test if the email configuration is working correctly:

```
python main.py --test-email
```

### Export Vulnerability Database to CSV

To export the vulnerability database to a CSV file:

```
python main.py --export-csv vulnerabilities.csv
```

### Change Scraping Interval

To change the scraping interval (in hours):

```
python main.py --interval 12
```

## Adding Custom OEM Scrapers

To add a scraper for a new OEM:

1. Open `oem_scrapers.py`
2. Create a new class that inherits from `OEMScraper`
3. Implement the `scrape()` method
4. Register the class with the `@ScraperRegistry.register` decorator

Example:

```python
@ScraperRegistry.register
class NewOEMScraper(OEMScraper):
    """Scraper for New OEM security advisories."""
    
    def __init__(self):
        super().__init__("New OEM", "https://newoem.com/security-advisories")
        
    def scrape(self):
        """Scrape New OEM security advisories."""
        logger.info(f"Scraping {self.name} for vulnerabilities")
        
        # Your scraping logic here
        
        return vulnerabilities
```

## Troubleshooting

- **No emails being sent**: Check your SMTP settings and email credentials in the `.env` file
- **No vulnerabilities found**: Verify network connectivity and that the OEM websites are accessible
- **Scraper errors**: Check the `vuln_scraper.log` file for detailed error information

## License

This project is licensed under the MIT License - see the LICENSE file for details. 

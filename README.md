# Zscaler ZIA Custom URL Category Analyzer - OAuth 2.0 Edition

---

**Copyright (c) 2025 ZHERO srl, Italy**  
**Website:** [https://zhero.ai](https://zhero.ai)

This project is released under the MIT License. See the LICENSE file for full details.

## Credits

**Original Script Author:** James Tucker (Zscaler)  
**OAuth 2.0 Implementation:** ZHERO srl  
**Special Thanks:** Joost Hage (Zscaler) for valuable contributions and guidance

---

## Overview

This tool analyzes custom URL categories in Zscaler Internet Access (ZIA) to provide insights into URL coverage and categorization. It's an OAuth 2.0 implementation of the original script by James Tucker from Zscaler.

### Key Features

-   🔐 OAuth 2.0 authentication (modern OpenAPI standard)
-   📊 Analyze URL coverage across custom categories
-   🔍 Identify URLs not categorized by Zscaler
-   📈 Generate categorization statistics
-   📄 Export results to CSV or XLSX (Excel) format
-   🚀 Batch processing for large URL lists

### What This Tool Does

1. Authenticates with Zscaler ZIA using OAuth 2.0
2. Lists all custom URL categories in your environment
3. For selected categories:
    - Shows percentage of URLs in known Zscaler categories
    - Lists URLs NOT defined/categorized by Zscaler
    - Provides category breakdown with counts
    - Exports full results to CSV

This is a modernized version of James Tucker's original `zia_custom_category_analyzer` script, updated to use OAuth 2.0 authentication and the Zscaler OneAPI standards.

## Prerequisites

-   Python 3.6 or higher
-   Zscaler ZIA tenant with API access enabled
-   OAuth 2.0 client credentials (Client ID and Client Secret)
-   Network access to Zscaler API endpoints

## Installation

1. Clone or download this project:

```bash
cd zia-custom-category-analyzer-oauth
```

2. Install required dependencies (eventually use a python venv):

```bash
pip install -r requirements.txt
```

3. Set up your OAuth credentials:

```bash
cp .env.example .env
# Edit .env with your Zscaler OAuth credentials
```

## Configuration

Edit the `.env` file with your Zscaler OAuth 2.0 credentials:

```env
# Zscaler Identity Base URL
# This is your Identity service URL (e.g., https://[YOUR-ID].zslogin.net)
ZSCALER_IDENTITY_BASE_URL=https://[YOUR-ID].zslogin.net

# OAuth Client ID
ZSCALER_CLIENT_ID=your_client_id_here

# OAuth Client Secret
ZSCALER_CLIENT_SECRET=your_client_secret_here
```

### How to Get OAuth Credentials

1. Log in to your Zscaler ZIA admin portal
2. Navigate to **Administration > API Key Management**
3. Create a new API client with appropriate permissions
4. Copy the Client ID and Client Secret

## Usage

### Basic Usage

Run the analyzer:

```bash
python zia_custom_category_analyzer_oauth.py
```

The script will:

1. Authenticate with Zscaler
2. Display all custom URL categories
3. Prompt you to select categories to analyze
4. Ask for your preferred export format (CSV or Excel)
5. Generate analysis and export reports

### Example Session

```
🌐 Zscaler ZIA Custom URL Category Analyzer - OAuth 2.0 Edition
   Original by James Tucker | OAuth version by ZHERO srl

🔐 Authenticating with Zscaler Identity...
✅ Authentication successful!

🔍 Fetching custom URL categories...

Found 3 custom URL categories:
------------------------------------------------------------
[1] Internal Resources
     Type: URL_CATEGORY
     Super Category: BUSINESS_AND_ECONOMY
     Description: Company internal websites and applications

[2] Partner Sites
     Type: URL_CATEGORY
     Super Category: BUSINESS_AND_ECONOMY

[3] Development Tools
     Type: URL_CATEGORY
     Super Category: INFORMATION_TECHNOLOGY

📋 Select categories to analyze:
Enter category numbers (e.g., 1,3,5) or 'all' for all categories: 1,3

📄 Select export format:
1. CSV (Comma-separated values)
2. XLSX (Excel with formatting)
Enter your choice (1 or 2) [default: 2]: 2
```

### Output Files

The tool generates output files for each analyzed category:

-   **CSV Format**: `category_name_category_analysis.csv` - Simple URL-to-category mappings
-   **Excel Format**: `category_name_category_analysis.xlsx` - Professional report with:
    -   Analysis Results sheet with formatted data and highlighted uncategorized URLs
    -   Summary sheet with statistics, charts, and credits
    -   Auto-adjusted column widths and frozen headers
    -   Clickable link to ZHERO website

## API Endpoints Used

This tool uses the following Zscaler API endpoints:

-   Zscaler Identity OAuth: `/oauth2/v1/token` - OAuth 2.0 authentication
-   ZIA API via OneAPI gateway:
    -   `/zia/api/v1/urlCategories/lite` - List URL categories
    -   `/zia/api/v1/urlCategories/{id}` - Get category details
    -   `/zia/api/v1/urlLookup` - Bulk URL categorization lookup

## Performance Considerations

-   The tool processes URLs in batches of 100 (API limit)
-   Large categories with thousands of URLs are fully supported
-   Progress indicators show batch processing status
-   Results are streamed to reduce memory usage
-   **Rate Limiting**: Enforces 2 seconds between API calls (conservative approach)
    -   Automatic delays between requests
    -   Time estimates for large batch operations

## Troubleshooting

### Authentication Errors

-   Verify your Client ID and Client Secret are correct
-   Ensure your API client has the necessary permissions
-   Check network connectivity to Zscaler API endpoints

### No Categories Found

-   Ensure you have custom URL categories defined in ZIA
-   Verify API permissions include URL category read access

### Rate Limiting

-   The tool respects Zscaler API rate limits
-   For very large deployments, consider running analyses sequentially

## Use Cases

1. **Compliance Auditing**: Verify custom URL lists against Zscaler's categorization
2. **Category Cleanup**: Identify redundant URLs already categorized by Zscaler
3. **Gap Analysis**: Find URLs that need custom categorization
4. **Migration Planning**: Analyze categories before policy changes

## Contributing

Feel free to submit issues or pull requests. When contributing:

1. Maintain backward compatibility
2. Follow the existing code style
3. Update documentation as needed
4. Test with various category sizes

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

Special thanks to James Tucker for creating the original script that inspired this OAuth 2.0 implementation.

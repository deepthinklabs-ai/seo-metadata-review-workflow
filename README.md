# SEO - Metadata Review Workflow

An n8n workflow for automated SEO metadata review and analysis.

## Overview

This workflow automates the process of reviewing and analyzing SEO metadata for ENTIRE websites, helping identify optimization opportunities and ensuring proper metadata implementation. Completed analysis is emailed to the user for each page analyzed.

## Features

- ✅ Automated metadata extraction using Firecrawl
- ✅ AI-powered SEO analysis using Anthropic Claude
- ✅ Batch processing capabilities
- ✅ Email notifications with detailed reporting
- ✅ Error handling and validation

## Prerequisites

- n8n instance (self-hosted or cloud)
- Anthropic API key for AI-powered analysis
- Firecrawl API key for enhanced web scraping to markdown format
- SMTP email configuration for notifications
- Required n8n nodes (see workflow dependencies below)

## Installation

1. **Import the Workflow**
   ```bash
   # Download the workflow JSON
   curl -O https://raw.githubusercontent.com/deepthinklabs-ai/seo-metadata-review-workflow/main/workflow.json
   ```

2. **Import in n8n**
   - Open your n8n instance
   - Go to Workflows
   - Click "Import from File" or "Import from URL"
   - Select the `workflow.json` file or paste the GitHub raw URL

3. **Configure API Credentials**
   - Set up required API credentials in n8n (see Configuration section)
   - Configure webhook URLs if using HTTP triggers
   - Test connections to ensure proper setup

## Configuration

### Required n8n Credentials

This workflow uses n8n's credential system for secure API key management. You'll need to set up the following credentials:

**Note**: All sensitive data is stored securely in n8n credentials. Never hardcode API keys in workflow nodes.

#### 1. Anthropic API Credentials
For AI-powered SEO analysis and recommendations:

**Setup**:
- Sign up or sign in at [Anthropic Console](https://console.anthropic.com/)
- Create an API key
- In n8n: Settings → Credentials → Add Credential
- Select "Anthropic"
- **Credential Name**: "Anthropic API"
- **API Key**: "x-api-key"
- **Base URL**: https://api.anthropic.com (note: this should be pre-populated)

#### 2. Firecrawl API Credentials
For enhanced web scraping and content extraction to markdown:

**Setup**:
- Sign up at [Firecrawl](https://firecrawl.dev/)
- Get your API key from the dashboard
- In n8n: Settings → Credentials → Add Credential
- Select "Firecrawl API"
- **Credential Name**: "Firecrawl API"
- **Base URL**: "https://api.firecrawl.dev/v1"
- **API Key**: "Bearer YOUR_FIRECRAWL_API_KEY" (note: be sure to include the "bearer " before your api key)

#### 3. SMTP Email Credentials
For sending analysis reports via email:

**Setup**:
- Configure your email provider (Gmail, Outlook, etc.)
- In n8n: Settings → Credentials → Add Credential
- Select "SMTP"
- **Credential Name**: "SEO Email SMTP"
- **Configure settings** based on your provider (see detailed guide in docs/CONFIGURATION.md)

### Input Parameters
- **URL**: Target website to analyze
- **Email From/To**: Notification email addresses

## Usage

### Manual Execution
1. Open the workflow in n8n
2. Ensure all credentials are configured
3. Provide target website URL in the Init Site node
4. Enter the Email From/Email To in the Send Email node
5. Click "Execute Workflow"
6. Check email for detailed analysis report


## Workflow Structure

Trigger → URL Processing → Firecrawl Scraping → Anthropic Analysis → Email Report → Output

### Key Nodes
- **Firecrawl**: Enhanced web content extraction (uses Firecrawl API credential)
- **Anthropic Claude**: AI-powered SEO analysis (uses Anthropic API credential)
- **Email**: Send formatted analysis reports (uses SMTP credential)
- **Set**: Structure and format output data
- **Code**: Custom logic and data processing

## Output Format

The workflow produces comprehensive analysis reports. Example email below:

Metadata Report
Page: TARGET URL
Score: 55/100

Key Findings
MEDIUM — Title length (74 chars) exceeds recommended range, may truncate in search results
HIGH — Meta description (243 chars) significantly exceeds limits and contains redundant content
HIGH — Complete absence of Open Graph metadata impacts social media sharing
MEDIUM — Missing language declarations affect accessibility and search engine understanding

Priority Fixes
Priority	Action	Why it matters
P0	Trim meta description to 120-155 characters by removing redundant phrases and improving flow	Current length will cause truncation and poor user experience
P0	Add complete Open Graph tags (og:title, og:description, og:image, og:locale)	Essential for proper social media sharing and engagement
P1	Add html_lang='en' attribute to html element	Improves accessibility and search engine language detection
P1	Optimize title length to 50-60 characters while maintaining key messaging	Reduces risk of truncation in search results

Recommended Title
Perfect Winery Venues for Unforgettable Events | (Insert Company Name)

Recommended Meta Description
Discover premier winery venues for weddings, corporate events, and celebrations. Search by region, compare layouts, and connect directly with breathtaking wine country spaces for your next unforgettable event.

Open Graph Snippet
<meta property='og:title' content='Perfect Winery Venues for Unforgettable Events | VineVenues'>
<meta property='og:description' content='Discover premier winery venues for weddings, corporate events, and celebrations. Search by region, compare layouts, and connect directly with breathtaking wine country spaces for your next unforgettable event.'>
<meta property='og:image' content='https://example.com/images/og-1200x630.jpg'>
<meta property='og:locale' content='en_US'>

Language
html_lang: — • og_locale: —

References
Google Search Essentials: Titles & snippets, Meta descriptions best practices, Open Graph protocol

## Troubleshooting

### Common Issues

**API Authentication Errors**
- Verify credentials are correctly configured in n8n
- Check credential names match those used in workflow nodes
- Ensure API keys have sufficient permissions
- Test credentials individually

**Firecrawl Extraction Fails**
- Check URL accessibility and robots.txt
- Verify Firecrawl API limits and usage in dashboard
- Review extraction parameters in workflow

**Anthropic Analysis Issues**
- Confirm API key has Claude access in Anthropic dashboard
- Check input data format and size limits
- Review custom prompts for syntax errors

**Email Delivery Problems**
- Verify SMTP credentials and settings in n8n
- Test SMTP connection using n8n's credential test feature
- Check spam filters and email quotas

### Debug Mode
1. Enable "Save Execution Progress" in workflow settings
2. Check individual node outputs for errors
3. Use "Execute Node" for targeted debugging
4. Review n8n logs for detailed error messages
5. Test credentials individually in n8n

## API Rate Limits

Monitor usage in respective dashboards:
- **Anthropic**: Check usage in Anthropic Console
- **Firecrawl**: Monitor limits in Firecrawl dashboard (typically 500-5000 requests/month)
- **Email**: Depends on SMTP provider limits

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly with all API integrations
5. Submit a pull request

## License

This workflow is available under the MIT License. See LICENSE file for details.

## Support

Please feel free to email me with any issues, questions, comments, enhancement requests, etc. Happy to help!

- 📧 Email: [dave@deepthinklabs.ai]
- 🐛 Issues: [GitHub Issues](https://github.com/deepthinklabs-ai/seo-metadata-review-workflow/issues)
- 📖 Documentation: [n8n Documentation](https://docs.n8n.io/)

## Changelog

### v1.0.0
- Initial release
- Anthropic Claude integration for AI analysis
- Firecrawl integration for enhanced scraping
- Email notification system
- Comprehensive SEO metadata analysis
- Secure credential-based configuration

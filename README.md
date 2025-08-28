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
- Firecrawl API key for enhanced web scraping
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
   - Set up required API credentials (see Configuration section)
   - Configure webhook URLs if using HTTP triggers
   - Test connections to ensure proper setup

## Configuration

### Required API Keys

#### 1. Anthropic API Key
For AI-powered SEO analysis and recommendations:
- Sign up at [Anthropic Console](https://console.anthropic.com/)
- Create an API key
- Add to n8n credentials as "Anthropic API"

#### 2. Firecrawl API Key  
For enhanced web scraping and content extraction:
- Sign up at [Firecrawl](https://firecrawl.dev/)
- Get your API key from the dashboard
- Add to n8n credentials as "Firecrawl API"

#### 3. Email SMTP Configuration
For sending analysis reports via email:
- Configure SMTP settings in n8n
- Supported providers: Gmail, Outlook, SendGrid, Mailgun, etc.
- Add to n8n credentials as "SMTP Email"

### Input Parameters
- **URLs**: Target websites to analyze
- **Analysis Depth**: Level of metadata analysis
- **Output Format**: JSON, CSV, or custom format
- **Email Recipients**: Notification email addresses
- **Analysis Options**: Custom SEO rules and preferences

### Environment Variables
```bash
# Add these to your n8n environment
ANTHROPIC_API_KEY=your_anthropic_api_key_here
FIRECRAWL_API_KEY=your_firecrawl_api_key_here
SMTP_HOST=your_smtp_host
SMTP_PORT=587
SMTP_USER=your_email@example.com
SMTP_PASS=your_email_password
WEBHOOK_URL=your_webhook_url
OUTPUT_PATH=/path/to/output
```

### n8n Credentials Setup

1. **Anthropic Credentials**
   ```
   Credential Type: HTTP Header Auth
   Name: Authorization
   Value: Bearer YOUR_ANTHROPIC_API_KEY
   ```

2. **Firecrawl Credentials**
   ```
   Credential Type: HTTP Header Auth  
   Name: Authorization
   Value: Bearer YOUR_FIRECRAWL_API_KEY
   ```

3. **SMTP Credentials**
   ```
   Credential Type: SMTP
   Host: your-smtp-host
   Port: 587 (or appropriate port)
   Secure: true/false (depending on provider)
   User: your-email@example.com
   Password: your-app-password
   ```

## Usage

### Manual Execution
1. Open the workflow in n8n
2. Provide target website URL
3. Configure analysis parameters
4. Click "Execute Workflow"
5. Check email for detailed analysis report

### Automated Execution
- Configure triggers (webhook, cron, etc.)
- Set up input sources (webhooks, databases, files)
- Monitor execution logs for results
- Automated email delivery for each analysis

## Workflow Structure

```
Trigger → URL Processing → Firecrawl Scraping → Anthropic Analysis → Email Report → Output
```

### Key Nodes
- **Firecrawl**: Enhanced web content extraction
- **Anthropic Claude**: AI-powered SEO analysis
- **Email**: Send formatted analysis reports
- **Set**: Structure and format output data
- **Code**: Custom logic and data processing
- **Webhook**: Receive trigger events

## Output Format

The workflow produces comprehensive analysis reports:

```json
{
  "url": "https://example.com",
  "metadata": {
    "title": "Page Title",
    "description": "Meta description",
    "keywords": ["keyword1", "keyword2"],
    "openGraph": {
      "title": "OG Title",
      "description": "OG Description",
      "image": "og-image.jpg"
    },
    "twitterCard": {
      "card": "summary_large_image",
      "title": "Twitter Title"
    }
  },
  "analysis": {
    "titleAnalysis": {
      "length": 65,
      "recommendations": ["Consider shortening title"],
      "score": 85
    },
    "descriptionAnalysis": {
      "length": 155,
      "recommendations": [],
      "score": 95
    },
    "overallScore": 88,
    "aiRecommendations": [
      "Add more descriptive keywords to title",
      "Include call-to-action in meta description"
    ]
  },
  "timestamp": "2025-08-28T08:13:20Z"
}
```

## Customization

### Adding New Analysis Rules
1. Open the Anthropic Claude node
2. Modify the analysis prompt
3. Add custom SEO criteria
4. Update output formatting accordingly

### Modifying Email Templates
1. Edit the Email node configuration
2. Customize HTML email template
3. Adjust report formatting and styling

### Adding New Data Sources
1. Configure additional Firecrawl options
2. Add new metadata extraction rules
3. Update analysis logic for new data points

## Troubleshooting

### Common Issues

**API Authentication Errors**
- Verify API keys are correctly configured
- Check credential names match node configurations
- Ensure API keys have sufficient permissions

**Firecrawl Extraction Fails**
- Check URL accessibility and robots.txt
- Verify Firecrawl API limits and usage
- Review extraction parameters

**Anthropic Analysis Issues**
- Confirm API key has Claude access
- Check input data format and size limits
- Review custom prompts for syntax errors

**Email Delivery Problems**
- Verify SMTP credentials and settings
- Check spam filters and email quotas
- Test email configuration with simple messages

### Debug Mode
1. Enable "Save Execution Progress" in workflow settings
2. Check individual node outputs for errors
3. Use "Execute Node" for targeted debugging
4. Review n8n logs for detailed error messages

## API Rate Limits

- **Anthropic**: Varies by plan (check your dashboard)
- **Firecrawl**: Varies by plan (typically 500-5000 requests/month)
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

---

**Original Workflow URL**: https://deepthinklabs.app.n8n.cloud/workflow/kNBoh6bzML9vdxut

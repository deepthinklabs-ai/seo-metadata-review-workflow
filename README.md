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
   - Set up required API credentials in n8n (see Configuration section)
   - Configure webhook URLs if using HTTP triggers
   - Test connections to ensure proper setup

## Configuration

### Required n8n Credentials

This workflow uses n8n's credential system for secure API key management. You'll need to set up the following credentials:

#### 1. Anthropic API Credentials
For AI-powered SEO analysis and recommendations:

**Setup**:
- Sign up at [Anthropic Console](https://console.anthropic.com/)
- Create an API key
- In n8n: Settings → Credentials → Add Credential
- Select "HTTP Header Auth"
- **Credential Name**: "Anthropic API"
- **Header Name**: "x-api-key"
- **Header Value**: Your Anthropic API key

#### 2. Firecrawl API Credentials
For enhanced web scraping and content extraction:

**Setup**:
- Sign up at [Firecrawl](https://firecrawl.dev/)
- Get your API key from the dashboard
- In n8n: Settings → Credentials → Add Credential
- Select "HTTP Header Auth"
- **Credential Name**: "Firecrawl API"
- **Header Name**: "Authorization"
- **Header Value**: "Bearer YOUR_FIRECRAWL_API_KEY"

#### 3. SMTP Email Credentials
For sending analysis reports via email:

**Setup**:
- Configure your email provider (Gmail, Outlook, SendGrid, etc.)
- In n8n: Settings → Credentials → Add Credential
- Select "SMTP"
- **Credential Name**: "SEO Email SMTP"
- **Configure settings** based on your provider (see detailed guide in docs/CONFIGURATION.md)

### Input Parameters
- **URLs**: Target websites to analyze
- **Analysis Depth**: Level of metadata analysis
- **Output Format**: JSON, CSV, or custom format
- **Email Recipients**: Notification email addresses
- **Analysis Options**: Custom SEO rules and preferences

### Credential Configuration Summary

| Service | Credential Type | Header/Field | Value Format |
|---------|----------------|--------------|--------------|
| Anthropic | HTTP Header Auth | x-api-key | `sk-ant-your-key` |
| Firecrawl | HTTP Header Auth | Authorization | `Bearer fc-your-key` |
| SMTP Email | SMTP | N/A | Host, port, user, password |

**Note**: All sensitive data is stored securely in n8n credentials. Never hardcode API keys in workflow nodes.

## Usage

### Manual Execution
1. Open the workflow in n8n
2. Ensure all credentials are configured
3. Provide target website URL
4. Configure analysis parameters
5. Click "Execute Workflow"
6. Check email for detailed analysis report

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
- **Firecrawl**: Enhanced web content extraction (uses Firecrawl API credential)
- **Anthropic Claude**: AI-powered SEO analysis (uses Anthropic API credential)
- **Email**: Send formatted analysis reports (uses SMTP credential)
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

- 📧 Email: [dave@deepthinklabs.ai]
- 🐛 Issues: [GitHub Issues](https://github.com/deepthinklabs-ai/seo-metadata-review-workflow/issues)
- 📖 Documentation: [n8n Documentation](https://docs.n8n.io/)
- 📋 Detailed Setup: [Configuration Guide](docs/CONFIGURATION.md)

## Changelog

### v1.0.0
- Initial release
- Anthropic Claude integration for AI analysis
- Firecrawl integration for enhanced scraping
- Email notification system
- Comprehensive SEO metadata analysis
- Secure credential-based configuration

---

**Original Workflow URL**: https://deepthinklabs.app.n8n.cloud/workflow/kNBoh6bzML9vdxut

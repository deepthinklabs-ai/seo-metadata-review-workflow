# SEO - Metadata Review Workflow - n8n

An n8n workflow for automated SEO metadata review and analysis.

## Overview

This workflow automates the process of reviewing and analyzing SEO metadata for websites, helping identify optimization opportunities and ensuring proper metadata implementation.

## Features

- ✅ Automated metadata extraction
- ✅ SEO analysis and recommendations
- ✅ Batch processing capabilities
- ✅ Detailed reporting
- ✅ Error handling and validation

## Prerequisites

- n8n instance (self-hosted or cloud)
- Required n8n nodes (see workflow dependencies below)
- Access to target websites for metadata analysis

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

3. **Configure Credentials**
   - Set up any required API credentials
   - Configure webhook URLs if using HTTP triggers
   - Test connections to ensure proper setup

## Usage

### Manual Execution
1. Open the workflow in n8n
2. Provide input URLs or data
3. Click "Execute Workflow"
4. Review the results in the output

### Automated Execution
- Configure triggers (webhook, cron, etc.)
- Set up input sources (webhooks, databases, files)
- Monitor execution logs for results

## Configuration

### Input Parameters
- **URLs**: Target websites to analyze
- **Analysis Depth**: Level of metadata analysis
- **Output Format**: JSON, CSV, or custom format
- **Notification Settings**: Email or webhook notifications

### Environment Variables
```bash
# Add these to your n8n environment
SEO_API_KEY=your_api_key_here
WEBHOOK_URL=your_webhook_url
OUTPUT_PATH=/path/to/output
```

## Workflow Structure

```
Trigger → URL Validation → Metadata Extraction → Analysis → Report Generation → Output
```

### Key Nodes
- **HTTP Request**: Fetch webpage content
- **HTML Extract**: Parse metadata elements
- **Code**: Custom SEO analysis logic
- **Set**: Structure output data
- **Webhook**: Receive trigger events

## Output Format

The workflow produces structured output containing:

```json
{
  "url": "https://example.com",
  "metadata": {
    "title": "Page Title",
    "description": "Meta description",
    "keywords": ["keyword1", "keyword2"],
    "openGraph": {...},
    "twitterCard": {...}
  },
  "analysis": {
    "titleLength": 65,
    "descriptionLength": 155,
    "recommendations": [...]
  },
  "timestamp": "2025-08-28T08:13:20Z"
}
```

## Customization

### Adding New Analysis Rules
1. Open the Code node in the analysis section
2. Add your custom logic
3. Update the output schema accordingly

### Modifying Output Format
1. Edit the Set nodes
2. Adjust the data structure
3. Update downstream nodes if needed

## Troubleshooting

### Common Issues

**Workflow fails to fetch webpage**
- Check URL validity
- Verify network connectivity
- Review CORS policies

**Metadata extraction incomplete**
- Ensure proper HTML parsing
- Check for JavaScript-rendered content
- Review CSS selectors

**Analysis results unexpected**
- Validate input data format
- Check analysis logic in Code nodes
- Review error logs

### Debug Mode
1. Enable "Save Execution Progress" in workflow settings
2. Check individual node outputs
3. Use "Execute Node" for targeted debugging

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

This workflow is available under the MIT License. See LICENSE file for details.

## Support

- 📧 Email: [your-email@example.com]
- 🐛 Issues: [GitHub Issues](https://github.com/deepthinklabs-ai/seo-metadata-review-workflow/issues)
- 📖 Documentation: [n8n Documentation](https://docs.n8n.io/)

## Changelog

### v1.0.0
- Initial release
- Basic metadata extraction and analysis
- HTML and Open Graph support

---

**Original Workflow URL**: https://deepthinklabs.app.n8n.cloud/workflow/kNBoh6bzML9vdxut

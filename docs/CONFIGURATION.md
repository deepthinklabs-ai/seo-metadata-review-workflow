# Configuration Guide

This guide provides detailed instructions for setting up all required API integrations and credentials for the SEO Metadata Review workflow.

## Required Services

### 1. Anthropic Claude API

**Purpose**: AI-powered SEO analysis and recommendations

**Setup Steps**:
1. Go to [Anthropic Console](https://console.anthropic.com/)
2. Sign up for an account or log in
3. Navigate to "API Keys" section
4. Click "Create Key" and give it a descriptive name
5. Copy the API key (starts with `sk-ant-`)

**n8n Configuration**:
```
Credential Type: HTTP Header Auth
Header Name: x-api-key
Header Value: YOUR_ANTHROPIC_API_KEY
```

**Usage Limits**: Check your plan limits in the Anthropic dashboard

---

### 2. Firecrawl API

**Purpose**: Enhanced web scraping and content extraction

**Setup Steps**:
1. Visit [Firecrawl](https://firecrawl.dev/)
2. Sign up for an account
3. Go to your dashboard
4. Copy your API key from the "API Keys" section
5. Note your plan limits (requests per month)

**n8n Configuration**:
```
Credential Type: HTTP Header Auth
Header Name: Authorization
Header Value: Bearer YOUR_FIRECRAWL_API_KEY
```

**Free Tier**: Usually includes 500 requests/month
**Paid Plans**: Higher limits available

---

### 3. Email SMTP Configuration

**Purpose**: Send analysis reports via email

#### Option A: Gmail SMTP
1. Enable 2-factor authentication on your Google account
2. Generate an App Password:
   - Go to Google Account settings
   - Security → 2-Step Verification → App passwords
   - Generate password for "Mail"
3. Use these settings:
   ```
   Host: smtp.gmail.com
   Port: 587
   Security: STARTTLS
   Username: your-email@gmail.com
   Password: your-app-password
   ```

#### Option B: Outlook/Hotmail SMTP
```
Host: smtp-mail.outlook.com
Port: 587
Security: STARTTLS
Username: your-email@outlook.com
Password: your-account-password
```

#### Option C: SendGrid (Recommended for production)
1. Sign up at [SendGrid](https://sendgrid.com/)
2. Create an API key
3. Configure as SMTP:
   ```
   Host: smtp.sendgrid.net
   Port: 587
   Username: apikey
   Password: YOUR_SENDGRID_API_KEY
   ```

**n8n Configuration**:
```
Credential Type: SMTP
Host: [from above]
Port: [from above]
Secure: true (for SSL) or false (for STARTTLS)
Username: [your email or apikey]
Password: [your password or API key]
```

---

## n8n Credential Setup

### Step 1: Add Anthropic Credentials
1. Go to n8n Settings → Credentials
2. Click "Add Credential"
3. Select "HTTP Header Auth"
4. Name: "Anthropic API"
5. Header Name: "x-api-key"
6. Header Value: Your Anthropic API key
7. Save

### Step 2: Add Firecrawl Credentials
1. Go to n8n Settings → Credentials
2. Click "Add Credential"
3. Select "HTTP Header Auth"
4. Name: "Firecrawl API"
5. Header Name: "Authorization"
6. Header Value: "Bearer YOUR_FIRECRAWL_API_KEY"
7. Save

### Step 3: Add SMTP Credentials
1. Go to n8n Settings → Credentials
2. Click "Add Credential"
3. Select "SMTP"
4. Name: "SEO Email SMTP"
5. Fill in your SMTP settings (see options above)
6. Test the connection
7. Save

---

## Environment Variables (Optional)

For additional security, you can use environment variables:

```bash
# Anthropic
ANTHROPIC_API_KEY=sk-ant-your-key-here

# Firecrawl  
FIRECRAWL_API_KEY=fc-your-key-here

# Email SMTP
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your-email@gmail.com
SMTP_PASS=your-app-password

# Workflow settings
DEFAULT_EMAIL_RECIPIENT=reports@yourcompany.com
MAX_PAGES_PER_ANALYSIS=50
```

Then reference in n8n using `{{ $env.ANTHROPIC_API_KEY }}`

---

## Testing Your Configuration

### 1. Test Anthropic Integration
Create a simple HTTP Request node:
- Method: POST
- URL: `https://api.anthropic.com/v1/messages`
- Credentials: Your Anthropic credential
- Body:
```json
{
  "model": "claude-3-haiku-20240307",
  "max_tokens": 1000,
  "messages": [
    {
      "role": "user",
      "content": "Test message"
    }
  ]
}
```

### 2. Test Firecrawl Integration
Create an HTTP Request node:
- Method: POST
- URL: `https://api.firecrawl.dev/v0/scrape`
- Credentials: Your Firecrawl credential
- Body:
```json
{
  "url": "https://example.com",
  "pageOptions": {
    "onlyMainContent": true
  }
}
```

### 3. Test Email Configuration
Create an Email Send node:
- Credentials: Your SMTP credential
- To: your-test-email@example.com
- Subject: "Test Email"
- Text: "This is a test email from n8n"

---

## Security Best Practices

1. **Never hardcode API keys** in workflow nodes
2. **Use n8n credentials** for all sensitive information
3. **Regularly rotate API keys** (monthly recommended)
4. **Monitor API usage** to detect unusual activity
5. **Use environment variables** for additional security layer
6. **Restrict SMTP credentials** to specific IP ranges if possible

---

## Troubleshooting

### Anthropic Issues
- **401 Unauthorized**: Check API key format and validity
- **429 Rate Limited**: You've exceeded your usage limits
- **400 Bad Request**: Check your request format

### Firecrawl Issues  
- **403 Forbidden**: API key invalid or expired
- **429 Too Many Requests**: You've hit rate limits
- **422 Unprocessable Entity**: Invalid URL or parameters

### Email Issues
- **Authentication Failed**: Check username/password
- **Connection Timeout**: Verify host and port settings
- **TLS/SSL Errors**: Check security settings (STARTTLS vs SSL)

### Common Solutions
1. Double-check all credential configurations
2. Test with simple examples first
3. Check API documentation for updates
4. Monitor n8n execution logs for detailed errors
5. Verify network connectivity and firewall settings

---

## Cost Estimation

### Monthly Costs (approximate)
- **Anthropic**: $0.50-$5.00 (depending on usage)
- **Firecrawl**: $0-$29 (free tier or paid plan)
- **Email**: $0-$15 (depends on provider)

**Total estimated monthly cost**: $0.50 - $49

Monitor your usage regularly to avoid unexpected charges.

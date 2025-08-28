# Configuration Guide

This guide provides detailed instructions for setting up all required API integrations using n8n's credential system for the SEO Metadata Review workflow.

## Required Services

### 1. Anthropic Claude API

**Purpose**: AI-powered SEO analysis and recommendations

**Setup Steps**:
1. Go to [Anthropic Console](https://console.anthropic.com/)
2. Sign up for an account or log in
3. Navigate to "API Keys" section
4. Click "Create Key" and give it a descriptive name
5. Copy the API key (starts with `sk-ant-`)

**n8n Credential Configuration**:
1. Go to n8n Settings → Credentials
2. Click "Add Credential" 
3. Select "HTTP Header Auth"
4. **Name**: "Anthropic API" (or your preferred name)
5. **Header Name**: `x-api-key`
6. **Header Value**: Your Anthropic API key
7. **Save** and test the credential

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

**n8n Credential Configuration**:
1. Go to n8n Settings → Credentials
2. Click "Add Credential"
3. Select "HTTP Header Auth"
4. **Name**: "Firecrawl API" (or your preferred name)
5. **Header Name**: `Authorization`
6. **Header Value**: `Bearer YOUR_FIRECRAWL_API_KEY`
7. **Save** and test the credential

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

**n8n Credential Configuration for Gmail**:
1. Go to n8n Settings → Credentials
2. Click "Add Credential"
3. Select "SMTP"
4. **Name**: "SEO Email SMTP" (or your preferred name)
5. Configure:
   - **Host**: `smtp.gmail.com`
   - **Port**: `587`
   - **Secure**: Enable STARTTLS
   - **Username**: `your-email@gmail.com`
   - **Password**: Your generated app password
6. **Test** the connection and **Save**

#### Option B: Outlook/Hotmail SMTP

**n8n Credential Configuration for Outlook**:
1. Go to n8n Settings → Credentials
2. Click "Add Credential"
3. Select "SMTP"
4. **Name**: "SEO Email SMTP"
5. Configure:
   - **Host**: `smtp-mail.outlook.com`
   - **Port**: `587`
   - **Secure**: Enable STARTTLS
   - **Username**: `your-email@outlook.com`
   - **Password**: Your account password
6. **Test** the connection and **Save**

#### Option C: SendGrid (Recommended for production)
1. Sign up at [SendGrid](https://sendgrid.com/)
2. Create an API key in the SendGrid dashboard

**n8n Credential Configuration for SendGrid**:
1. Go to n8n Settings → Credentials
2. Click "Add Credential"
3. Select "SMTP"
4. **Name**: "SEO Email SMTP"
5. Configure:
   - **Host**: `smtp.sendgrid.net`
   - **Port**: `587`
   - **Secure**: Enable STARTTLS
   - **Username**: `apikey` (literally the word "apikey")
   - **Password**: Your SendGrid API key
6. **Test** the connection and **Save**

---

## n8n Workflow Configuration

### Step 1: Import the Workflow
1. Download the workflow JSON from the repository
2. In n8n, go to Workflows
3. Click "Import from File"
4. Select the downloaded JSON file
5. The workflow will be imported with placeholder credential references

### Step 2: Assign Credentials to Nodes
After importing, you need to assign your created credentials to the appropriate nodes:

#### Anthropic Nodes
1. Open any Anthropic/Claude node in the workflow
2. In the "Credentials" section, select your "Anthropic API" credential
3. Repeat for all Anthropic-related nodes

#### Firecrawl Nodes
1. Open any Firecrawl node in the workflow
2. In the "Credentials" section, select your "Firecrawl API" credential
3. Repeat for all Firecrawl-related nodes

#### Email Nodes
1. Open any Email/Send node in the workflow
2. In the "Credentials" section, select your "SEO Email SMTP" credential
3. Configure recipient email addresses as needed

### Step 3: Test Individual Credentials

**Test Anthropic Integration**:
1. Create a simple HTTP Request node
2. Set URL: `https://api.anthropic.com/v1/messages`
3. Method: POST
4. Assign your Anthropic credential
5. Add test body:
```json
{
  "model": "claude-3-haiku-20240307",
  "max_tokens": 100,
  "messages": [{"role": "user", "content": "Hello"}]
}
```
6. Execute to test connection

**Test Firecrawl Integration**:
1. Create a simple HTTP Request node
2. Set URL: `https://api.firecrawl.dev/v0/scrape`
3. Method: POST
4. Assign your Firecrawl credential
5. Add test body:
```json
{
  "url": "https://example.com",
  "pageOptions": {"onlyMainContent": true}
}
```
6. Execute to test connection

**Test Email Configuration**:
1. Create a simple Send Email node
2. Assign your SMTP credential
3. Set test recipient and message
4. Execute to test delivery

---

## Credential Security Best Practices

### 1. Credential Naming Convention
Use descriptive names for easy identification:
- `Anthropic API - Production`
- `Firecrawl API - SEO Workflow`
- `SMTP - SEO Reports`

### 2. Access Control
- Only share credentials with team members who need access
- Use n8n's sharing features for collaborative workflows
- Regularly audit who has access to credentials

### 3. Credential Rotation
- Rotate API keys monthly or quarterly
- Update credentials in n8n when keys are rotated
- Monitor for any authentication failures

### 4. Testing and Validation
- Always test credentials after creation
- Set up monitoring to detect credential issues
- Use n8n's credential testing features regularly

---

## Troubleshooting Credentials

### Anthropic Issues
- **401 Unauthorized**: 
  - Check API key format (should start with `sk-ant-`)
  - Verify the header name is exactly `x-api-key`
  - Ensure API key is active in Anthropic Console

- **429 Rate Limited**: 
  - Check usage limits in Anthropic dashboard
  - Consider upgrading plan if hitting limits regularly

### Firecrawl Issues  
- **403 Forbidden**: 
  - Verify API key is correct and active
  - Check header format: `Authorization: Bearer YOUR_KEY`

- **429 Too Many Requests**: 
  - Monitor usage in Firecrawl dashboard
  - Consider rate limiting in workflow design

### Email/SMTP Issues
- **Authentication Failed**: 
  - For Gmail: Ensure you're using App Password, not regular password
  - For Outlook: Check if 2FA is interfering
  - For SendGrid: Verify username is literally "apikey"

- **Connection Timeout**: 
  - Check host and port settings
  - Verify firewall isn't blocking SMTP ports
  - Test from n8n server network

- **TLS/SSL Errors**: 
  - Ensure correct security settings (STARTTLS vs SSL)
  - Check certificate validity

### General Debugging Steps
1. **Test credentials individually** using n8n's test feature
2. **Check credential names** match exactly in workflow nodes
3. **Review n8n logs** for detailed error messages
4. **Verify API quotas** haven't been exceeded
5. **Check service status** pages for outages

---

## Credential Management Workflow

### Initial Setup Checklist
- [ ] Create Anthropic API key and n8n credential
- [ ] Create Firecrawl API key and n8n credential  
- [ ] Configure SMTP email credential
- [ ] Test all three credentials individually
- [ ] Import workflow and assign credentials to nodes
- [ ] Test complete workflow end-to-end

### Maintenance Schedule
- **Weekly**: Monitor API usage and quotas
- **Monthly**: Review credential access and rotate if needed
- **Quarterly**: Audit all credentials and remove unused ones

---

## Cost Monitoring

### Using n8n Credentials for Cost Control
- Set up monitoring workflows that use the same credentials
- Track API usage through respective dashboards
- Set up alerts when approaching usage limits

### Monthly Cost Estimation
- **Anthropic**: $0.50-$5.00 (depending on analysis volume)
- **Firecrawl**: $0-$29 (free tier or paid plan)
- **Email**: $0-$15 (depends on provider and volume)

**Total estimated monthly cost**: $0.50 - $49

All costs can be monitored through the respective service dashboards using the same credentials configured in n8n.

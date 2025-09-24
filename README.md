# Google Maps Email Finder - ClayGen Alternative

A powerful n8n workflow that replicates ClayGen's functionality for extracting contact information from company websites and social media profiles.

## 🎯 **Purpose**

This workflow automatically:
- Searches Google for company websites and social media profiles
- Crawls websites to extract contact information
- Crawls social media profiles (Facebook, LinkedIn, Twitter, Instagram, etc.) for additional contact details
- Uses AI to process and validate extracted contact information
- Returns structured contact data with quality scores

## 📊 **Workflow Structure**

```
Webhook Trigger → Google Search (SerpApi) → Website Crawler → HTML Data Extractor → 
Split Social Links → Social Media Crawler → Social Media Contact Extractor → 
AI Data Processor → Data Validator → Response Formatter → Webhook Response
```

## 🔗 **Webhook Endpoint**

- **URL**: `https://n8n.ottomatik.ai/webhook/claygen-alternative`
- **Method**: POST
- **Input**: 
  ```json
  {
    "company_name": "Company Name"
  }
  ```
  or
  ```json
  {
    "query": "search query"
  }
  ```

## 📁 **Files**

- `google-maps-email-finder.json` - The complete n8n workflow export
- `WORKFLOW_ANALYSIS.md` - Detailed analysis of required fixes and improvements
- `README.md` - This file

## 🚨 **Current Status**

**⚠️ WORKFLOW NEEDS FIXES BEFORE USE**

The workflow has the correct structure but requires several critical configuration fixes before it can be used. See `WORKFLOW_ANALYSIS.md` for detailed information about what needs to be fixed.

## 🔧 **Required Fixes**

1. **Google Search Node** - Add query parameter
2. **HTTP Request Nodes** - Add User-Agent headers
3. **HTML Extractors** - Add source data configuration
4. **AI Processors** - Add schema type configuration
5. **Credentials** - Set up SerpApi credentials

## 🚀 **Getting Started**

1. Import `google-maps-email-finder.json` into your n8n instance
2. Follow the fixes outlined in `WORKFLOW_ANALYSIS.md`
3. Set up SerpApi credentials
4. Activate the workflow
5. Test with a company name via the webhook endpoint

## 📝 **Notes**

- The workflow is currently **INACTIVE** and needs to be activated after fixes
- All nodes are properly connected with error handling and retry logic
- Split Out node correctly handles social media links array
- Enhanced CSS selectors target Facebook's data-testid attributes for better extraction

## 🔗 **Related**

- **n8n Instance**: https://n8n.ottomatik.ai
- **Workflow URL**: https://n8n.ottomatik.ai/workflow/1E2Mqj2ed6ac3XNl
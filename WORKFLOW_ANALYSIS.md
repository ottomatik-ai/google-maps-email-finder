# ClayGen Alternative - Website Social Media Contact Extractor

## Workflow Analysis & Required Fixes

**Workflow ID**: `1E2Mqj2ed6ac3XNl`  
**Workflow URL**: https://n8n.ottomatik.ai/workflow/1E2Mqj2ed6ac3XNl  
**Analysis Date**: September 24, 2025

## 🚨 **CRITICAL PROBLEMS THAT MUST BE FIXED**

### **1. Google Search Node - MISSING QUERY PARAMETER** ❌
```json
"parameters": {
  "options": {
    "gl": "us",
    "device": "desktop", 
    "google_domain": "google.com",
    "hl": "en"
  }
}
```
**PROBLEM**: No `query` parameter! The node will fail because it doesn't know what to search for.

**FIX**: Add `query: "={{ $json.company_name || $json.query || 'company website contact' }}"`

### **2. Website Crawler - MISSING USER AGENT** ❌
```json
"parameters": {
  "url": "={{ $json.url }}",
  "options": {
    "response": {},
    "timeout": 30000
  }
}
```
**PROBLEM**: No User-Agent header! Websites will block the requests.

**FIX**: Add User-Agent header: `"User-Agent": "Mozilla/5.0 (compatible; n8n-bot/1.0; +https://n8n.io)"` and `"responseFormat": "text"`

### **3. Social Media Crawler - MISSING USER AGENT** ❌
```json
"parameters": {
  "url": "={{ $json.social_links }}",
  "options": {
    "response": {},
    "timeout": 30000
  }
}
```
**PROBLEM**: No User-Agent header! Social media sites will block the requests.

**FIX**: Add User-Agent header: `"User-Agent": "Mozilla/5.0 (compatible; n8n-bot/1.0; +https://n8n.io)"` and `"responseFormat": "text"`

### **4. HTML Data Extractor - MISSING SOURCE DATA CONFIG** ❌
```json
"parameters": {
  "extractionValues": { ... },
  "options": {}
}
```
**PROBLEM**: Missing `sourceData` and `dataPropertyName` parameters! The node won't know where to get the HTML data from.

**FIX**: Add `"sourceData": "json"` and `"dataPropertyName": "data"`

### **5. Social Media Contact Extractor - MISSING SOURCE DATA CONFIG** ❌
```json
"parameters": {
  "extractionValues": { ... },
  "options": {}
}
```
**PROBLEM**: Missing `sourceData` and `dataPropertyName` parameters! The node won't know where to get the HTML data from.

**FIX**: Add `"sourceData": "json"` and `"dataPropertyName": "data"`

### **6. AI Data Processor - MISSING SCHEMA TYPE** ❌
```json
"parameters": {
  "text": "...",
  "attributes": { ... },
  "options": {}
}
```
**PROBLEM**: Missing `schemaType: "fromAttributes"` parameter! The AI won't know how to structure the output.

**FIX**: Add `"schemaType": "fromAttributes"`

### **7. Data Validator - MISSING SCHEMA TYPE** ❌
```json
"parameters": {
  "text": "...",
  "attributes": { ... },
  "options": {}
}
```
**PROBLEM**: Missing `schemaType: "fromAttributes"` parameter! The AI won't know how to structure the output.

**FIX**: Add `"schemaType": "fromAttributes"`

## 🔧 **IMPLEMENTATION PLAN**

### **Step 1: Fix Google Search Node**
- Add `query: "={{ $json.company_name || $json.query || 'company website contact' }}"`

### **Step 2: Fix Website Crawler**
- Add User-Agent header: `"User-Agent": "Mozilla/5.0 (compatible; n8n-bot/1.0; +https://n8n.io)"`
- Add response format: `"responseFormat": "text"`

### **Step 3: Fix Social Media Crawler**
- Add User-Agent header: `"User-Agent": "Mozilla/5.0 (compatible; n8n-bot/1.0; +https://n8n.io)"`
- Add response format: `"responseFormat": "text"`

### **Step 4: Fix HTML Data Extractor**
- Add `"sourceData": "json"`
- Add `"dataPropertyName": "data"`

### **Step 5: Fix Social Media Contact Extractor**
- Add `"sourceData": "json"`
- Add `"dataPropertyName": "data"`

### **Step 6: Fix AI Data Processor**
- Add `"schemaType": "fromAttributes"`

### **Step 7: Fix Data Validator**
- Add `"schemaType": "fromAttributes"`

### **Step 8: Set Up Credentials**
- Configure SerpApi credentials for Google Search
- Test the workflow

## 🎯 **PRIORITY ORDER**
1. **Google Search query** (workflow won't start without this)
2. **HTML extractors source data** (data won't be extracted)
3. **User agents** (requests will be blocked)
4. **AI schema types** (AI processing will fail)
5. **Credentials setup** (final step)

## 📊 **WORKFLOW STRUCTURE**

```
Webhook Trigger → Google Search (SerpApi) → Website Crawler → HTML Data Extractor → 
Split Social Links → Social Media Crawler → Social Media Contact Extractor → 
AI Data Processor → Data Validator → Response Formatter → Webhook Response
```

## 🎯 **PURPOSE**

This workflow replicates ClayGen's functionality for:
- Searching Google for company websites and social media profiles
- Crawling websites to extract contact information
- Crawling social media profiles (Facebook, LinkedIn, Twitter, Instagram, etc.) for additional contact details
- Using AI to process and validate extracted contact information
- Returning structured contact data with quality scores

## 🔗 **WEBHOOK ENDPOINT**
- **URL**: `https://n8n.ottomatik.ai/webhook/claygen-alternative`
- **Method**: POST
- **Input**: `{"company_name": "Company Name"}` or `{"query": "search query"}`

## 📝 **NOTES**
- The workflow has the right structure but is missing critical configuration parameters
- All nodes are properly connected
- Split Out node is correctly positioned to handle social media links array
- Error handling and retry logic are properly configured
- The workflow is currently INACTIVE and needs to be activated after fixes
# G.K. Classes - Oral Test Platform

Welcome to the G.K. Classes Oral Test Platform! This is a free, online system for conducting oral exams with speech recognition and automated result tracking.

---

## 🎯 **For Teachers**

### First Time Setup (Once)

1. **Open this website**
2. You'll see the **Teacher Setup** page
3. Enter:
   - **Google API Key** (from Google Cloud)
   - **Google Sheet ID** (your questions sheet)
   - **Google Apps Script URL** (from your deployment)
4. Click **"Load & Setup"**
5. Share this link with students

### Setting Up Google API Key

1. Go to [Google Cloud Console](https://console.cloud.google.com)
2. Create a new project
3. Enable **Google Sheets API**
4. Create an **API Key** (Application restrictions: None)
5. Copy the key

### Setting Up Google Apps Script

1. Go to [script.google.com](https://script.google.com)
2. Create new project
3. Paste this code:

```javascript
function doPost(e) {
  try {
    const data = JSON.parse(e.postData.contents);
    const sheet = SpreadsheetApp.openById(data.sheetId).getSheetByName('Results');
    
    const row = [
      data.timestamp,
      data.name,
      data.class,
      data.roll,
      data.count,
      data.topics,
      data.responses
    ];
    
    sheet.appendRow(row);
    return ContentService.createTextOutput(JSON.stringify({success: true}))
      .setMimeType(ContentService.MimeType.JSON);
  } catch(e) {
    return ContentService.createTextOutput(JSON.stringify({success: false, error: e.toString()}))
      .setMimeType(ContentService.MimeType.JSON);
  }
}
```

4. Click **Deploy** → **New Deployment**
5. Select **Web app**
6. Execute as: **Your email**
7. Allow: **Anyone**
8. Copy the deployment URL

---

## 📱 **For Students**

### Taking the Test

1. **Open this link** (your teacher will send it)
2. **Enter your details:**
   - Name
   - Class (9th/10th)
   - Roll Number
3. **Select topics** you want to be tested on
4. **Click "Start Test"**
5. **For each question:**
   - **Desktop:** Click "Record" and speak your answer
   - **Mobile:** Type your answer in the text box
6. **Click "Next"** to continue
7. Results are automatically saved! ✅

---

## ✨ **Features**

✅ **Free to use** (no subscription)  
✅ **Speech recognition** (Desktop)  
✅ **Text input** (Mobile - no speech needed)  
✅ **Automatic result saving** (Google Sheets)  
✅ **Multiple topics** (choose what to test)  
✅ **Progress tracking** (see question progress)  
✅ **Works offline** (downloads your answers first)  

---

## 🔧 **Google Sheet Format**

Your Google Sheet should have:

### **Questions Sheet**
| Chapter | Question |
|---------|----------|
| Chapter 1 | What is...? |
| Chapter 1 | Define...? |
| Chapter 2 | Explain...? |

### **Results Sheet** (Auto-created)
| Timestamp | Student Name | Class | Roll | Questions | Topics | Responses |
|-----------|--------------|-------|------|-----------|--------|-----------|
| (auto) | (student) | (student) | (student) | (count) | (selected) | (all Q&A) |

---

## 📊 **Cost Breakdown**

- **HTML App:** FREE
- **Google Sheets:** FREE
- **Google Apps Script:** FREE
- **Hosting (Netlify):** FREE
- **Google Sheets API:** FREE (10,000 requests/day)

**Total Cost: $0** ✅

---

## 🆘 **Troubleshooting**

### *"Error: API Key invalid"*
- Check your API Key is correct
- Make sure Google Sheets API is enabled
- Verify Sheet is shared publicly

### *"Results not saving"*
- Check Google Apps Script deployment
- Verify Sheet has "Results" tab
- Check browser console for errors

### *"Speech not working on mobile"*
- Mobile uses text input (this is expected)
- Desktop uses microphone
- This is by design for compatibility

---

## 📧 **Support**

For issues, contact: [your email]

---

**Version:** 1.0  
**Last Updated:** 2026  
**License:** Free to use

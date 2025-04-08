# Web Down

Web Down is a script designed to simplify the creation of website downloaders. With this script, you can quickly build a website downloader without starting from scratch.

## 🚀 Preview
![Preview Image](path/to/preview/image)

## ⚙️ Installation
```bash
npm install
npm start
```

## 📖 Usage Guide
To add new social media platform downloader features, follow these steps:

### 1. Adding New Downloader
You can utilize the downloader API from https://elsty.xyz/documentation

Navigate to `/src/scraper/fitur` and create a code like this:

```javascript
const axios = require("axios");

class ElstyDownloader {
  constructor(url) {
    this.url = url;
  }

  async download() {
    try {
      const response = await callAPI(
        "elsty",
        "/api/download/social",
        "GET",
        {
          query: {
            url: this.url,
          },
          useApiKey: false,
        }
      );
      
      if (response.success) {
        if(response.data.images.length > 0 && !response.data.videos.length > 0) {
          return {
            status: "success",
            slide: true,
            video: false,
            table: false,
            data: {
              title: response.data.title,
              download: response.data.images.map((v) => {
                return { ext: "png", url: v.url };
              }),
            }
          };
        } else if(response.data.videos.length > 0) {
          return {
            status: "success",
            slide: true,
            video: false,
            table: false,
            data: {
              title: response.data.title,
              download: response.data.videos.map((v) => {
                return { ext: "mp4", url: v.url };
              }),
            }
          };
        }
      }
    } catch(error) {
      console.error(error);
      throw new Error('Failed to download from Instagram: ' + error.message);
    }
  }
}
module.exports = ElstyDownloader;
```

### 2. Integration Steps
Go to `src/scraper/index.js` and:
- Import your feature function:
```javascript
const FiturDownloader = require("./fitur.js")
```
- Integrate it in the index downloader (around line 19):
```javascript
Fitur: FiturDownloader // call feature function
```

### 3. Adding Link Regex
Navigate to `src/system/patterns.js` and add the regex pattern for your social media platform:
```javascript
fitur: /https://social.xyz/i
```

### 4. Adding Platform Data
- Go to `public` directory
- Import your platform icon to `img/icon` directory
- Upload your `icon.png` file
- Navigate to `data/platforms.json` and add your platform data:
```json
{
  "index": 5,
  "name": "Fitur",
  "icon": "/img/icons/fitur.png"
}
```

## 👥 Contributors
- [xvannn](https://github.com/xvannn07) - Project Creator
- [Fika bauk](https://github.com/apalah) - API Provider

## 📝 License
MIT License

# cloudflare-bypass
 A very basic Cloudflare UAM bypass (ideal for scrapers)
 Using puppeteer (a chromium based headless browser) to resolve the UAM check

## Usage
``` js
const cloudflareBypass = require('./src/cloudflare-bypass');
const axios = require('axios');
(async function(){
    const cookie = await cloudflareBypass({
        url: 'YOUR_URL',
    });

    if(cookie){
        // Parse cookie array into correct header format
        const cookies = cookie.map(item => `${item.name}=${item.value};`);
        const options = {
            headers: {
                'User-Agent': cookie.useragent,
                'Cookie': cookies
            }
        }
        const result = await axios.get('YOUR_URL', options);
        console.log(`Cloudflare bypass cookie + result`, cookies, result.data);
    }else{
        console.log("Failed to get cf_clearance cookie");
    }
})();
```

### Output
``` json
{
  "name": "cf_clearance",
  "value": "Example value",
  "domain": ".cloudflare-protected-url.com",
  "path": "/",
  "expires": 1670776181.662808,
  "size": 72,
  "httpOnly": true,
  "secure": true,
  "session": false,
  "sameSite": "None",
  "priority": "Medium",
  "sameParty": false,
  "sourceScheme": "Secure",
  "sourcePort": 443,
  "useragent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4691.0 Safari/537.36"
}
```

## TODO
- Add captcha resolver
# cloudflare-bypass
 A very basic Cloudflare UAM bypass (ideal for scrapers)
 Using puppeteer (a chromium based headless browser) to resolve the UAM check

## Usage
``` js
const cloudflareBypass = require('cloudflare-bypass');
(async function(){
    const cookie = await cloudflareBypass({
        url: 'https://cloudflare-protected-url.com'
    });

    console.log(`Cloudflare bypass cookie`, cookie);
})();
```

### Output
``` json
{
  name: 'cf_clearance',
  value: 'Example value',
  domain: '.cloudflare-protected-url.com',
  path: '/',
  expires: 1670776181.662808,
  size: 72,
  httpOnly: true,
  secure: true,
  session: false,
  sameSite: 'None',
  priority: 'Medium',
  sameParty: false,
  sourceScheme: 'Secure',
  sourcePort: 443
}
```

## TODO
- Add captcha resolver
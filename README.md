# playwright-extra-plugin-solve-cloudflare

> A plugin for [playwright-extra](https://github.com/berstend/puppeteer-extra/tree/master/packages/playwright-extra) that provides an automated cloudflare solution using the service [2CAPTCHA](https://2captcha.com/?from=18177101)

## Install

```bash
npm install playwright-extra-plugin-solve-cloudflare
```

If this is your first [playwright-extra](https://github.com/berstend/puppeteer-extra/tree/master/packages/playwright-extra) plugin here's everything you need:

```bash
npm install playwright playwright-extra puppeteer-extra-plugin-stealth playwright-extra-plugin-solve-cloudflare
```

## Usage

```js
import { chromium } from 'playwright-extra'
import solveCF from "playwright-extra-plugin-solve-cloudflare";
import stealth from "puppeteer-extra-plugin-stealth";
chromium.use(stealth());
chromium.use(
  solveCF({
    provider: {
      id: '2captcha',
      token: 'XXXXXXX' // REPLACE THIS WITH YOUR OWN 2CAPTCHA API KEY ⚡  
    }
  })
)
chromium.launch({ headless: true }).then(async browser => {
  const page = await browser.newPage()
  await page.goto("https://rucaptcha.com/demo/cloudflare-turnstile-challenge");
  await page.waitForSelector(`a[href="/demo/cloudflare-turnstile"]`,{timeout:700000}) // WAIT TARGET ELEMENT
  await page.screenshot({path:"target.png",fullPage:true});
  await browser.close()
})
```
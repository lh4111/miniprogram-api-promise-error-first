# miniprogram-api-promise-error-first

[![](https://img.shields.io/npm/v/miniprogram-api-promise-error-first)](https://www.npmjs.com/package/miniprogram-api-promise-error-first)

Extend WeChat miniprogram's api to surport promise.

# Installation

```
npm install --save miniprogram-api-promise-error-first
```

# Getting started
Call the method promisifyAll at the program entry (app.js), It only needs to be called once.

💨example:
```js
import { promisifyAll, promisify } from 'miniprogram-api-promise-error-first';

const wxp = {}
// promisify all wx's api
promisifyAll(wx, wxp)
console.log(wxp.getSystemInfoSync())

(async () => {
    const [err, systemInfo] = await wxp.getSystemInfo()
    if (err) {
        console.error(err)
        return
    }
    console.log(systemInfo)
});


(async () => {
    const [err] = await wxp.showModal()
    if (err) {
        console.error(err)
        return
    }
    
    wxp.openSetting()
});

// compatible usage
wxp.getSystemInfo({success(res) {console.log(res)}})

(async () => {
    // promisify single api
    const [err, res] = await promisify(wx.getSystemInfo)()
});

```

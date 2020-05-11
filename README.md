## hooman ![Build Status](https://img.shields.io/travis/sayem314/hooman.svg?style=flat-square&label=daily+builds)

HTTP interceptor using got to bypass Cloudflare DDOS protection / JavaScript challenge on Node.js

![](https://github.com/sayem314/hooman/raw/master/screenshot.png)

## Install

```shell
# with npm: npm i hooman got
yarn add hooman got
```

> got is peer-dependencies

## Usage Example

###### GET HTML

```js
const hooman = require('hooman');

(async () => {
  try {
    const response = await hooman.get('https://sayem.eu.org');
    console.log(response.body);
    //=> '<!doctype html> ...'
  } catch (error) {
    console.log(error.response.body);
    //=> 'Internal server error ...'
  }
})();
```

###### POST JSON

```js
const { body } = await hooman.post('https://httpbin.org/anything', {
  json: {
    hello: 'world',
  },
  responseType: 'json',
});
console.log(body.data);
//=> {hello: 'world'}
```

###### Pipe Stream

```js
// This is mandatory to set cookie first since .stream() doesn't fire hooks
await hooman(jsChallengePage);

// Now we can download files
const image = fs.createWriteStream('image.jpg');
hooman.stream(imageUrl).pipe(image);
```

###### Captcha

```js
const response = await hooman.get('https://sayem.eu.org', {
  captchaKey: '2captcha_api_key',
});
console.log(response.body);
```

> All you need to do is provide `captchaKey` and rest is done by hooman. It automatically detects if g/hCaptcha is present and need solving or can be solved. There are console.log print on hit as well.

![Test Results](https://github.com/sayem314/hooman/raw/master/captcha-test.png)

#### API

Please see available [API here](https://github.com/sindresorhus/got/blob/master/readme.md#api).

> All methods and props of [got](https://github.com/sindresorhus/got) should work fine.

## Support

I don't make any profit with this library. If you want to show your appreciation, you can donate me [here](https://sayem.eu.org/donate) :scream_cat: Thanks! You can also hire me for scraping solution, ping me and we will discuss further :smile:

> Made with :heart: & :coffee: by Sayem

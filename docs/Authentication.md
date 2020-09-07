# Authentication
To access the API, you need to provide an API key with every request. You can find your API key in your [account dashboard](app.simplerecommend.com/account).

It's extremely important you keep this API key secret. Only you and your system should have access to it. You shall not, in any way, store the API key on the front-end of your application since the client can access it. Because of this, we urge you to reserve communication with our API to the back-end of your system, where only you hold access to the source code and data.

To include the API key in a request, you set an HTTP header as such:
```
Api-Key: <Your Secret API Key>
```

An example in code, using NodeJS and Axios:
```javascript
const apiKey = process.env.MY_API_KEY // Fetch your API key from an environment variable.
const axios = require('axios');
const data = '{\n    "provider": "myProviderID"\n}';

const config = {
  method: 'post',
  url: 'https://api.simplerecommend.com/v1/actors',
  headers: {
      "Api-Key": apiKey // Here's where you set the header
  },
  data : data
};

axios(config)
.then(function (response) {
  console.log(JSON.stringify(response.data));
})
.catch(function (error) {
  console.log(error);
});

```
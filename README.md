# golden-retriever

![demo](https://i.imgur.com/BJaKKyc.jpg)

## Description

golden-retriever is an app for Slack which aims to inform the price in bitcoin 
in dollars (as well as in pounds and euros).
Simply invoking the slash command `/btc` will allow access to this information

Because the results for currency conversions are acquired through a request to 
the CoinDesk endpoint API, a very simple cache was implemented.
If two requests are made in a time interval of less than 10 seconds, access to CoinDesk 
is avoided and a previously saved value is returned.

## Working demo

A slightly modified version is running in a Webtask function (Auth0).

The POST endpoint for the `/btc` slash command is:
```
https://wt-2d0c1b127ddf2114db57608a0d9ef965-0.run.webtask.io/golden-retriever/api/btc
```

And finally the access through OAuth is (to be able to generate the "Add to Slack" button)
```
https://wt-2d0c1b127ddf2114db57608a0d9ef965-0.run.webtask.io/golden-retriever/oauth
```

## Setup

### Dependencies

```
npm i
```

### Environment variables

There is an example `.env` file, called `.env.sample` that has two required fields 
`SLACK_CLIENT_ID` and `SLACK_CLIENT_SECRET`.

The procedure for the app to work should be a copy of this file with the name .env 
and both variables should be filled with the values supplied by Slack at the moment of app creation.

In case the `.env` file does not exist or these two variables are not defined the application will not start.

### Local Development

```
npm run dev
```
This will start the app on port 9000

### Production

```
npm run prod
```
This command will transpile the complete project, execute it with supervisor and deattach it from terminal, this 
will allow that if the process for some reason it crashs, it will be automatically restarted.

### ngrok

Among the installed dependencies is `ngrok`, which allows to expose the local server of the application 
to the internet and thus use it as an endpoint for the slash command and access through OAuth.
To start `ngrok` and make the tunnel to the local server on 9000 port, just execute the command:

```
npm run ngrok
```

![ngrok](https://i.imgur.com/pd1feoS.jpg)


## Testing

```
npm test
```

## License
 
The MIT License (MIT)

Copyright (c) 2017 Sebastián Alvarez

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

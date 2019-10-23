# __Bespoken's Virtual Device: YAML Test Scripts Demo__
The Virtual Device Test Scripts are meant to make it easy for anyone to write automated tests for Alexa and Google Assistant.

They use a simple YAML syntax for allowing anyone to write complex (but still readable) end-to-end tests.

In this example, we are going to test one of our voice apps, Guess The Price, which is available for [Alexa](https://www.amazon.com/Juan-Perata-Guess-The-Price/dp/B0779F5ZDN) and [Google](https://assistant.google.com/services/a/uid/000000bef721231c).

## __Setup__

### __Install Bespoken Tools__
Make sure you have npm installed, [get it here](https://www.npmjs.com/get-npm).

Install Bespoken CLI to run the scripts. Open a command-line and run this command:  

```
npm install bespoken-tools -g
```
### __Install project dependencies__
This project utilizes the jest-html-reporter to create an HTML version of the test output.

To enable this, just run:
```
npm install
```

Within the project directory.

### __Get your Virtual Device Tokens__
You need to get a token to run the test scripts. A different token is needed per each locale and platform you want to test. Our example works for the Alexa and Google Assistant en-US version of the voice app, thus we need one token for Alexa and another one for Google. See [here](https://read.bespoken.io/end-to-end/setup/) for the instructions to get your tokens.

### __Configure your test scripts:__
Once you get your tokens, you need to include them in the `testing.json` configuration file, so you can run the tests.

The first YAML document of the test script (identified with three dashes, ---) defines the configuration section. In this section, you can indicate which locale and which voice to use.

```yaml
---
configuration:
  locale: en-US
  voiceId: Joey
```

### __Additional parameters__
The `testing.json` contains extra configuration parameters like these:
```json
{
  "type": "e2e",
  "findReplace": {
    "launch voice app": "open guess the price"
  },
  "homophones": {
    "lettuce": ["let us"],
    "is": ["as", "does", "it's"],
    "two": ["to", "2"],
    "contestant": ["contested"]
  },
  "trace": false,
  "silent": false
}
```
* __[Find and replace](https://read.bespoken.io/end-to-end/guide/#find-replace)__: This parameter will replace, within the test script files, the string `launch voice app` with `open guess the price` or `talk to guess the price`.
* __[Homophones](https://read.bespoken.io/end-to-end/guide/#configuration)__: Use this to specify words with a similar sound, for example, if you receive "let us" instead of "lettuce" or "to" instead of "two".
* __Trace and silent__: Both parameters allow you to get extra information from the response payload, to enable set trace to true and silent to false.

## __Running tests__
The test script files within the en-US folder work for both, Alexa and Google Assistant versions of the voice app.

To run the test script files you need to overwrite some parameters from the command line. For example, if you are an MS Windows user you can run a specific test file for the Alexa skill like this:

```BASH
$ set "findReplace.launch voice app=open guess the price" & bst test en-US\onePlayerGame.e2e.yml --platform alexa
```

We are overwriting the `testing.json` `launch voice app` parameter with the value of the environment variable `findReplace.launch voice app`. The same happens when we use the `--platform alexa` flag.

If we want to execute a test script for the Google Assistant version of the voice app we can write something like this:

```BASH
$ set "findReplace.launch voice app=talk to guess the price" & bst test en-US\onePlayerGame.e2e.yml --platform google
```

Notice how the invocation name changes.

That's it! Now just wait, and your tests will run. The results will be shown in the console, as well as summarized in the HTML report at `<PROJECT_DIR>/test-report.html`


## More Info and Docs
See the full docs for the test scripts [here](https://read.bespoken.io/end-to-end/getting-started/).

## Questions/Feedback?
Help is only a few clicks away. Have questions or feedback? Email us at [support@bespoken.io](mailto:support@bespoken.io).

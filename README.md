# __Bespoken Virtual Device: YAML Test Scripts Demo__
The Virtual Device Test Scripts are meant to make it easy for anyone to write automated tests for Alexa and Google Assistant.

They use a simple YAML syntax for allowing anyone to write complex (but still readable) end-to-end tests.

## __Setup__

### __Install Bespoken Virtual Device__
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
First, you need to get a token. A different token is needed per each locale you want to test. Our example works for the Alexa en-US and de-DE versions of the voice app; and for Google Assistant en-US, so you need 3 tokens. See [here](https://read.bespoken.io/end-to-end/setup/) for the instructions to get your tokens.

### __Configure your test scripts:__
We have included our tokens on the `testing.json` file in this repo so you can run them and see them in action. You should add your tokens when creating your own test scripts.

**`FYI - the included tokens are so that new users can get started quickly. However, they are common tokens and will NOT work as reliably as creating your own.`** 

Please follow the steps above to create your own Virtual Device Tokens.

* Within your test script add a configuration section like the example shown below.
* Add the locale for the test script and the Amazon Polly voiceId.
```yaml
---
configuration:
  locale: en-US
  voiceId: Joey
```

### __Additional parameters__
You will notice there is a file named `testing.json` in the sample project. This file contains extra configuration parameters like these:
```json
{
  "type": "e2e",
  "findReplace": {
    "INVOCATION_NAME": "open bring"
  },
  "homophones": {
    "lettuce": ["let us"],
    "figs": ["six","6","vicks"]
  },
  "trace": false,
  "jest": {
    "silent": true
  }
}
```
* __Find and replace__: This parameter will replace, within the test script files, the string `INVOCATION_NAME` with `open bring`.
* __Homophones__: Use this to specify words with a similar sound, for example, if you receive "let us" instead of "lettuce" or "six" instead of "figs".
* __Trace and silent__: Both parameters allows you to get extra information from the response payload, to enable set trace to true and silent to false.

## __Running tests__
The test script files within de-DE folder have been created just for the German Bring Alexa skill, and the en-US ones work for both, Alexa and Google Assistant versions of the voice app.

To run a particular file within the German scripts, enter:
```
bst test de-DE\my-test-file.yml
```

To run a directory containing many tests, provide the directory path instead:
```
bst test test-directory
```

That command will run all yml files that are contained within that directory.

To run the en-US test script files you need to overwrite some parameters from the command line. For example, if you are an MS Windows user you can run a specific test file for the Alexa skill like this:

```BASH
$ set "findReplace.INVOCATION_NAME=open bring" & bst test en-US\launchRequest.e2e.yml --platform alexa
```

We are overwriting the `testing.json` `INVOCATION_NAME` parameter with the value of the environment variable `findReplace.INVOCATION_NAME`. Same happens when we use the `--platform alexa` flag.

If we want to execute a test script for the Google Assistant version of the voice app we can write something like this:

```BASH
$ set "findReplace.INVOCATION_NAME=talk to bring shopping list" & bst test en-US\launchRequest.e2e.yml --platform google
```

Notice how the invocation name changes.

That's it! Now just wait, and your tests will run. The results will be shown in the console, as well as summarized in the HTML report at: `<PROJECT_DIR>/test-report.html`


## More Info and Docs
See the full docs for the test scripts [here](https://read.bespoken.io/end-to-end/getting-started/).

## Questions/Feedback?
Help is only a few clicks away. Have questions or feedback? Email us at [support@bespoken.io](mailto:support@bespoken.io).

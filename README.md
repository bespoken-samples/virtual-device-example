# __Bespoken's Virtual Device: YAML Test Scripts Demo__
The Virtual Device Test Scripts are meant to make it easy for anyone to write automated tests for Google Assistant.

They use a simple YAML syntax for allowing anyone to write complex (but still readable) end-to-end tests.

In this simple example, we are going to test the [Google](https://assistant.google.com/services/a/uid/000000bef721231c) version of Guess The Price, one of our voice apps. It is also possible to use one single set of tests to QA an app created for both, Alexa and Google platforms. To know how to do it, read [here](https://github.com/bespoken-samples/virtual-device-example/tree/one-set-of-tests-for-alexa-google).

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

### __Get your Virtual Device Token__
You need to get a token to run the test scripts. A different token is needed per each locale and platform you want to test. Our example works for the Google en-US version of the voice app, thus we need just one token. See [here](https://read.bespoken.io/end-to-end/setup/) for the instructions to get your token.

### __Configure your test scripts:__
Once you get your token, you need to include it in the `testing.json` configuration file, so you can run the tests.

The first YAML document of the test script (identified with three dashes, ---) defines the configuration section. In this section, you can indicate which locale and which voice to use. We support both, [Amazon Polly](https://docs.aws.amazon.com/polly/latest/dg/voicelist.html) and [Google WaveNet](https://cloud.google.com/text-to-speech/docs/voices) voices.

```yaml
---
configuration:
  locale: en-US
  voiceId: en-US-Wavenet-D
```

### __Additional parameters__
The `testing.json` contains extra configuration parameters like these:
```json
{
  "type": "e2e",
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
* __[Homophones](https://read.bespoken.io/end-to-end/guide/#configuration)__: Use this to specify words with a similar sound, for example, if you receive "let us" instead of "lettuce" or "to" instead of "two".
* __Trace and silent__: Both parameters allow you to get extra information from the response payload, to enable set trace to true and silent to false.

## __Running tests__
The test script files within the en-US folder work for the Google version of the voice app.

To run a test script use the `test` command from the command line like this:

```BASH
$ bst test en-US\invokingVoiceApp.e2e.yml
```
To run the entire set of tests in the en-US folder, run the `test` command as follow:

```BASH
$ bst test en-US\
```

That's it! Now just wait, and your tests will run. The results will be shown in the console, as well as summarized in the HTML report at `<PROJECT_DIR>/test-report.html`


## More Info and Docs
See the full docs for the test scripts [here](https://read.bespoken.io/end-to-end/getting-started/).

## Questions/Feedback?
Help is only a few clicks away. Have questions or feedback? Email us at [support@bespoken.io](mailto:support@bespoken.io).

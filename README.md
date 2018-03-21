# Bespoken Virtual Device: YAML Test Scripts Demo
The Virtual Device Test Scripts are meant to make it easy for anyone to write automated tests for Alexa (and Google Assistant, soon).

They use a simple YAML syntax for allowing anyone to write complex (but still readable) end-to-end tests.

## Setup

### Install Bespoken Virtual Device
Make sure you have npm installed, [get it here](https://www.npmjs.com/get-npm).

Install the virtual-device-sdk to run the scripts. Open a command-line and run this command:  

```
npm install virtual-device-sdk -g
```
### Get your Virtual Device Token
First, you need to get a token. See [here for instructions](https://github.com/bespoken/virtual-device-sdk/blob/master/docs/token_guide.md).

### Create a .env file:  
This file contains the tokens for each locale and other important environment variables. We have included our .env file 
in this repo so you can run the test scripts and see them in action. Our .env file contains our tokens. You should add
yours when creating your own test scripts. 

* Create a file ".env" in the folder where you are going to run the scripts or copy the example.env and save it as .env.
* Add your tokens. By default, the token will be stored as:
```
VIRTUAL_DEVICE_TOKEN=<MY_TOKEN_VALUE>
```
* If the tests use more than one token, they will be selected based on the locality appended at the end:
```
VIRTUAL_DEVICE_TOKEN_DE_DE=<DE_DE_TOKEN_VALUE>
VIRTUAL_DEVICE_TOKEN_EN_GB=<EN_GB_TOKEN_VALUE>
VIRTUAL_DEVICE_TOKEN_EN_US=<EN_US_TOKEN_VALUE>
```
* If you are using different invocation names for your skill you can use the INVOCATION_NAME parameter.This will cause any instances of the value INVOCATION_NAME to be replaced by <my_invocation_name> in the test scripts.
```
replace.INVOCATION_NAME=<my_invocation_name>
```
So a script that looks like this:
```yaml
"open INVOCATION_NAME and say hello": "*"
```

Will be turned into this:
```yaml
"open my_invocation_name and say hello": "*"
```
This is a useful feature for tests that are run against multiple instances of the same skill, where there are slight variations in the input or output.

## Running tests
Once you have created your tests, you can run a particular file by entering:
```
bvd my-test-file.yml
```

To run a directory containing many tests, provide the directory path instead:
```
bvd test-directory
```

That command will run all yml files that are contained within that directory.

That's it! Now just wait, and your tests will run.


##Questions/Feedback? 
Help is only a few clicks away. Have questions or feedback? Email us at [ivan@bespoken.io](mailto:ivan@bespoken.io) or [jpk@bespoken.io](mailto:jpk@bespoken.io) 
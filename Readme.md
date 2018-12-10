# AWS Lambda Runtime sample - PHP


## Overview

This repo contains an implementation of PHP runtime layer with AWS Lambda.

Files:
1. `runtime/php` - Statically compiled PHP 7.2.11 on alinux 2017.03
2. `runtime/bootstrap` - This is a Bash script. This initizlizes and starts the PHP runtime
3. `runtime/runtime.php` - This contains the interations with AWS runtime API and the main logic to execute the function handler
4. `function/Function.php` - Sample lambda function

## Handler

This runtime expects the function handler in AWS Lambda configuration in the form `filename.handler`. This means that if you configure AWS lambda's handler field as `filename.handler` the runtime layer will look for a file `fielname.php` in your function code and execute the function `handler` passing in the event payload as the first argument. Refer to file `function/Function.php` in this repositiory for example.

# Configuration

To use this runtime:
1. Download or clone this repo
2. Zip the files bootstrap, static PHP binary and runtime.php in the runtime folder of this repo
3. Create a layer in AWS and upload the zip file created in above step
3. Take not of the ARN generated in the layer
5. Create a Lambda function from scratch. Select custom runtime.
6. Click con layers and paste in the ARN from the above step
7. Define the handler in lambda function `function.handler`
8. Create a file `function.php` with a function called `handler($eventData)`, this function will be called when lambda is invoked.

You will see "hello" returned upon testing.

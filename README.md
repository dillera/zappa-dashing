# zappa-dashing

Monitor your AWS Elastic Beanstalk environment in different regions with a health dashboard.

This project consists only of a small portion of "application code" (see `server.py` plus `static/app.js`)
and is made possible thanks to:

* [zappa.io](https://www.zappa.io) deploy AWS Lambda function in only a matter of seconds
* [mini-dashing](https://github.com/pushmatrix/mini-dashing) JavaScript version of 
  dashing resp. [smashing](https://github.com/Smashing/smashing) 


To get an better idea on what you can expect, here is an example screenshot:

![Screenshot of zappa-dashing](http://i.imgur.com/vRFYJoGr.png)

*Note:* Since AWS Lambda does not support Python 3 yet, we have to use Python 2(.7) when
working with the Flask app resp. deploying it with the help of zappa.


## Initial Setup

To setup your local machine you need to execute once:

	$ virtualenv-2 venv
	$ source venv/bin/activate
	$ pip install -r requirements.txt

To allow the zappa role accessing AWS health information, please ensure
that you attached the IAM role `ZappaLambdaExecution`
the policy `AWSElasticBeanstalkEnhancedHealth`.


## Customize to your needs

Copy `settings-sample.py` to `settings.py` and modify as required to your environment,
same for `static/settings-sample.js`. Specifically adjust the AWS regions to your needs.

The monitor screen is defined in `templates/home.html`, make sure that the CSS IDs do correlate
with the regions you setup in the previous settings files.


## Initial Deployments

To install the `dev` environment on AWS Lambda with the help of zappa initially:

	$ zappa deploy dev  

As soon as the ZIP is packaged and uploaded, the code will be deployed as AWS Lambda function and
the endpoints registered with the AWS API gateway. When finished you will receive a URL to
access your function.


## Development Workflow

Test on your local machine:

	$ source venv/bin/activate
	$ ./server.py

Open your browser and visit [http://localhost:5000](http://localhost:5000).

Once you are happy with the results, you might want to deploy to AWS API Gateway + Lambda with
the help of:

	$ zappa update dev


## Further helpful commands

Show access log for the `dev` environment:

    zappa tail dev --http

Leave virtual environment:

	$ deactivate


## Contribution 

Contributions are more than welcome, please file an issue or even better submit a
pull request :-)

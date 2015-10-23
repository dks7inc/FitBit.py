# A python library for the FitBit API

Originally created by [jpattel](https://github.com/jplattel/FitBit.py), who "Didn't see one that fitted my needs so I build my own."

Adapted to use the newer OAuth 2.0 (fitbit.com/oauth2) API as OAuth 1.0a is being deprecated and doesn't offer access to newer statistics such as heartrate.


## Usage

Edit the fitbit.py file with your client id, secret, callback uri, and required scope.

	import fitbit
	z = fitbit.Fitbit()

For a simple example see: ```example.py```.

Get the authorization URL for completion by logged in FitBit user in the browser:

    auth_url = z.GetAuthorizationUri()

The access code is part of the redirect URL as the ```code=[access_code]``` GET.

Request an access and refresh token using the access code (you have 10 minutes)

    access_token, refresh_token = z.GetAccessToken(access_code)

Store both tokens for later usage. You can now call the API with it:

	response, status_code = z.ApiCall(access_token, apiCall='/1/user/-/activities/log/steps/date/today/7d.json')

All responses for the functions are received in JSON but are also available in XML.

In case the access token has expired (```status_code```: ```401```) a new pair of tokens can be obtained using the refresh token

    access_token, refresh_token = z.RefAccessToken(refresh_token)

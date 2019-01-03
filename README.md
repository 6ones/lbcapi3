lbcapi3 is a simple python3 wrapper for the LocalBitcoins API to make it easier to develop applications that interface with LocalBitcoins.com.
For the original library - python2, check out https://github.com/LocalBitcoins/lbcapi

To install
==========
The easiset way to install lbcapi is to use pip. Open up a terminal window and type the following command to install

    pip install lbcapi3

If you're running OS X you may need to first install pip using homebrew. First, download and install Homebrew and then run the command

    brew install python

If you're running Windows pip will come built-in with the latest version of Python.

Usage example (using HMAC)
============
This example uses the library to call the /api/myself/ endpoint

```python
from lbcapi import api

hmac_key = 'You HMAC secret here'
hmac_secret = 'Your HMAC secret here'

conn = api.hmac(hmac_key, hmac_secret)
conn.call('GET', '/api/myself/').json()
```

To find out all the available API calls please see the API documentation on LocalBitcoins.com
https://localbitcoins.com/api-docs/

Pagination example
============
Pagination seems to cause problems so, here is an example on how to do it with this library
```python 
import urllib.parse
from lbcapi import api

hmac_key = 'Your HMAC key here'
hmac_secret = 'Your HMAC secret here'

conn = api.hmac(hmac_key, hmac_secret)
ads_json = conn.call('GET', '/api/ads/').json()
parsed = urllib.parse.urlparse(ads_json['pagination']['next'])
params = urllib.parse.parse_qs(parsed.query)
ads_json_II = conn.call('GET', '/api/ads/', params=params).json()

```



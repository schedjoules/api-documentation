# Events

Please note that this API is still in beta.

## Set yourself up
Mail us at hello@schedjoules.com and we'll provide you with your API key.

## Making a request
For all requests the following headers and parameters are required:
```
Headers
- API-VERSION		string		Version of API you are using	'1'
- Authorization		string		Your API key					'Token token="123456789abcdefghijklmopqrstuvwxyz"

Parameters
- u 			string		UUID per user/device (> 19 chars)		'123e4567-e89b-12d3-a456-426655440000'
```

### Search
```
GET /events
			
Optional GET parameters
- q			string		search in summary and description	'Ajax'
- latlng		float		search in area				'52.3,4.9'
- radius		integer		meters around search area	'10000'
- start_at_or_after	datetime	search from in UTC			'2016-10-01T19:00:00'	default: now
- start_before		datetime	search til in UTC			'2017-12-10T06:00:00'
- results		integer		nr of results returned		'15'	default: 20. max: 100
```

Example request: https://api.schedjoules.com/events?latlng=52.3,4.9&radius=10000&u=123e4567-e89b-12d3-a456-426655440000

### Get 1 event by ID
```
GET /events/{event_id}
```

## Response

```
- uid					string		event ID		
- created				datetime	event created at
- updated				datetime	event last updated at
- title					string		event title
- locations				object
	- start				key
		- name			string		location name
		- coordinates		float		location geo coordinates
		- address		key			
			- street	string		location street
			- region	string		location region
			- postcode	string		location postcode/zipcode
			- city		string		location city
			- country	string		location country
- isAllday				boolean
- start					datetime
- timeZone				string
- duration				string
- links					object
	- rel				string
	- type				string
	- href				string
	- properties			string
```

### Pagination
By default the api returns a maximum of 100 results per request. The [link headers](https://tools.ietf.org/html/rfc5988) let you scroll into the future or past.

### Actions
Every event is actionable. We provide links for buying tickets, navigation, share and add-to-calendar.

```
GET /events/{EVENT_ID}/actions?u={UID}
Required GET parameters
- id	string		event UID							'9cd4568cc969'
- u	string		UUID per user/device (> 19 chars)	'123e4567-e89b-12d3-a456-426655440000'
```

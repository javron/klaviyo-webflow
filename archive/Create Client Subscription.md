Create Client Subscription
post
https://a.klaviyo.com/client/subscriptions
Creates a subscription and consent record for email and/or SMS channels based on the provided email and phone_number attributes, respectively. One of either email or phone_number must be provided.

This endpoint is specifically designed to be called from publicly-browseable, client-side environments only and requires a public API key (site ID). Never use a private API key with our client-side endpoints.

Do not use this endpoint from server-side applications.
To subscribe profiles from server-side applications, instead use POST /api/profile-subscription-bulk-create-jobs.

Profiles can be opted into multiple channels: email marketing, SMS marketing, and SMS transactional. You can specify the channel(s) to subscribe the profile to by providing a subscriptions object in the profile attributes.

If you include a subscriptions object, only channels in that object will be subscribed. You can use this to update email or phone on the profile without subscribing them, for example, by setting the profile property but omitting that channel in the subscriptions object. If a subscriptions object is not provided, subscriptions are defaulted to MARKETING.

Rate limits:
Burst: 100/s
Steady: 700/m

Scopes:
subscriptions:write

Query Params
company_id
string
required
Your Public API Key / Site ID. See this article for more details.

Body Params
data
object
required

data object
type
string
required

subscription
attributes
object
required

attributes object
custom_source
string
A custom method detail or source to store on the consent records for this subscription.

Homepage footer signup form
profile
object
required

profile object
data
object
required

data object
type
string
required

profile
id
string
Primary key that uniquely identifies this profile. Generated by Klaviyo.

string
attributes
object
required

attributes object
email
string
Individual's email address

sarah.mason@klaviyo-demo.com
phone_number
string
Individual's phone number in E.164 format

+15005550006
external_id
string
A unique identifier used by customers to associate Klaviyo profiles with profiles in an external system, such as a point-of-sale system. Format varies based on the external system.

string
anonymous_id
string
Id that can be used to identify a profile when other identifiers are not available

01GDDKASAP8TKDDA2GRZDSVP4H
_kx
string
Also known as the exchange_id, this is an encrypted identifier used for identifying a
profile by Klaviyo's web tracking.

You can use this field as a filter when retrieving profiles via the Get Profiles endpoint.

string
first_name
string
Individual's first name

Sarah
last_name
string
Individual's last name

Mason
organization
string
Name of the company or organization within the company for whom the individual works

Example Corporation
locale
string
The locale of the profile, in the IETF BCP 47 language tag format like (ISO 639-1/2)-(ISO 3166 alpha-2)

en-US
title
string
Individual's job title

Regional Manager
image
string
URL pointing to the location of a profile image

https://images.pexels.com/photos/3760854/pexels-photo-3760854.jpeg
location
object

location object
address1
string
First line of street address

89 E 42nd St
address2
string
Second line of street address

1st floor
city
string
City name

New York
country
string
Country name

United States
latitude
Latitude coordinate. We recommend providing a precision of four decimal places.


string

number
string
longitude
Longitude coordinate. We recommend providing a precision of four decimal places.


string

number
string
region
string
Region within a country, such as state or province

NY
zip
string
Zip code

10017
timezone
string
Time zone name. We recommend using time zones from the IANA Time Zone Database.

America/New_York
ip
string
IP Address

127.0.0.1
properties
object
An object containing key/value pairs for any custom properties assigned to this profile


properties object
string
pseudonym
Dr. Octopus

Add Field
meta
object

meta object
patch_properties
object
Specify one or more patch operations to apply to existing property data


patch_properties object
append
object
Append a simple value or values to this property array


append object
string
skus
92538

Add Field
unappend
object
Remove a simple value or values from this property array


unappend object

Add Field
unset
string
Remove a key or keys (and their values) completely from properties

subscriptions
object

subscriptions object
email
object
The subscription parameters to subscribe to on the "EMAIL" Channel.


email object
marketing
object
required
The parameters to subscribe to on the "EMAIL" Channel. Currently supports "MARKETING".


marketing object
consent
string
required
The Consent status to be set as part of the subscribe call. Currently supports "SUBSCRIBED".


SUBSCRIBED
consented_at
date-time
The timestamp of when the profile's consent was gathered. This should only be used when syncing over historical consent info to Klaviyo; if the historical_import flag is not included, providing any value for this field will raise an error.

2025-04-15T13:42:41.278Z
sms
object
The subscription parameters to subscribe to on the "SMS" Channel.


sms object
marketing
object
The parameters to subscribe to marketing on the "SMS" Channel.


marketing object
consent
string
required
The Consent status to be set as part of the subscribe call. Currently supports "SUBSCRIBED".


SUBSCRIBED
consented_at
date-time
The timestamp of when the profile's consent was gathered. This should only be used when syncing over historical consent info to Klaviyo; if the historical_import flag is not included, providing any value for this field will raise an error.

2025-04-15T13:42:41.278Z
transactional
object
The parameters to subscribe to transactional messaging on the "SMS" Channel.


transactional object
consent
string
required
The Consent status to be set as part of the subscribe call. Currently supports "SUBSCRIBED".


SUBSCRIBED
consented_at
date-time
The timestamp of when the profile's consent was gathered. This should only be used when syncing over historical consent info to Klaviyo; if the historical_import flag is not included, providing any value for this field will raise an error.

2025-04-15T13:42:41.278Z
relationships
object
required

relationships object
list
object
required

list object
data
object

data object
type
string
required

list
id
string
required
The list ID to add the newly subscribed profile to.

Y6nRLr
Headers
revision
string
required
Defaults to 2025-04-15
API endpoint revision (format: YYYY-MM-DD[.suffix])

2025-04-15
Responses
202
Success


4XX
Client Error


5XX
Server Error

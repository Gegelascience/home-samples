# Step 0: Install Python 3 and requests module
Download and install the Python 3 then install with pip command 'requests' library. You can now run the snippet with python command. 

# Step 1: Requesting resources
```Python
import requests

baseUrl = "http://services.odata.org/v4/TripPinServiceRW/"
response = requests.get(baseUrl +"People")

if response.status_code != 200:
    print("error: " + str(response.status_code))
    print(response.text)
else:
    print("success")
    print(response.json())

```

# Step 2: Requesting an individual resource
```Python
import requests

baseUrl = "http://services.odata.org/v4/TripPinServiceRW/"
response = requests.get(baseUrl +"People('russellwhyte')")

if response.status_code != 200:
    print("error: " + str(response.status_code))
    print(response.text)
else:
    print("success")
    print(response.json())
```

# Step 3: Queries
```Python
import requests

baseUrl = "http://services.odata.org/v4/TripPinServiceRW/"

queryparams = {
    "$top":2,
    "$select":"FirstName, LastName",
    "$filter":"Trips/any(d:d/Budget gt 3000)"
}

response = requests.get(baseUrl +"People", params=queryparams)

if response.status_code != 200:
    print("error: " + str(response.status_code))
    print(response.text)
else:
    print("success")
    print(response.json())
```

# Step 4: Creating a new resource
```Python
import requests

baseUrl = "https://services.odata.org/v4/(S(dhzln0mseufepcdhv3dzuuh4))/TripPinServiceRW/"

newPerson = {
    "UserName":"jeanbon",
    "FirstName":"Jean",
    "LastName":"Bon",
    "Emails":[
        "jeanbon2@example.com"
    ],
    "AddressInfo":[
        {
            "Address": "187 Suffolk Ln.",
            "City": {
                "CountryRegion": "United States",
                "Name": "Boise",
                "Region": "ID"
            }
        }
    ],
    "Gender": "Male"
}
headers= {
    'OData-Version': '4.0',
    'OData-MaxVersion': '4.0'
}

response = requests.post(baseUrl +"People",headers=headers, json=newPerson, allow_redirects=False)

if response.status_code != 201:
    print("error: " + str(response.status_code))
    print(response.request.method)
    print(response.request.url)
    print(response.headers)
    print(response.text)
else:
    print("success")
    print(response.json())
```

# Step 5: Relating resources
```Python
import requests

baseUrl = "http://services.odata.org/v4/TripPinServiceRW/"

payload = {
    "@odata.id": "http://services.odata.org/V4/TripPinServiceRW/People('russellwhyte')/Trips(0)"
}

response = requests.post(baseUrl +"People('lewisblack')/Trips/$ref", json=payload)

if response.status_code != 204:
    print("error: " + str(response.status_code))
    print(response.text)
else:
    print("success")
    print(response.json())

```

# Step 6: Invoking a function
```Python
import requests

baseUrl = "http://services.odata.org/v4/TripPinServiceRW/"
response = requests.get(baseUrl +"People('russellwhyte')/Trips(0)/Microsoft.OData.SampleService.Models.TripPin.GetInvolvedPeople()")

if response.status_code != 200:
    print("error: " + str(response.status_code))
    print(response.text)
else:
    print("success")
    print(response.json())
```
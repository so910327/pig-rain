## Datas
|table name| items(type) | source |
|----------|-------------|--------|
| pig-user | user-email(S,HASH), password(S) | dynamodb(./lib/connect.js)|
|pig-notification| user-email(S), area-id(S,HASH), timespan-id(N,RANGE), threshold(N)|dynamodb(./lib/connect.js)
| pig-area | see note 1., 2. | ./data/pig-area.json (./data/create-area.js) |
| pig-timespan | [] |./data/pig-timespan |
| pig-city | see note 1., 3.| ./data/area-county.json (./data/create-area.js) |
| pig-county | see note 1., 4.| ./data/area-county.json (./data/create-area.js) |
| pig-stop | see note 1., 5.| ./data/area-county.json (./data/create-area.js) |

0. about id
	* city-id: AreaN, N=1,2,3,...
	* county-id: CN, N=1,2,3,...
	* stop-id: [0-9A-Z]{5}
1. pig-area.json
	
	```
	{
		<stop-id, type = string>:
			{
				"city": <city name, type = string>,
				"stop": <stop name, type = string>,
				"addr": <stop address, type = string>
			}
	},
	{
		<stop-id, type = string>:
			{
				"city": <city name, type = string>,
				"stop": <stop name, type = string>,
				"addr": <stop address, type = string>
			}
	},...	
	```


2. pig-city.json

	```
	{
		<city-id, type = string>: <city name, type = string>,
		<city-id, type = string>: <city name, type = string>,
		...		
	} 
	```

3. pig-county.json

	```
	{
		<city-id, type = string>: 
		{
			<county-id, type = string>: <county name, type = string>,
			<county-id, type = string>: <county name, type = string>,
			...	
		},
		<city-id, type = string>: 
		{
			<county-id, type = string>: <county name, type = string>,
			<county-id, type = string>: <county name, type = string>,
			...	
		},
		...
	} 
	```
	
3. pig-stop.json

	```
	{
		<county-id, type = string>: 
		{
			<stop-id, type = string>:
			{
				"name": <stop name, type = string>,
				"addr": <stop name, type = string>
			},
			<stop-id, type = string>:
			{
				"name": <stop name, type = string>,
				"addr": <stop name, type = string>
			},
			...
		},
		<county-id, type = string>: 
		{
			<stop-id, type = string>:
			{
				"name": <stop name, type = string>,
				"addr": <stop name, type = string>
			},
			<stop-id, type = string>:
			{
				"name": <stop name, type = string>,
				"addr": <stop name, type = string>
			},
			...
		},
		...
	} 
	```
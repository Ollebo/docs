#Maps

How maps are processed and stored in Olle bo 


## Adding new map 


![Map Maker](/draw/map-maker.png "Map Maker")


- Users uploads a map from our client Map is saved with format {USER / Company } - {UID}. geotiff for geotiff images
- When map is uploada a API Request PUT /maps/ to the API 
- When the Api gets a new map a create map job is added to the nats que
- Make-map tool is triggerd by the que and process the map. From the incomming bucket and adds it to the public ore private bucket
- When Map is process the Api set it to complete




## Accessing maps


![Map Maker](/draw/map-access.png "Map Access")

When accessing map there are 3 diffrent ways.

### Our Maps
Our maps are redering and displayed from or map server rendering the global openstreat map and data.*
Our own maps are also rendered using posgis database.


### Public Maps
All public maps are stored in a S3 Bucket and accesble using the url usr/uid/ tiles format.
They are server from the s3 bucket using cloudfront for cache and rendering.

Example

'''
maps.ollebo.com/layers/Mattias/1234-1234-1234-1234/x/y/x.png
'''


### Private Maps
Private maps are stored in the private s3 bucket in the same format as the public. But the maps are not public assacble.
For access control pur API gatweay. And will verify the access to the maps.
Maps are stored in the same setup but access to the users in diffrent way

Example

'''
private.ollebo.com/layers/Mattias/1234-1234-1234-1234/x/y/x.png
'''

To verify the access to the maps in private.ollebo.com/layers/Mattias/1234-1234-1234-1234/x/y/x.png the user need to be part of the group with the name Mattias.



### Own hosted

(To be resolved )
Own hosted then using our stack bring up a small self hosted map service.*
The stack will connect and make maps to display. 
The self hopsted stack will 

- Find new maps detected localy
- Render tha maps so they are avviable to display
- Update the User uing the api to add the new created maps
- Set the map to Private ore Public mode

- Setup there own access control to the maps 






   
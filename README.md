# immich-n8n

## Master
I have not added this one to the workflows folder as it does contain all my credentials but it is also very simple and does not contain any logic.
### Description
My master workflow sequences all the other flows calls:
- Add to album and archive my screenshots
- Add to album and archive my partner screenshots
- Update People albums
- Update People album (a bigger one I have separated from the previous call)
### Expected Input parameters
None
### Screenshot
![image](https://github.com/user-attachments/assets/69153212-7778-4621-b4cc-6d20336d8ec9)

## Immich Screenshots
### Description
This flow must be called from another flow with the required input parameters.
It will search for all the assets taken after the input date, not archived and with PNG in the original file name, add them to the input album and archive them.
### Expected Input parameters
```
{
    "BaseURL": "https://my.immich/api/",
    "apiKey": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "takenAfter": "YYYY-MM-DD",
    "screenshotAlbumID": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
}
```
### Screenshot
<img width="656" alt="image" src="https://github.com/user-attachments/assets/ec62f597-ec5f-4a2a-96ff-f0ec3f4c19a4">

## Immich People Album
### Description
This flow must be called from another flow with the required input parameters. Input parameters are a list of albums with a list of immich users and for each user a list of people IDs
For a personal album, 1 user will be required
for a shared album, multiple users/peoples assets can be added to the same albumID
### Expected Input parameters
```
{
    "BaseURL": "https://my.immich.app/api/",
    "Albums": [
        {
            "albumID": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "albumName": "Blablabla",
            "apiKey": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
            "users": [
                {
                    "persons": [
                        "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
                    ],
                    "apiKey": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
                },
                {
                    "persons": [
                        "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
                    ],
                    "apiKey": "yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy"
                }
            ]
        }
    ]
}
```
### Screenshot
<img width="695" alt="image" src="https://github.com/user-attachments/assets/e1160d7a-aef8-46f6-9cb2-b08e993b18a0">

### TODO
I do have 1 ginormous album with 50k+ assets. That solution may not be scalable for that matter. If immich api allows to pull albums assets between 2 dates at some point this would be a good solution.
## Immich People Album Sub
### Description
This flow is called from the previous flow with the required input parameters. 
It recursively pulls assets between 2 dates until the returned count < 250 items and then add them to the designated album.
### Expected Input parameters
```{
    "startDate": "YYYY-MM-DD",
    "endDate": "YYYY-MM-DD",
    "persons": [
        "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
    ],
    "apiKey": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "albumID": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "BaseURL": "https://my.immich.app/api/",
    "assetIDs": [
        "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
        "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
    ]
}
```
### Screenshot
![image](https://github.com/user-attachments/assets/8207b7d0-bfbc-4f73-97b6-6642f09ce83d)

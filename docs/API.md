# API
End points and information on how to consume them. Pay attention to describing your request and response cycles. These are the main components of your API where users will be  interacting with your services, so pay close attention to this.

## Create a new Actor
### `POST /actors`
Example response:
```
{
    "token": "QuiteALongRandomTokenYouShouldStoreAssociatedWithUser"
}
```

## Create Event
### `POST /events`
Example request body:
```
{
    "events": [
        {
            "actor": "OneSpecificActorsToken", // String; Required
            "item": "OneOfYourItemsUniqueID", // String; Required
            "rating": 5 // Number; Required
            "tag": "bought_item" //Optional
        }
    ]
}
```

### `DELETE /events`
Example request body:
```
{
    "match": [
        {
            "actor": "actorTokenToDelete"
        },
        {
            "tag": "oldTagToDelete"
        }
    ]
}
```

## Get Recommendations
### `GET /recommendations?actor=<TOKEN>`
Example response body:
```
{
    "actor1_ID" : {
        "items": [
            "item1_ID",
            "item2_ID",
            "item3_ID"
        ]
    }
}
```

<details>
  <summary>Example Code In Javascript</summary>
      
  Spoiler text. Note that it's important to have a space after the summary tag. You should be able to write any markdown you want inside the `<details>` tag... just make sure you close `<details>` afterward.
  
  ```javascript
  console.log("I'm a code block!");
  ```
</details>
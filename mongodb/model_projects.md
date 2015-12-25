### Alternativa para modelagem da coleção projects

```js
{
    "name": String,
    "description": String,
    "date_begin": Date,
    "date_dream": Date,
    "date_end": Date,
    "visible": Boolean,
    "realocate": Boolean,
    "expired": Boolean,
    "visualizable_mod": String,
    "goal":[{
            "name": String,
            "description": String,
            "date_begin": Date,
            "date_dream": Date,
            "date_end": Date,
            "realocate": Boolean,
            "expired": Boolean,
            "goal_tags": [],
            "activities":[{
                activity_id: String
            }]
            "goal_historic":[{
                date_realocate:Date
            }],
        }],
    "project_tags": [],
    "project_members": [{
            "type":String,
            "user":String,
            "notify":Boolean
    }]   
}

```
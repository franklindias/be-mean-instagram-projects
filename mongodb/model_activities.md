### Alternativa para modelagem da coleção activities

```
{
    name: String,
    description: String,
    date_begin: Date,
    date_dream: Date,
    date_end: Date,
    realocate: Boolean,
    expired: Boolean,
    comments :[{
        text: String,
        date: Date,
        comment_files:[{
                path: String,
                wight: Decimal,
                name_file: String
        }],
        comment_members: [{
                user: String,
                notify: Boolean
        }]
    }],
    tags:[],
    members:[{
        user: String,
        notify: Boolean
    }],
    historic:[{
        date_realocate: Date
    }]
}

```
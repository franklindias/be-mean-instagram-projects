### Alternativa para modelagem da coleção users

```js
{  
	name:String,  
	bio:String,  
	email:String,  
	date_register:Date,  
	avatar_path:String,
    auth: {  
		username:String,  
		password:String,  
		last_access:String,  
		online:Boolean,  
		disable:Boolean,  
		hash_token:String  
	}
}

```
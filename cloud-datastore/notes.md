
## Concept
- Entity
- Kind
- Property
- Ancestor
- Descendant 
- Indexes

## Replicate
- Increate read rate performance
## Sharing
- Increate write rate performance


## Development
- Need to create `app engine` for using `data store`
- Load `DataStore` module library with `GCP project id`
- Using datastore to create `key` with `kind name`
- Create `entity`
- Save object to Data store

## Best practice

With numberic key
- Avoid sequential numbering of keys.
- Let Cloud Datastore automatically assign the numeric ID for the key.
- When creating keys manually, get a block of IDs using the allocateIds() method.

Cloud Datastore supports atomic transactions.
The following error code from a Cloud Datastore request: INTERNAL -> 
Requests that return an INTERNAL error should not be retried more than once.

With Enities
- Entity keys can have manually generated numeric ids.
- Entities of the same kind can have different properties.

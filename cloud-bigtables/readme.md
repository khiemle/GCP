## Use cases of Big Table

- User information: quick access to information about connection between users
- User-generated content: app show users a large amount of user-generated content
- Time series data: retrieve most recent N records, storing data for serveral kind of events, filter base type of events 

- Avoid table scan


## Choosing row key

- keep row key short
- long key will take memory and storage, increase response time 
- only way to query Cloud Bigtable efficiently is by row key

### Reverse domain names
- Example : `com.company.product`
- each row's data tends to overlap with `adjacent` rows --> Cloud bigtable can compress your data more efficiently
- work best: data is spread across many different reserve domain names 
- in case small number of reserve domain: --> consider to use another row keys
--> to avoid overload a tablet by pushing most writes to single node of cluster

### String identifiers
- identify with simple string like User IDs --> row key or part of row keys
- dont recommend using a hash with row key --> 
- use `human-readble` values instead of hashing key, `multiple values`, separate those value by `#`


### Timestamps
- need to retrieve data by the time recorded
- Part of row key, `not the row key`, `not start of the row key` (if not most writes would be pushed to single node)

## Multiple values in a single row key
- Case: users post the message and mention another user -> row key can be: list of tagged username userA#userB
### `Row key prefixes`
- Well-plan row key prefix --> take advantage of Cloud BigTable's sorting order

### Row keys avoid
- Domain names: `company.com` will be in separate row ranges like `services.company.com`, `product.company.com` and so on
- Sequential numeric IDs
- Frequently updated identifiers: Avoid using a single row key to identify a value that must be updated very frequently
For the values that change very frequently : keep update from application, and update to big table periodically
- Hashed value: not recommend, need to use by multi readable value



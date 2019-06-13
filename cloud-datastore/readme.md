
## Concept
- Entity & Kind
    * Ancestor path: can't be change after entity's created, pernament
    * Root entity is the entity without parent entity
    * when create new entity, you're able to designate the parent 
    * Datastore make sure that it never assign same numberic ID for 
    entities
    * Ancestors & Descendants 
        - The complete key identifying the entity: sequence of `kind-indetifier pairs`
        ```
        [User:alice, TaskList:default, Task:sampleTask]
        ```
        ```
        KeyFactory keyFactory = datastore.newKeyFactory()
            .addAncestors(PathElement.of("User", "Alice"), PathElement.of("TaskList", "default"))
            .setKind("Task");
        Key taskKey = keyFactory.newKey("sampleTask");
        ```
    * Entity groups
        - Group of root entity and its descendants
        - `System-allocated ID` guaranteed unique 
- Property
    - one or more
    - each property: name and one or more value( `array property` )
        ```
        Entity task = Entity.newBuilder(taskKey)
        .set("tags", "fun", "programming")
        .set("collaborators", "alice", "bob")
        .build();
        ```
    - same kind, same property, but the value types can be difference
    - can be indexed or unindexed

- Indexes
- Identifies:
    * can't be change after created
    * create by
        * auto assign when the entity is created
            ```
            KeyFactory keyFactory = datastore.newKeyFactory().setKind("Task");

            Key taskKey = datastore.allocateId(keyFactory.newKey());
            ```
            `allocateIds` will generate the value which generate by Datastore mode

        * application create the own custom key name
        ```
        Key taskKey = datastore.newKeyFactory().setKind("Task").newKey("sampleTask");
        ```

## Development

Always remember create `KeyFactory -> Key` first, and call datastore with that key

Learn how to 

- Create entity instance
```
Key taskKey = datastore.newKeyFactory()
    .setKind("Task")
    .newKey("sampleTask");
Entity task = Entity.newBuilder(taskKey)
    .set("category", "Personal")
    .set("done", false)
    .set("priority", 4)
    .set("description", "Learn Cloud Datastore")
    .build();
```
- `upsert` overwrite if exists or `insert` (require doesn't exists)
```
Entity task = Entity.newBuilder(keyFactory.newKey("sampleTask")).build();
datastore.put(task);
```
- `insert`
```
Key taskKey = datastore.add(FullEntity.newBuilder(keyFactory.newKey()).build()).getKey();
```
- `get`
```
Entity task = datastore.get(taskKey);
```
- `update`
```
Entity task = Entity.newBuilder(datastore.get(taskKey)).set("priority", 5).build();
datastore.update(task);
```
- `delete`
```
datastore.delete(taskKey);
```

Batch operations
- mutil-entities
- should use this replace for inviduals entities
```
FullEntity<IncompleteKey> task1 = FullEntity.newBuilder(keyFactory.newKey())
    .set("category", "Personal")
    .set("done", false)
    .set("priority", 4)
    .set("description", "Learn Cloud Datastore")
    .build();
FullEntity<IncompleteKey> task2 = Entity.newBuilder(keyFactory.newKey())
    .set("category", "Personal")
    .set("done", false)
    .set("priority", 5)
    .set("description", "Integrate Cloud Datastore")
    .build();
List<Entity> tasks = datastore.add(task1, task2);
Key taskKey1 = tasks.get(0).getKey();
Key taskKey2 = tasks.get(1).getKey();
```
- `lookup`
```
Iterator<Entity> tasks = datastore.get(taskKey1, taskKey2);
```
- `delete`
```
Iterator<Entity> tasks = datastore.get(taskKey1, taskKey2);
```

## Queries
- kind
- filters (zero or more)
    * key filters
    ```
        Query<Entity> query = Query.newEntityQueryBuilder()
        .setKind("Task")
        .setFilter(PropertyFilter.gt("__key__", keyFactory.newKey("someTask")))
        .build();
    ```
    * properties filters
    ```
        Query<Entity> query =
        Query.newEntityQueryBuilder().setKind("Task").setFilter(PropertyFilter.eq("done", false))
        .build();
    ```
    * composite filters
    ```
        Query<Entity> query = Query.newEntityQueryBuilder()
            .setKind("Task")
            .setFilter(CompositeFilter.and(
                PropertyFilter.eq("done", false), PropertyFilter.ge("priority", 4)))
            .setOrderBy(OrderBy.desc("priority"))
            .build();
    ```
- sort orders (zero or more)
- special queries
    * ancestors queries
    ```
        Query<Entity> query = Query.newEntityQueryBuilder()
        .setKind("Task")
        .setFilter(PropertyFilter.hasAncestor(
            datastore.newKeyFactory().setKind("TaskList").newKey("default")))
        .build();
    ```
    * kindless queries
        - can't include filters or sort orders on properties
        - can filter on entity key, and ancestor query
    * projection queries
        - specified properties
        - require specified properties to be indexed
        - key-only queries: low latency
- Java
```
QueryResults<Entity> tasks = datastore.run(query);
```



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

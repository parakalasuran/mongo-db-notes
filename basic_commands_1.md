Reference: https://www.mongodb.com/docs/manual/tutorial/



# To list all the dbs available

    $ show dbs


# To use a db [mongodb will create a new one if not exists]

    $ use <db_name>


# To list all the collections with a db

    $ db.getCollectionNames()



# To find all the documents within a collections

    $ db.<collection_name>.find()


# To find one document within a collections. This returns document not cursor like find(). 

    $ db.<collection_name>.findOne()



# To insert one document into the collection
    
    $ db.<collection_name>.insertOne(<json>)

    # ex : 
    
    $ db.<collection_name>.insertOne({id:"1", name: "<name>"})



# To drop collection 

    $ db.myCollection.drop()



# To drop database

    $ db.runCommand({"dropDatabase": 1})

or 

    $ db.dropDatabase()



# To get stats of the collection / avg obj size / no of objects etc...
 
    $ db.stats()




# Create Collection 

    $ db.createCollection(
        "posts", 
        { 
            validator: { 
                $jsonSchema: { 
                    bsonType: 'object', 
                    required: ['title', 'text', 'creator', 'comments'],
                    properties: {
                        title: {
                            bsonType: 'string',
                            description: 'Must be a string'
                        },
                        text: {
                            bsonType: 'string'
                        },
                        creator: {
                            bsonType: 'objectId'
                        },
                        comments: {
                            bsonType: 'array',
                            required: ['text', 'author'],
                            properties: {
                                text:{
                                    bsonType: 'string'
                                },
                                author:{
                                    bsonType: 'objectId'
                                }
                            }
                        }
                    }
                }
            } 
        }
    )


# Inserting record following the schema - 

    $ db.posts.insertOne(
            { 
                title:'First Post', text: 'My First Post', 
                creator: ObjectId("658b0addc1d95e7fc5dd5f2a"), 
                comments:[ { text:'Wonderful', author: ObjectId("658b0addc1d95e7fc5dd5f2b") } ] 
            } 
        )


# Modify the collection to throw 'warning' and continue. 

    $ db.runCommand({
        collMod: "posts", 
        validator: { 
            $jsonSchema: { 
                bsonType: 'object', 
                required: ['title', 'text', 'creator', 'comments'],
                properties: {
                    title: {
                        bsonType: 'string',
                        description: 'Must be a string'
                    },
                    text: {
                        bsonType: 'string'
                    },
                    creator: {
                        bsonType: 'objectId'
                    },
                    comments: {
                        bsonType: 'array',
                        required: ['text', 'author'],
                        properties: {
                            text:{
                                bsonType: 'string'
                            },
                            author:{
                                bsonType: 'objectId'
                            }
                        }
                    }
                }
            }
        },
        validationAction: 'warn' 
    })



# Relationships

## One-to-One

One to one relationship can be setup using a reference or embedded based on the use case. 


Reference : 

    $ db.person.insertOne({name:'Olive', age:56, salary:4000})

    $ db.cars.insertOne({model:'BMW', price:40000, owner:ObjectId("6588503b0a2c194c51ae8883")})

        Here the ObjectId represents the person. 



Embedded:

    $ db.patient.insertOne({_id:1, name:'Susan', age:45, diseaseSummary:{diseases:['cold','headache']}})

# Relationships

## One -to- One

One to one relationship can be setup using a reference or embedded based on the use case. 


Reference : 

    $ db.person.insertOne({name:'Olive', age:56, salary:4000})

    $ db.cars.insertOne({model:'BMW', price:40000, owner:ObjectId("6588503b0a2c194c51ae8883")})

        Here the ObjectId represents the person. 



Embedded:

    $ db.patient.insertOne({_id:1, name:'Susan', age:45, diseaseSummary:{diseases:['cold','headache']}})



## One -to- Many 

Reference: 

    $ db.qa_db.insertOne({creator:"Debra", question:"What stout means?", answers:['q1a1','q1a2']})

    $ db.ans_db.insertOne({_id:'q1a1', text:'bulky / heavy built'}, {_id:'q1a2',text:'dark sweet brew'})


Embedded:

    $ db.qa_threads.insertOne({
        creator: 'Debra',
        question: 'Meaning of stout',
        answers: [
            {text:'bulky / heavy weight'},
            {text:'sweet dark brew'} 
        ]
    })


## Many -to- Many


    Customer Collection

    $ db.customers.insertOne({name:'Tory', age:25})
    $ db.customers.insertOne({name:'King', age:35})

    Product Collection 

    $ db.products.insertOne({title:'Nintendo', style:'hand held', price:129.99 })
    $ db.products.insertOne({title:'kindle', style:'light', price: 99.99})


    # Bridge collection

    $ db.orders.insertMany({orderNum:1, name:'Tory', product:'kindle'},{orderNum:1, name:'Tory', product:'Nintendo'})


    or

    use references to the objects using reference to customer & product _id in Bridge collection



## Join two collections 

    $ db.patients.aggregate([
        { 
            $lookup: {
                from:'patientSummary',
                localField:'diseaseSummary',
                foreignField:'_id',
                as: 'Summary'
            }
        }
    ])



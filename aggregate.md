## Join Two collections

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




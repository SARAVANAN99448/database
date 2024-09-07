
test> use library
switched to db library
<!-- creating books -->
library> db.books.insertMany([{title:"To kill a mocking bird",author:"Harper Lee",published_year:1960},{title:"the great gatsby",author:"F.scott fitzgerald",published_year:1925},{title:"The catcher in the rye",author:"J.D.salinger",published_year:1951},{title:"The lord of the rings",author:"J.R.R.tolkien"},{title:"Demon slayer",author:"koyoharu",published_year:2016},{title:"jujutsu kaisen",author:"Gege akutami",published_year:2018}])
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('66daf6a0b9175bac152710bc'),
    '1': ObjectId('66daf6a0b9175bac152710bd'),
    '2': ObjectId('66daf6a0b9175bac152710be'),
    '3': ObjectId('66daf6a0b9175bac152710bf'),
    '4': ObjectId('66daf6a0b9175bac152710c0'),
    '5': ObjectId('66daf6a0b9175bac152710c1')
  }
}
<!-- Retrieve  -->
library> db.books.find()
[
  {
    _id: ObjectId('66daf6a0b9175bac152710bc'),
    title: 'To kill a mocking bird',
    author: 'Harper Lee',
    published_year: 1960
  },
  {
    _id: ObjectId('66daf6a0b9175bac152710bd'),
    title: 'the great gatsby',
    author: 'F.scott fitzgerald',
    published_year: 1925
  },
  {
    _id: ObjectId('66daf6a0b9175bac152710be'),
    title: 'The catcher in the rye',
    author: 'J.D.salinger',
    published_year: 1951
  },
  {
    _id: ObjectId('66daf6a0b9175bac152710bf'),
    title: 'The lord of the rings',
    author: 'J.R.R.tolkien'
  },
  {
    _id: ObjectId('66daf6a0b9175bac152710c0'),
    title: 'Demon slayer',
    author: 'koyoharu',
    published_year: 2016
  },
  {
    _id: ObjectId('66daf6a0b9175bac152710c1'),
    title: 'jujutsu kaisen',
    author: 'Gege akutami',
    published_year: 2018
  }
]
<!-- Finding the specific author -->
library> db.books.find({author:"Harper Lee"})
[
  {
    _id: ObjectId('66daf6a0b9175bac152710bc'),
    title: 'To kill a mocking bird',
    author: 'Harper Lee',
    published_year: 1960
  }
]
<!-- Finding the specific year -->
library> db.books.find({published_year:2016})
[
  {
    _id: ObjectId('66daf6a0b9175bac152710c0'),
    title: 'Demon slayer',
    author: 'koyoharu',
    published_year: 2016
  }
]
<!-- earliest published year. -->

library> db.books.find().sort({published_year:1}).limit(1)
[
  {
    _id: ObjectId('66daf6a0b9175bac152710bd'),
    title: 'the great gatsby',
    author: 'F.scott fitzgerald',
    published_year: 1925
  }
]

library> db.books.find().sort({published_year:1}).limit(2)
[
  {
    _id: ObjectId('66daf6a0b9175bac152710bd'),
    title: 'the great gatsby',
    author: 'F.scott fitzgerald',
    published_year: 1925
  },
  {
    _id: ObjectId('66daf6a0b9175bac152710be'),
    title: 'The catcher in the rye',
    author: 'J.D.salinger',
    published_year: 1951
  }
]
<!-- updating the published_year -->
library> db.books.updateOne({title:"the catcher in the rye"},{$set:{published_year:1999}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 0,
  modifiedCount: 0,
  upsertedCount: 0
}
<!-- Adding genre to all the books -->
library> db.books.updateMany({},{$set:{genre:"mystery"}},{multi:true})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 6,
  modifiedCount: 6,
  upsertedCount: 0
}
library> db.books.find()
[
  {
    _id: ObjectId('66daf6a0b9175bac152710bc'),
    title: 'To kill a mocking bird',
    author: 'Harper Lee',
    published_year: 1960,
    genre: 'mystery'
  },
  {
    _id: ObjectId('66daf6a0b9175bac152710bd'),
    title: 'the great gatsby',
    author: 'F.scott fitzgerald',
    published_year: 1925,
    genre: 'mystery'
  },
  {
    _id: ObjectId('66daf6a0b9175bac152710be'),
    title: 'The catcher in the rye',
    author: 'J.D.salinger',
    published_year: 1951,
    genre: 'mystery'
  },
  {
    _id: ObjectId('66daf6a0b9175bac152710bf'),
    title: 'The lord of the rings',
    author: 'J.R.R.tolkien',
    published_year: 1985,
    genre: 'mystery'
  },
  {
    _id: ObjectId('66daf6a0b9175bac152710c0'),
    title: 'Demon slayer',
    author: 'koyoharu',
    published_year: 2016,
    genre: 'mystery'
  },
  {
    _id: ObjectId('66daf6a0b9175bac152710c1'),
    title: 'jujutsu kaisen',
    author: 'Gege akutami',
    published_year: 2018,
    genre: 'mystery'
  }
]
<!-- deleting specific book -->
library> db.books.deleteOne({title:"The lord of the rings"})
{ acknowledged: true, deletedCount: 1 }
library> db.books.find()
[
  {
    _id: ObjectId('66daf6a0b9175bac152710bc'),
    title: 'To kill a mocking bird',
    author: 'Harper Lee',
    published_year: 1960,
    genre: 'mystery'
  },
  {
    _id: ObjectId('66daf6a0b9175bac152710bd'),
    title: 'the great gatsby',
    author: 'F.scott fitzgerald',
    published_year: 1925,
    genre: 'mystery'
  },
  {
    _id: ObjectId('66daf6a0b9175bac152710be'),
    title: 'The catcher in the rye',
    author: 'J.D.salinger',
    published_year: 1951,
    genre: 'mystery'
  },
  {
    _id: ObjectId('66daf6a0b9175bac152710c0'),
    title: 'Demon slayer',
    author: 'koyoharu',
    published_year: 2016,
    genre: 'mystery'
  },
  {
    _id: ObjectId('66daf6a0b9175bac152710c1'),
    title: 'jujutsu kaisen',
    author: 'Gege akutami',
    published_year: 2018,
    genre: 'mystery'
  }
]
<!-- deleting books before 2000  -->
library> db.books.deleteMany({published_year:{$lt:2000}})
{ acknowledged: true, deletedCount: 3 }
library> db.books.find()
[
  {
    _id: ObjectId('66daf6a0b9175bac152710c0'),
    title: 'Demon slayer',
    author: 'koyoharu',
    published_year: 2016,
    genre: 'mystery'
  },
  {
    _id: ObjectId('66daf6a0b9175bac152710c1'),
    title: 'jujutsu kaisen',
    author: 'Gege akutami',
    published_year: 2018,
    genre: 'mystery'
  }
]
<!-- recently published books limit(1) -->
library> db.books.find().sort({published_year:-1}).limit(1)
[
  {
    _id: ObjectId('66daf6a0b9175bac152710c1'),
    title: 'jujutsu kaisen',
    author: 'Gege akutami',
    published_year: 2018,
    genre: 'mystery'
  }
]
<!-- recently published books limit(2) -->
library> db.books.find().sort({published_year:-1}).limit(2)
[
  {
    _id: ObjectId('66daf6a0b9175bac152710c1'),
    title: 'jujutsu kaisen',
    author: 'Gege akutami',
    published_year: 2018,
    genre: 'mystery'
  },
  {
    _id: ObjectId('66daf6a0b9175bac152710c0'),
    title: 'Demon slayer',
    author: 'koyoharu',
    published_year: 2016,
    genre: 'mystery'
  }
]
<!-- title contains the word  -->
library> db.books.find({title:{$regex: /(Demon)/i}})
[
  {
    _id: ObjectId('66daf6a0b9175bac152710c0'),
    title: 'Demon slayer',
    author: 'koyoharu',
    published_year: 2016,
    genre: 'mystery'
  }
]


library> db.books.find({title:{$regex: /(kaisen)/i}})
[
  {
    _id: ObjectId('66daf6a0b9175bac152710c1'),
    title: 'jujutsu kaisen',
    author: 'Gege akutami',
    published_year: 2018,
    genre: 'mystery'
  }
]

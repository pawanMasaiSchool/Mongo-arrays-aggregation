Problem

create a collection of posts
it should have title, comments, author details, tags
comments should be an array of objects with, body, author of the comment etc., comment id
tags should be array of strings


push a new tag into a post
=>  db.posts.updateOne({title:"Pawan"},{$push:{tags:"React"}})

push multiple tags into a post
=> db.posts.updateOne({title:"Albert"},{$push:{tags:{ $each: [ "MongoDB","SQL","JavaScript","React"]  }}})

pull and remove a particular tag
=> db.posts.updateOne({title:"Albert"},{ $pull: {tags:"JS"} })

pull and remove an array of values use $in
=> db.posts.updateOne({title:"Abhishek"},{ $pull: {tags:{$in: ['Coding','Masai', 'JS'] } } })

use $pop to remove first and last tag

// To remove last element from array we use 1
=> db.posts.updateOne({title:"Pawan"},{ $pop:{ tags:1  }  })
// To remove first element from array we use -1
=> db.posts.updateOne({title:"Pawan"},{ $pop:{ tags:-1  }  })

use addToSet to add.5 tags
=> db.posts.updateOne({title:"Pawan"},{ $addToSet:  { tags: { $each:  [ "Masai", "JS", "HTML", "CSS", "Mongo"] } } })


Part II
create a collection of users with high scores
each user can have 3 high scores
it should be always in descending order

add 5 new high scores, and maintain the order, and keep the limit of 3 scores
=> db.users.updateOne({username:"Pawan"}, { $push: { high_scores: { $each: [ 100,110,50,60,64 ],$sort:-1, $slice:3   }  }  })

remove multiple scores which are greater than x value
=> db.users.updateMany({}, { $pull: { high_scores: { $gte:90  }  } })
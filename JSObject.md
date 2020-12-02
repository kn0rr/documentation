# Objects

Objects are collections of properties. A property is a key-value pair.
Instead of accessing data using an index, we use custom keys.
all keys are converted to strings (except for symbols).

````js
const animals={
    name: 'Rex',
    type: 'dog',
    age: 12
}

//access property:
animals.type//dog

//access property where key is a number:
const number={1:2}
number[1] //2 
animals.['name'] //'Rex'

//Use variable to look for value in object

const n=1
const prop ='name'
number[n] //2
animals[prop] // 'Rex'
animals.prop //undefined it is not working vor variables you have to use []

//Add and change values
const userReviews= {};

userReviews['user1']=3.0 //userReviews{user1:3.0}
userReviews.user2=2.5 //userReviews{user1:3.0, user2:2.5}
userReviews.user1=2.0 //userReviews{user1:2.0, user2:2.5}
userReviews.user1+=2.0 //userReviews{user1:4.0, user2:2.5}
userReviews.user2++ //userReviews{user1:4.0, user2:3.5}

//More Complex Object

const student= {
    firstName:'John',
    lastName:'Doe',
    strengths:['Math', 'Sports'],
    exams: {
        midterm: 50,
        final: 12
    }
}
//avg of scores
const avg =(student.exams.midterm+student.exams.final)/2 // 31
student.strengths[1] //'Sports'

// Multiple Objects in an Array

const shoppingCart=[
    {
        product: 'pencil',
        price: 0.5,
        quantity: 30
    },
    {
        product: 'rubber',
        price: 0.25,
        quantity: 50
    },
    {
        product: 'basket',
        price: 12.0,
        quantity: 10
    }
]

//Comparing arrays
let nums=[1,2,3] //nums->12546
let nums2=[1,2,3] // nums->456789

nums===nums2 //false because nums stores reference in 123456 and nums 2 in 456789
nums==nums2 //false because nums stores reference in 123456 and nums 2 in 456789

let moreNums=nums

moreNums===nums //true
moreNums===nums2 //false

//How to check values than
const user={
    name:'John'
    email:'john.doe@gmail.com'
    notifications:[]
}
//not working
if (user.notifications===[]){   
    console.log("no new Notifications")
}
// working
if (user.notifications.length===0){   
    console.log("no new Notifications")
}
// working
if (!user.notifications.length){   
    console.log("no new Notifications")
}



````
>Object is also a reference type like array (stores data in a reference) -> therefore use in most cases const
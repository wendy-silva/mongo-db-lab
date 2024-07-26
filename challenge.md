# MongoDB CLI

## Getting Started

The prompts below each ask for you to write the query in MongoDB for performing
some action (described in the prompt). Your response should be a valid query and
it should be property formatted in Markdown. For example:

**Prompt:** Find all burgers in the `burgers` collection.

```
db.burgers.find({})
```

### Instructions

* Start your `mongo` server
* Connect to the `mongo` shell

### Prompts

**Prompt:** What is the command to start the `mongo` server?
* brew services start mongodb-community

**Prompt:** What is the command to connect to the `mongo` shell?
* mongosh

**Prompt:** What is the command for listing all `mongo` databases?
* show dbs

**Prompt:** What command would you use to create a database called `burgers`?
* use burgers

**Prompt:** What command would you use to add the collection `burger` to your
`burgers` database?
*db.burgers.insertOne({burger})

**Prompt:** What is the command for listing all collections in a database?
* show collections

## Inserting

### Prompts

**Prompt:** Insert a single burger into the `burgers` collection with the
following:

* a `patty` property set to `beef`
* a `cheese` property set to `false`
* a `toppings` set to an array with `ketchup`, `onions`, and `pickles`

**Answer:** *db.burgers.insertOne({name: 'burger', patty:' beef', cheese: false, toppings:['ketchup','onions','pickles']})*

**Prompt:** Insert 10 burgers into the `burgers` collection with the following:

* a `patty` property that is set to one of: `beef`, `turkey`, or `veggie`
* a `cheese` property that is either `true` or `false`
* a `toppings` property that is either one of `ketchup`, `onions`, `pickles`,
  `mustard`, and `mayonnaise`

**Answer:** *db.burgers.insertMany([
 {patty: "beef", cheese: true, toppings: ["ketchup", "onions", "pickles"]},
 { patty: "turkey", cheese: false, toppings: ["mustard", "mayonnaise"]},
 { patty: "veggie", cheese: true, toppings: ["ketchup", "mustard"]},
 {patty: "beef", cheese: false, toppings: ["onions", "pickles"]},
 { patty: "turkey", cheese: true, toppings: ["mayonnaise", "ketchup"]},
   { patty: "veggie", cheese: false, toppings: ["mustard", "onions"]},
   { patty: "beef", cheese: true, toppings: ["ketchup", "pickles"]},
   { patty: "turkey", cheese: false, toppings: ["mayonnaise", "mustard"]},
  { patty: "veggie", cheese: true, toppings: ["ketchup", "onions", "pickles"]},  
  { patty: "beef", cheese: false, toppings: ["mustard", "onions"]}
]);*

## Reading

The following prompts will have you querying (reading) from your `burger`
collection. If you don't have burgers in your database that match the query
criteria described below, you wont get any results back. So, add one or two that
match that criteria before running the query.

### Prompts

**Prompt:** What query would find all burgers with a `beef` patty?

**Answer:** *db.burgers.find({patty: 'beef'})*

**Prompt:** What query would find all burgers with cheese on them?

**Answer:** *db.burgers.find({cheese: true})*

**Prompt:** What query would find a burger by it's ObjectId?

**Answer:** *db.burgers.find({ _id: ObjectId(ID Here)})*

**Prompt:** What query would find all burgers with `ketchup` as a topping?

**Answer:** *db.burgers.find({ toppings: "ketchup" })*

**Prompt:** What query would find all burgers with either a turkey or veggie
patty?

**Answer:** *db.burgers.find({ patty: { $in: ["turkey", "veggie"] } }*

**Prompt:** What query would find all burgers with a beef patty and cheese?

**Answer:** *db.burgers.find({ patty: "beef", cheese: true })*

**Prompt:** What query would find all burgers with a beef patty and ketchup as
a topping?

**Answer:** *db.burgers.find({ patty: "beef", toppings: "ketchup" })*

**Prompt:** What query would find all burgers with a beef patty and both onions
and pickles as toppings?

**Answer:** *db.burgers.find({patty: "beef", toppings: { $all: ["onions", "pickles"]} })*

**Prompt:** What query would find burgers with either a turkey patty or cheese?

**Answer:** *db.burgers.find({ $or: [{ patty: "turkey" }, { cheese: true }] })*

## Update

### Prompts

**Prompt:** What query would update one burger by it's ObjectId, setting it's
"patty" to "pork"?

**Answer:** *db.burgers.updateOne( { _id: ObjectId("yourObjectIdHere") }, { $set: { patty: "pork" } })*

**Prompt:** What query would update all burgers with beef paddies to have
cheese? (i.e. set "cheese" to true)

**Answer:** *db.burgers.updateMany( { patty: "beef" }, { $set: { cheese: true } })*

## Delete

### Prompts

**Prompt:** What query would delete a burger by it's ObjectId?

**Answer:** *db.burgers.deleteOne({ _id: ObjectId("ObjectIdHere") })*

**Prompt:** What query would delete all veggie burgers?

**Answer:** *db.burgers.deleteMany({ patty: "veggie" })*

**Prompt:** What query would delete all burgers with pickles on them?

**Answer:** *db.burgers.deleteMany({ toppings: "pickles" })*
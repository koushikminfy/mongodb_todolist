# mongodb_todolist


### Step 1: Connect to MongoDB

Start by connecting to your MongoDB cluster using the following command:

mongosh "mongodb+srv://cluster0.loewrvf.mongodb.net/" --apiVersion 1 --username koushik0416

### Step 2: Create the Database

Switch to your desired database. In this case, we are using `todo_db`:

use todo_db

### Step 3: Insert a Single Task

To insert one task into the collection, use:


db.tasks.insertOne({
  description: "Buy Shoes",
  status: "pending",
  created_at: new Date()
})


### Step 4: Insert Multiple Tasks

To insert ten tasks in one go, run:

db.tasks.insertMany([
  { description: "Buy groceries", status: "pending", created_at: new Date() },
  { description: "Complete homework", status: "pending", created_at: new Date() },
  { description: "Call mom", status: "pending", created_at: new Date() },
  { description: "Finish reading book", status: "pending", created_at: new Date() },
  { description: "Reply to emails", status: "pending", created_at: new Date() },
  { description: "Clean the room", status: "pending", created_at: new Date() },
  { description: "Water the plants", status: "pending", created_at: new Date() },
  { description: "Exercise for 30 minutes", status: "pending", created_at: new Date() },
  { description: "Plan the weekend trip", status: "pending", created_at: new Date() },
  { description: "Review project notes", status: "pending", created_at: new Date() }
])


### Step 5: View All Tasks

To see all the tasks in your collection:


db.tasks.find()


### Step 6: Convert Status Field to Boolean

Update the `status` field from "pending" to `false` for all documents:


db.tasks.updateMany(
  { status: "pending" },
  { $set: { status: false } }
)


### Step 7: Add a Task with Default Boolean Status

Insert a new task with `status` set to `false` by default:


db.tasks.insertOne({
  description: "New task from user",
  status: false,
  created_at: new Date()
})


### Step 8: Mark a Task as Completed

To mark a specific task as completed, change its `status` to `true`. For example:

db.tasks.updateOne(
  { _id: ObjectId('6836e3f9c7996ce8cc6c4bd2') },
  { $set: { status: true } }
)


### Step 9: Verify the Update

To confirm the update, find the task by its ID:


db.tasks.find({ _id: ObjectId('6836e3f9c7996ce8cc6c4bd2') })


### Step 10: Update Any Task and Add a Timestamp

To update a task and also add an `updated_at` timestamp, use:

db.tasks.updateOne(
  { _id: ObjectId('6836e3f9c7996ce8cc6c4bd3') },
  { $set: {
      description: "Buy groceries and fruits",
      status: false,
      updated_at: new Date()
    }
  }
)


### Step 11: Count All Tasks

To get the total number of tasks:

db.tasks.countDocuments()

### Step 12: Count Completed Tasks Only

To count how many tasks are marked as completed (`status: true`):

db.tasks.countDocuments({ status: true })

# Capstone

## User Stories
 ***MVP***
1) User sees Mission Statement "Provide a platform where users can upload and share their latest programming work AND talent seekers can view projects of up and coming developers."

2) HOME 
    - User sees a link for to log-in or register. 
    - User sees website mission statement 
    - Users can either create an account to upload their work, create an account to recruite OR browse existing content
        
3) Create Account
    - User will be able to create an account with the following information
    - Username / Password
    - firstName / lastName
    - email address
    - Personal Website URL
    - Location
    - Personal Summary or Description & Experience
    - After account is created, redirect to new account page
        
4) Personal Account page 
    - User sees session message acknowledging account creation
    - User can click on a link for user to EDIT their existing account information
    - If user ia a Developer user they will see a button that allowsc the user to create projects from their index
    - Developer users will be able to click on their existing projects to view the project show page
    - If user is a Recruiter they can have a list of Prospects that they have added
    
5) Account Edit Page
    - Users will have access to an account editing page where they can edit/update their existing account info
    - Once user submits edits, they get redirected to User Show Page
    
6) Create Project Showcase
    - Developer user will be able to enter information outlined in project model
        - Project Name
        - Project Description
        - Project Link
        - Github (or other repo)
        - Pictures!!!

7) Users Index
    - Users and non-users will have the ability to view existing Dev users in the Users index page
    - They will see a list of all existing users in the database, which can be accessed to provide that users projects and information
    
8) User Show Page / Project Index
    - User sees information listed in step 3  displayed
    - User will see a list of the user's projects and links displayed
    - User will be able to select a specific project, which will redirect you to the project show page
    - User will also see a button to start a conversation with that user(Conversation create button)
    - Recruiter user will be able to add Developer users to their prospects
    
9) Convo Show Page
    - User can see the picture of the user they are in a conversation with
    - User can also see any previous messages in that conversation
    - User can create a new message

10) Project Show page
    - The user will see information from the project model as well as a link to visit the deployed project
        - Project Name
        - Project Description
        - Project Link
        - Github (or other repo)
        - Pictures!!!
    - Note: Links will direct users to an external site where project is hosted
    - Site visitors will have access to go back to the user page / project index
    - User will have an option for editing their own existing projects
    
11) Project Edit Page
    - User will be able to edit/update or delete their project information
    - After Project edits are complete, redirect to project show page
    
## Routes
***Developer***

Post "/dev/" creates a new dev

Get "/dev/" gets a list of the devs

Get "/dev/:id" gets a specific dev and their projects based on id

Delete "/dev/:id" deletes a specific dev based on id

Put "/dev/:id" updates the dev's info based on the id

***Project***

Post "/project/" creates a new project

Get "/project/:id" gets the detail,on a specific

Delete "/project/:id" deletes a specific based on id

Put "/project/:id" updates the info of a project based on id

***Recruiter*** 

Post "/recruiter/" creates a new recruiter

Get "/recruiter/:id" gets a specific recruiter and their prospects based on id

Delete "/recruiter/:id" deletes a specific recruiter based on id

Put "/recruiter/:id" updates the recruite's info based on the id

***Conversation***

Post "/conversation/" creates a conversation between a recruiter and a developer

Get "/conversation/" gets a list conversations between the user and other users

Get "/conversation/:id" gets a specific conversation between the user and another user

***Message***

Post "/message/"





## Models

```
const developerSchema = new mongoose.Schema({
	userName: { type: String, required: true, unique: true },
	password: { type: String, required: true }, 
	firstName: { type: String, required: true }, 
	lastName: { type: String, required: true }, 
	email: { type: String, required: true },
	location: String,
	imageURL: String, 
	experience: String,
	projects: [{
		type: mongoose.Schema.Types.ObjectId, 
		ref: 'Project'
	}]
})

const recruiterSchema = new mongoose.Schema({
	userName: { type: String, required: true, unique: true },
	password: { type: String, required: true }, 
	firstName: { type: String, required: true }, 
	lastName: { type: String, required: true }, 
	email: { type: String, required: true },
	location: String,
	imageURL: String, 
	description: String,
	developer: [{
		type: mongoose.Schema.Types.ObjectId,
		ref: 'Developer'
	}]
})f


const projectSchema = new mongoose.Schema({
	name: { type: String, required: true },
	description: String,
	projectURL: { type: String, required: true },
	repo: String,
	projectImage: String
})
 
const conversationSchema = new mongoose.Schema({
	developer: {
		type: mongoose.Schema.Types.ObjectId, 
		ref: 'Developer'
	},
  	recruiter: {
		type: mongoose.Schema.Types.ObjectId, 
		ref: 'Recruiter'
	},
	messages: [{
		type: mongoose.Schema.Types.ObjectId, 
		ref: 'Message'
	}]
	
})

const messageSchema = new mongoose.Schema({
  	time: { type: Date, default: Date.now },
		text: { type: String, required: true },
  	fromRec:[{
		type: mongoose.Schema.Types.ObjectId, 
		ref: 'Recruiter'
	}],
 	fromDev: [{
		type: mongoose.Schema.Types.ObjectId, 
		ref: 'Developer'
	}]

})
```


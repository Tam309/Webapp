# Fix Food API

## Overview

The application is built on a Node.js and Express framework, leveraging MongoDB for data persistence through Mongoose ORM. It is developed with TypeScript to ensure type safety and better code structuring. The backend architecture supports API versioning, enabling seamless future updates and modifications without impacting existing functionality.

## Features

-TBD

## Getting started

### Requirements

- Node.js
- MongoDB
- npm or yarn

# **Meal Planner API Documentation**

# **Overview**
This project is a meal planning API that generates and ranks meal recipes for a user group based on their allergies, dislikes, and preferences. The API fetches recipes from a database, filters them based on group member restrictions, and returns ranked meal plans.

---

## **Feautures**

1. **Generate Ranked Recipes**: Retrieves recipes for a user group, ranking them based on members' allergies and dislikes.
2. **14-Day Meal Plan**: Provides breakfast, lunch, and dinner recipes for 14 days.
3. **Add/Remove Users from User Group**: Allows adding and removing users from a group.

---

## **Installation**
- Node.js
- MongoDB

## **Steps**
1. Install dependencies
```bash
npm install
```
2. Start MongoDB and set up your enviroment
```bash
MONGO_URI=<your-mongodb-connection-string>
```
3. Run the application  
```bash
npm run start
```

---

# **API Endpoints**

## **Get all recipes**
- Endpoint ``GET /recipes``
- Description: Retrieves all recipes from the database.    
- Response Example
```json
[
    {
        "_id": "670e59f2cbbb841bfb5da373",
        "name": "Recipe 1",
        "ingredients": [
            "beef",
            "potatoes",
            "carrots",
            "onion"
        ],
        "cuisine": "Italian",
        "mealType": "Lunch",
        "prepTime": 54,
        "cookTime": 11,
        "totalTime": 179,
        "instructions": "Prepare the ingredients and follow standard cooking methods.",
        "seasonal": "Winter",
        "dietaryRestrictions": [
            "vegan"
        ],
        "likes": 49,
        "lastCooked": null
    },
    ...
]
``` 

## **Get user group profile based on group id**
- Endpoint ``GET /usergroup/:groupId``
- Description: Retrieves user group profile based on the user group id from the database
- Response Example
```json
{
    "_id": "6710ee74e5ec10de8706bf00",
    "groupId": "1",
    "members": [
        {
            "_id": "67110195858733c7abe0a500",
            "userId": "1",
            "name": "Pascal",
            "age": 43,
            "allergies": [],
            "preferences": [
                "Light lunches",
                "Tasty and wholesome dinners"
            ],
            "dislikes": [
                "Dill"
            ]
        },
        {
            "_id": "67110195858733c7abe0a501",
            "userId": "2",
            "name": "Ellie",
            "age": 36,
            "allergies": [
                "Lactose-intolerant"
            ],
            "preferences": [
                "Pesco-vegetarian",
                "Flexible"
            ],
            "dislikes": [
                "Liver",
                "Chicken"
            ]
        },
        {
            "_id": "67110195858733c7abe0a502",
            "userId": "3",
            "name": "Elliot",
            "age": 13,
            "allergies": [],
            "preferences": [
                "Would only eat grilled cheese if given a chance"
            ],
            "dislikes": [
                "Olives",
                "Pickles"
            ]
        },
        {
            "_id": "67110195858733c7abe0a503",
            "userId": "4",
            "name": "Rose",
            "age": 10,
            "allergies": [],
            "preferences": [
                "Anxious FOMO",
                "Wants to like everything"
            ],
            "dislikes": [
                "Strong cheeses"
            ]
        }
    ],
}
```

## **Add new user group**
- Endpoint ``POST /usergroup`` 
- Description: Creates a new user group with the provided information
- Request Body:
```json
{
  "groupId": "2",
  "members": [
    {
    "userId": "1",
      "name": "Angle",
      "age": 43,
      "allergies": [],
      "preferences": ["Light lunches", "Tasty and wholesome dinners"],
      "dislikes": ["Chives"]
    },
    {
    "userId": "2",
      "name": "Johnson",
      "age": 36,
      "allergies": ["Lactose"],
      "preferences": ["Pesco-vegetarian", "Flexible"],
      "dislikes": ["Beef", "Heart", "Fat"]
    },
    {
        "userId": "3",
        "name": "Elisa",
        "age": 20,
        "allergies": ["Glucoes"],
        "preferences": ["Dinner"],
        "dislikes": ["Milk"]
    }
  ]
}
```

## **Adjust user group**
- Endpoint ``PUT /usergroup/:groupId``  
- Description: Add or remove 1 user from a specific user group
- Request Body for remove user:
```json
{
  "action": "remove",
  "userId": "5"
}
```
- Request Body for add user:
```json
{
  "userId": "5",
  "name": "Thomas",
  "age": 19,
  "allergies": [],
  "preferences": "breakfast",
  "dislikes": []
}
```

## **Get 5 recipes ranked from best to worst**
- Endpoint ``GET /usergroup/:groupId/recipe``
- Description: Retrieves 5 recipes for a user group, ranked based on members' allergies and dislikes
- Response Example
```json
[
    {
        "_id": "670e59f2cbbb841bfb5da373",
        "name": "Recipe 1",
        "ingredients": [
            "beef",
            "potatoes",
            "carrots",
            "onion"
        ],
        "cuisine": "Italian",
        "mealType": "Lunch",
        "prepTime": 54,
        "cookTime": 11,
        "totalTime": 179,
        "instructions": "Prepare the ingredients and follow standard cooking methods.",
        "seasonal": "Winter",
        "dietaryRestrictions": [
            "vegan"
        ],
        "likes": 49,
        "lastCooked": null
    },
    {
        "_id": "670e59f2cbbb841bfb5da374",
        "name": "Recipe 2",
        "ingredients": [
            "beef",
            "potatoes",
            "carrots",
            "onion"
        ],
        "cuisine": "Japanese",
        "mealType": "Breakfast",
        "prepTime": 6,
        "cookTime": 18,
        "totalTime": 70,
        "instructions": "Prepare the ingredients and follow standard cooking methods.",
        "seasonal": "Summer",
        "dietaryRestrictions": [
            "gluten-free"
        ],
        "likes": 32,
        "lastCooked": null
    },
    {
        "_id": "670e59f2cbbb841bfb5da378",
        "name": "Recipe 6",
        "ingredients": [
            "spaghetti",
            "olive oil",
            "garlic",
            "chili flakes",
            "parsley"
        ],
        "cuisine": "American",
        "mealType": "Dinner",
        "prepTime": 7,
        "cookTime": 74,
        "totalTime": 16,
        "instructions": "Prepare the ingredients and follow standard cooking methods.",
        "seasonal": "Summer",
        "dietaryRestrictions": [
            "vegan"
        ],
        "likes": 67,
        "lastCooked": null
    },
    {
        "_id": "670e59f2cbbb841bfb5da379",
        "name": "Recipe 7",
        "ingredients": [
            "tofu",
            "bell peppers",
            "soy sauce",
            "ginger"
        ],
        "cuisine": "American",
        "mealType": "Dinner",
        "prepTime": 6,
        "cookTime": 112,
        "totalTime": 59,
        "instructions": "Prepare the ingredients and follow standard cooking methods.",
        "seasonal": "Spring",
        "dietaryRestrictions": [
            "gluten-free"
        ],
        "likes": 25,
        "lastCooked": null
    },
    {
        "_id": "670e59f2cbbb841bfb5da37b",
        "name": "Recipe 9",
        "ingredients": [
            "spaghetti",
            "olive oil",
            "garlic",
            "chili flakes",
            "parsley"
        ],
        "cuisine": "Italian",
        "mealType": "Lunch",
        "prepTime": 31,
        "cookTime": 98,
        "totalTime": 148,
        "instructions": "Prepare the ingredients and follow standard cooking methods.",
        "seasonal": "Spring",
        "dietaryRestrictions": [
            "none"
        ],
        "likes": 4,
        "lastCooked": null
    }
]
```

## **Get 14-day meal plan**  
- Endpoint ``GET /usergroup/:groupId/mealplan``
- Description: Retrieves a 14-day meal plan for a user group, based on members' dietary 
- Response Example
```json
[
    {
        "day": "Day 1",
        "breakfast": {
            "_id": "670e59f2cbbb841bfb5da5a7",
            "name": "Recipe 565",
            "ingredients": [
                "spaghetti",
                "olive oil",
                "garlic",
                "chili flakes",
                "parsley"
            ],
            "cuisine": "Italian",
            "mealType": "Breakfast",
            "prepTime": 23,
            "cookTime": 102,
            "totalTime": 79,
            "instructions": "Prepare the ingredients and follow standard cooking methods.",
            "seasonal": "Summer",
            "dietaryRestrictions": [
                "vegan"
            ],
            "likes": 63,
            "lastCooked": null
        },
        "lunch": {
            "_id": "670e59f2cbbb841bfb5da53d",
            "name": "Recipe 459",
            "ingredients": [
                "chicken",
                "rice",
                "soy sauce",
                "broccoli"
            ],
            "cuisine": "Japanese",
            "mealType": "Lunch",
            "prepTime": 19,
            "cookTime": 50,
            "totalTime": 127,
            "instructions": "Prepare the ingredients and follow standard cooking methods.",
            "seasonal": "Winter",
            "dietaryRestrictions": [
                "none"
            ],
            "likes": 96,
            "lastCooked": null
        },
        "dinner": {
            "_id": "670e59f2cbbb841bfb5da5fe",
            "name": "Recipe 652",
            "ingredients": [
                "chicken",
                "rice",
                "soy sauce",
                "broccoli"
            ],
            "cuisine": "Mexican",
            "mealType": "Dinner",
            "prepTime": 53,
            "cookTime": 14,
            "totalTime": 75,
            "instructions": "Prepare the ingredients and follow standard cooking methods.",
            "seasonal": "Spring",
            "dietaryRestrictions": [
                "none"
            ],
            "likes": 81,
            "lastCooked": null
        },
        ...
]
```

---

# **Project Structure**
```plaintext
|-- ff.api/
    |-- src/
        |-- models/
            |-- Recipe.ts
            |-- UserGroup.ts
        |-- routes/
            |-- routes.ts
        |-- app.ts
```
- **models/**: Contains Mongoose schemas for Recipe and UserGroup.
- **app.ts**: Initializes Express and connects to MongoDB.

---

# **License**
- No License

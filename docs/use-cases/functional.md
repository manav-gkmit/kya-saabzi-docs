# Functional Use Case

### Sign-Up

| Element            | Detail  |
|:-------------------|:--------|
| **Name**           | Sign Up
|  **ID**            | UC-01
| **Description**    | User can register themself from here
| **Actors**         | User, System
| **Pre-Conditions** | <ul><li>Sign Up Page with `Username` & `Password` fields</li></ul>
|  **Basic Flow**    | <ul><li> User selects `Username` field and enters preferred username</li><li> User selects `Password` field and enters password </li><li> User clicks on the `Register` button </li><li> System stores the `username` & `password` in the database </li></ul>
| **Post-Conditions**| User has been successfully registered

### Login

| Element            | Detail  |
|:-------------------|:--------|
| **Name**           | Login
|  **ID**            | UC-02
| **Description**    | User can login from here
| **Actors**         | User, System
| **Pre-Conditions** | <ul><li>Login Page with `Username` & `Password` fields</ul></li>
|  **Basic Flow**    | <ul><li> User selects `Username` field and enters registered username</li><li> User selects `Password` field and enters their password </li><li> User clicks on the `Login` button </li><li> System authenticates the user and logs them in </li></ul>
| **Post-Conditions**| User has logged in successfully

### Add dish

| Element            | Detail  |
|--------------------|---------|
| **Name**           | Add the dish
|  **ID**            | UC-03
| **Description**    | User can post what they have cooked today
| **Actors**         | User, Dish
| **Pre-Conditions** | <ul><li>Dish poster has been identified</li><li>Interface to post a dish is present</li></ul>
|  **Basic Flow**    | <ul><li> User enters the dish cooked today</li><li> User presses the `Submit` button </li><li> System stores the dish log in the database </li></ul>
| **Post-Conditions**| Dish cooked today is stored.

### Get recommendation

| Element            | Detail  |
|--------------------|---------|
| **Name**           | Dish Recommendation
|  **ID**            | UC-04
| **Description**    | User can get dish recommendation based on their history and other's preferences
| **Actors**         | User, Dish
| **Pre-Conditions** | <ul><li>User must have some past history in the database</li><li>Others must have cooked atleast one dish</li></ul>
|  **Basic Flow**    | <ul><li>User selects how many recommendations they want</li><li> User clicks on the `Get recommendation` button </li></ul>
| **Post-Conditions**| Recommendations were successfully provided

### Search dish by name

| Element            | Detail  |
|--------------------|---------|
| **Name**           | Dish's date last cooked
|  **ID**            | UC-05
| **Description**    | User can search when a dish was last cooked
| **Actors**         | User, Dish
| **Pre-Conditions** | <ul><li>Users must have cooked atleast one dish</li></ul>
|  **Basic Flow**    | <ul><li>User enters the name of the dish</li><li>User clicks on the `Search` button</li></ul>
| **Post-Conditions**| Date last cooked for the dish entered is provided

### Delete dish

| Element            | Detail  |
|--------------------|---------|
| **Name**           | Delete dish
|  **ID**            | UC-06
| **Description**    | User can delete the logs for a dish
| **Actors**         | User, Dish
| **Pre-Conditions** | <ul><li>Users must have cooked atleast one dish</li></ul>
|  **Basic Flow**    | <ul><li>User enters the name of the dish</li><li>User clicks on the `Delete` button</li></ul>
| **Post-Conditions**| Logs for the dish are deleted

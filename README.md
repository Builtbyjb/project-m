# Capstone

## Overview

My final project is a team project management application that allows users to create projects, add other users to the project, and within each project create tasks that can be assign to different members of the team. The application also allows team members to assign different stages to the tasks. These stages include Todo, In progress, and Completed.

I decided to build a team project management application because coordinating school online projects
was a difficult process. There was no way to know the current state of the project and track each each team
member progress. My final project is an implementation of how i would solve the problem.

## Distinctiveness and Complexity

The different filtering options, role based access system, ability to add and remove team members, ability to
assign tasks to different team members, ability to set different task stages, and the ability to discuss
each tasks through comments makes the project different from other projects in this course and complex to
build.

Users can create projects through a create project pop screen by providing a project name and a project
description. Projects can be filtered based on if the user is the creator of the project, the user is added to a project by another user, the project is marked as completed or the project is uncompleted. Users can also search for a project by providing a project name through the project search bar.

Each individual project page allows users to add tasks, add team members, add comments to each tasks, assign task to team membes, change the task stage, filter tasks based on who is assign to the tasks, the task stage or both. Users can only see projects they created or are added to.

The role based system grants different acess to different team member roles. The admin is the creator of the project. The role based system rules are as follows;

- The admin and the team leader can add or remove any team member.
- Team members can only remove themselves.
- Only the admin can edit project name and description.
- The admin and the team leader can mark a project as completed.
- Only the admin can delete a project.
- The admin and team leader can assign tasks.
- The admin and team leader can delete tasks.
- The admin cannot be removed from the project.
- Only the creator of a comment can delete or edit the comment.
- Only the admin can edit team member roles.
- Each project can only have one admin and team leader.

Only users with an account can be added to a project. Team members still assigned to tasks cannot be removed.
The projects uses pop ups to add team members,edit team member roles, add tasks, edit tasks,
edit project name, edit project description, and view comments.

The challenges I faced when building this project include accessing newly created elememts without reloading
the page, figuring out how to implement the project name search functionality, and implementing the role
based access system.

## File Documentation

### Static

- ** script.js **: Contains all the javascript responsible for the applications functionality. The file Contains functions such as:

  - sendGetRequests: This is an asynchronous function that takes in a url and an id as arguments. It sends
    a fetch request with a http method of "GET" to the server and returns a response.

  - sendPostRequests: This is an asynchronous function that takes in a url and a formData as arguments. It sends a fetch request with a http method of "POST" and a body containing the formData to the server and returns a response.

  - sendDeleteRequests: This is an asynchronous function that takes in a url and an id as arguments. It sends a fetch request with a http method of "Delete" to the server and returns a response.

  - sendPutRequests: This is an asynchronous function that takes in a url, an id, and a JSON object called data. It sends a fetch request with a http method of "PUT" and a body containing the JSON object. It returns a response.

  - textCounter: This function takes in a textId(The id of the textarea element) and a countId(The id of the span element that displays the count) as arguments. It updates the number of characters a user as typed in a text area. It displays the text count at the bottom right of every text area element used in the project.

  - deleteElement: This function takes in an element id as an arguement. It sets the animation play state of an element with the delete-item class to running and removes the element when the animation ends.

  - displayPopUp: This function takes in an element id as an argument. It displays an element by removing the "hide-pop-up" class from the element.

  - closePopUp: This function takes in an element id as an agrument. It hides an element by adding the hide-pop-up class to an element. It also clears any input the element may have.

  - updateCommentCount: This is an asynchronous function that takes a taskId and a commentCount. It sends a put request to the server with the new comment count, if the request is successfull it updates the web page
    with the new comment count.

  - generateComment: This function takes in a comment object, a username, and a taskId. It creates a new comment element.

  - generateTask: This function takes in a response which is task object. It creates a new task element

  - generateTeamMember: This function takes in a response which is team member object. It creates a new team member object.

  The file also contains eventListeners added to the document or html elements that handle click events and change event on the web page.

- ** style.css **: Contains all the style properties that improves user experience.

### Templates

- ** layout.html **: This is the base html file. It contains the head tag, the nav bar and, the script tag. The other html files extend this file.

- ** index.html **: This file dispays all the projects related to a user. It also contains the create project pop, the create project button, the projects filter dropdown, and the project search input field.

- ** login.html **: This file contains a form with two input elements the takes in a username and a password, and a third input element of type submit that sends the username and the password to the server.

- ** register.html **: This file contains a form with five input elements. The input elements takes in an email, a username, a password, a confirmation password and an input field of type submit that sends the input values to the server.

- ** project.html **: This file contains html elements that displays all the tasks related to the a project, it displays the project name and the project description, it displays all the team members related to the project. It also contain html elements that add team member, add tasks, edit project name and edit project description. The project files also displays a comment pop and all the comment related to each tasks.

### API

- ** views.py **: The file contains api endpoints such as:

  - register: This function is called when a post request is sent to the register endpoint, it recieves a username, an email, a password, and a comfirmaation password. It creates a user object, saves the user object and logins in the user using the login function imported from "django.contrib.auth".

  - login_view: This function is called when a post request is sent to the login endpoint, it recieves a username and a password. It authenticates the user using the authenticate function from "django.contrib.auth" and then logins in the user.

  - logout_view: This function is called when a "GET" request is sent to the logout endpoint. It logs out a user using the logout function from "django.contrib.auth".

  - index: This function is called when a "GET" request is sent to the "/" endpoint. It returns a list of projects related to the user that sent the request.

  - project: This function is called when a request is sent to the "/project" endpoint with an id, if no id is provided it redirects the user to the home page. The function performs different actions depending on the type of request sent to the endpoint.

    If the request method is "POST", the function creates a new project object saves it to the database, creates a new team object with the user as the admin, and returns the project object.

    If the request method is "DELETE", the function deletes the project with the request id from the database, it returns an error if a project with the request id does not exist and the project id if the project is successfully deleted.

    If the request method is "PUT", the function updates the name, description, or the "is_completed" field of the project with the request id depending on the request body.

    If the request method is "GET", the function gets the project with the request id, all the tasks and team members related to the project, the function also filters the tasks based on who the tasks are assigned to, the task stage or both depending on the query strings recieved from the url.

  - task: This function is called when a request is sent to the "/task" endpoint with an id, if no id is provided it redirects the user to the home page.

  If the request method is "POST", the function creates a new task object and saves the task object to the database. i

  If the request method is "DELETE", the function deletes the task with the request id from the database.

  If the request method is "PUT", the function updates the task object with the request id with the new task.

  If the request method is "GET", the function redirects the user to home page.

  - comment: This function is called when a request is sent to the "/comment" endpoint with an id.

  If the request method is "POST", the function creates a new comment object with the comment recieved from the request body.

  If the request method is "DELETE", the function deletes the comment object with the request id from the database.

  If the request method is "GET", the function gets all the comments related to the task id gotten from the request id.

  If the request method is "PUT", the function gets the comment object with the request id and update the comment object with the new comment.

  - stage: This function is called when a "PUT" request is sent to the "/stage" endpoint with an id. The function gets the task object with request id and then updates the task objects stage.

  - team: This function is called when a request is sent to the "/team" endpoint with an id.

  If the request method is "POST", the function checks if the username gotten from the request body is a registered user, it also checks if the user is already part of the team, if all the checks are passed the function then create a new team object, and if the role gotten from the request body is "Team leader", the function updates the project team leader to the new username gotten from the request body.

  If the request method is "PUT", the function updates the team member role.

  If the request method is "DELETE", the function deletes the team object with the request id, if the role is team leader the function sets the project team leader value to unassigned.

  - assign: This function is called when a "PUT" request is sent to the "/assign" endpoint with an id. It updates the assigned to value of the task object with the request id.

  - comment_count: This function is called when a "POST" request is sent to the "/comment_count" endpoint. The function updates the comment_count value of the task object with the id gotten from the request body.

- ** urls.py **: defines all the urls and their assigned handliers in views.py

- ** models.py **: defines all the sqlite models and their fields. This models include:

  - user: This class uses django default user table fields.

  - project: This class includes fields relating to a project. This fields include name, description, is_completed, creator, creator_id, and team_leader.

  - task: This class includes fields relating to a project. This fields include the project class, task, assigned_to, stage, and comment_count.

  - comment: This class includes fields relating to a comment. This fields include the task class, comment, and creator.

  - team: This class includes fields relating to a team. This fields include the project class, member, and role.

## Running The Application

The project can be ran with the following commands:

- "pip install -r requirements.txt" to install the project dependenciences.
- "Python manage.py runserver"

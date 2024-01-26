---
title:  'Coding project with my husband: testing GPT Pilot for UI creation'
---

Back in [November](https://www.ieva.dev/2023/11/03/coding_project_with_husband_pt1.html) I shared a bit about a coding project that we have started with my husband Vytautas. The progress on it is very slow. The fact that people are asking about it helps to keep on going. 

We already have the basic API, so it is Frontend time. Since none of us have any experience with it we decided to see if AI can help us and test the [GPT pilot](https://github.com/Pythagora-io/gpt-pilot).

![Reactions](/assets/images/gpt_pilot_test.drawio.svg){: width="880" }

**Prerequisites.** To be able to use the tool you need an OpenAI subscription as the project is using their API and to have some money in the balance. But don’t be afraid - we played quite a bit with it and it didn’t cost us 10 euros.

**Generating the prompt.** The first and key part of the tool is to describe clearly what you need the AI to generate. We spent probably close to an hour on this. We drew a workflow and noted which endpoint should be used where. The final result looked something like this:


![Workflow](/assets/images/bbd_workflow.drawio.svg){: width="800" }


**The prompt** that we came up with looking at the drawing:

```
The app is a UI (frontend) web application for participating in a book reading challenge. The backend REST API already exists.

Opening an app you get to the login page. The user can login using a username and a password (POST /users/login). After successful login you are redirected to a homepage that has a navigation bar at the bottom (consisting of: "My challenges", "All challenges", "Profile"). Clicking on "All challenges" redirects to the screen consisting of a list of challenges available (GET /club/challenges). Each item in the list displays the name attribute of the challenge from the GET response, "Join" and "Leave" buttons depending if the user has already joined the challenge (GET /club/challenges/users retrieves all challenges that the user participates in). After clicking on a particular challenge, the user is redirected to the challenge's screen which displays the information (cover, author, title) about the books that are associated with this challenge (challenge_books ids) (GET /club/challenges/{id}/books) and "Join" and "Leave" buttons depending if the user has already joined the challenge. When the user joins the challenge, she is redirected to "My challenges" screen that contains challenges returned from GET /club//challenges/users. The main interaction that a user can do after joining a challenge is commenting on a book. To do that they need to click on a challenge displayed in "My challenges", then after bein redirected to the challenge screen, they need to click on a book. This action will redirect to a book screen with the title, author and cover of the book (GET /club/challenge_books/{id}) and the list of user's comments done on the challenge_book (GET /club/challenge_books/{id}/comments). The user can add a new comment by clicking on a button which opens a form with the textbox as the comment's content (POST /club/challenge_books/{id}/comments).
```


A few things that became obvious while doing this:


* **Documentation is very important.** It was more than a month between when we finished working on the API and when we sat down to test the GPT pilot. We had the list of endpoints in our Jira tasks and in the notebook, but no broader documentation on what we had envisioned. We found ourselves confused about the purposes of several endpoints. 
* **Workflow first.** Since we are both backend engineers we started designing this from the API. Once we put the workflow on paper some endpoints started to feel a bit out of place.

**Feeding the prompt to the GPT pilot**. 

**Attempt 1.** The same evening when we generated the prompt, we fed it to the GPT pilot. It asked us a couple of follow up questions (e.g. what should be the style of the web page, is error handling needed etc.) and started to code away. It printed out the descriptions of tasks and implemented them. There were a few errors that it managed to fix itself with some help and by the end of the evening we had functioning login and home pages that actually communicated with the backend app. We went to bed feeling hopeful and looking forward to the next session.

The high level plan of what it wanted to do looked something like this:

* Set up the React.js project with Redux and all necessary dependencies, Router and establish the base project structure with basic navigation (My challenges, All challenges, Profile).
* Implement the 'Login' functionality with JWT for authentication.
* Render a list of all challenges available using the GET /club/challenges API call.
* Implement the 'Join' and 'Leave' challenge functionality.
* Implement the challenge screen that shows book information when a challenge is clicked
* Implement the 'Add Comment' feature for a book in a challenge

**Attempt 2.** The next session was not as smooth as expected. To relaunch the app we seem to have needed an app_id, which we didn’t write down anywhere and struggled to find. Eventually we decided to just start a new project. We already had the prompt anyway. Unfortunately this time we never got to a working login page. We hit some bug and it kept crashing on the same step. 

By the way, when rerunning the project we noticed it actually prints this at the very beginning:
```
------------------ STARTING NEW PROJECT ----------------------
If you wish to continue with this project in future run:
python main.py app_id=1eb5598d-3dd5-4cef-ad8e-3c23caef9db5
```

**Subsequent attempts.** We spent a bit more time on this trying to figure out how to get past the bugs. The thing that worked best was to implement some of the instructions by ourselves, then rewind it a few dev steps back and hope for the best. The last time we tried to get it working we reached a point where we fed stuff generated with GPT pilot back to ChatGPT to verify it. That was the breaking point for us as it felt too absurd.

**Final impressions.** Vytautas said it made him feel like a robot as the AI was making all the creative decisions and we ended up trying to implement and debug them as it crashed so often. For me it was kind of fun at first, interesting what will happen next, how to get through to the next step - much like a text based game.

**What’s next?** We will have to do it the old way. Vytautas is more excited about becoming a full stack developer, so he is learning some javascript basics and looking for good resources to learn React. Recommendations are welcome.
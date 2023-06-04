---
parent: Topics
layout: default
title: "Pull Requests"
description:  "aka PRs; a checklist for doing them properly"
---

# {{page.title}}

# A Checklist

1. PR Title:
   - Is it escriptive enough that someone familiar with the project can understand it at first glance?
   - Is it short enough to be readable at a glance? (For example, don't try to put the entire "As an X I can Y so that Z" story into the title field.)
2. Linked to an Issue?
   - You can link to an issue with certain magic words such as `Closes #15`, `Fixes #27`
   - But if you don't phrase it just right, the link doesn't happen.
   - In that case, use the manual feature for linking to an issue (see below)
3. Linked Issue is in the "In Review" column on team's Kanban board.
4. PR is tagged with the Team's tag, like this one:
   ![image](https://user-images.githubusercontent.com/1119017/202531598-e935a3eb-98dd-4816-8b0c-434e512e9207.png)
5. Test cases all pass.
   - If you have difficulty with this one, ask for help from a team member first.
   - Then ask for help on the Slack help channel associated with the project, e.g. `#proj-ucsb-courses-search`, `#proj-ucsb-cs-las`, `#proj-mapache-search` on the slack.
   - Then ask for help during staff office hours or during lecture/discussion work time.
6. You have requested (and gotten) a code review from a fellow team members.
7. You have requested (and gotten) a code review from a member of staff (i.e. an LA, TA, or the instructor)
   - Please consult the page with team assignments (e.g. for W21 that's here: ) to see which LA and TA are assigned to your team. 
   - Request those members of staff first; however anyone on staff can review your PR.
8. Address all concerns brought up in the code review. This doesn't mean that you have to do exactly as the code reviewer says, but it does mean
   that you can't just ignore what they suggest.  Acceptable ways of resolving a code review concern include:
   - Doing what the code reviewer asks
   - Presenting a good case why you are not going to do that (e.g. "that's a good point, but let's do that in a different issue", or "I see the situation differently; here's my point of view; let's discuss.")
9. Address any merge conflicts that exist between your feature branch and the then current `main` branch.  You may need to "rebase" your branch on main.
   - Merge conflicts with `package-lock.json` are a special case covered here: <https://ucsb-cs156.github.io/topics/spring_react_package_lock_json_merge_conflicts/>
   - If you have other merge conflicts that you don't know how to resolve, ask for help.
1. Is it still a "draft PR"?  If so, you need to convert it to a regular PR before it can be merged.
   
# Keeping PRs small and focused

It's good to avoid PRs that have changes to many files in them; fewer than 10 files is ideal.    Especially true if the files span both front and backend.

Sometimes though, it's unavoidable.  In that case, a guide to the changes, as shown in this PR description, can be really helpful to your code reviewers:
* <https://github.com/ucsb-cs156/proj-courses/pull/9>


# Linking a PR to an issue

 You can link to an issue automatically with certain magic words such as `Closes #15`, `Fixes #27`.
 
 But if that doesn't work, here's how to do it manually:
 
![link-PR](https://user-images.githubusercontent.com/1119017/202532386-2108c4b7-3d01-4594-9a50-665d07556c35.gif)
 
 
# Doing a Code Review
 
Many companies use "branch protection" rules in GitHub for their `main` branch (or `master` branch, if using the older convention).

Rules may include the number of code reviews that must be done.  In our case, we are requiring two code reviews, one from the team, and one from a member of staff.

For these code reviews to "count", i.e. to make the PR mergeable, the code review needs to be done *with the right set of mouse clicks* in GitHub. (It isn't enough, for example, to just put a "comment" `LGTM` ("Looks Good To Me"); that comment has to be done *as an approving code review*. 

Here's what that looks like. 

![LGTM-Code-Review](https://user-images.githubusercontent.com/1119017/202532159-d2ea281f-873f-45fc-8c44-b338f3e4f244.gif)


# What to look for in a Code Review?

Students often ask what they should look for in a code review.  

In general, you are looking for any opportunities to make the code better, and/or to find things the developer may have missed. It should be approached in a spirit of "helpful suggestions".

1. It can be helpful to test the code on your team's Heroku deployment at the same time you are reviewing the code.
2. It's good to look for any "commented out code" that the developer may have left in the code while they were debugging, and suggest that it be removed.
3. It's helpful to look for opportunities to make the code "DRYer", i.e. to follow the rule "Don't Repeat Yourself".   Is there copy/pasted code that could be factored out into a common function or method?
4. It's helpful to look for opportunities to improve naming.  Are the variables names, class names, and method names chosen meaningful and helpful to others reading the code?

These are just a few examples to give the idea of the kinds of things you can be looking for.

# Did I mention: Keep them small?

I want to strongly encourage everyone on all teams to submit smaller PRs.

This is an important real world skill, and it's also really, really, helpful to success in this course.
What I would prefer to see:

* A separate PR for the @Entity and @Repository class for a new database table, with nothing else in the PR  (5 pts)
* A separate PR for the frontend fixtures that match a new Entity from the backend, or an anticipated api endpoint. (5 pts)
* A separate PR for a form and/or table component along with the storybook entry and tests for it.  (10 pts)
* A separate PR for the GET/POST endpoints for a new database table entry for CRUD operations. (10 pts)
* A separate PR for DELETE endpoint for a new database table entry. (10 pts)
* A separate PR for UPDATE endpoint for a new database table entry (10 pts)
* A separate PR for any additional backend endpoints; one PR per one or two new endpoints. (10 pts)
* A separate PR for a new frontend Page that brings together preexisting components and calls to a backend api that now exists (and was merged in an earlier PR), including the App.js and AppNavbar modifications  (10 pts)

That's a total of 70 points, and these PRs sail through the review process like sports cars.  They are dead simple to review, and test.

What I'm getting instead, often, is one PR that tries to do 5 or 6 things from the list above, or even ALL of them.  That maxes out at 20 points, leaving points on the table.  It's also much, much, much, harder to code review and test.

It requires dedicated concentration by one of the staff members for perhaps up to an hour.   We try to spread out time among multiple teams, and we also have other tasks.  This will be true of your real world software engineering colleagues too.   It's much easier to get five colleagues to each do a 10 minute code review than to get one colleague to do a 50 minute code review.

Plus: if there are rounds of "revise and resubmit" for your PRs after code reviews find issues, these go much faster on smaller PRs.
Please, please, please take this to heart!

# PR Descriptions

In many organizations, PR descriptions are read by both programmers and non-programmers.

What are the non-programmers doing reading PR descriptions?  They may be going through them to:
* put together updates about what has changed in the app in the past week, month or quarter that are provided to tech support, sales, and customers
* determine what extra testing may need to be done before cutting a new branch from main to  deploy  to prod (i.e. to live customers)
* find "what changed recently" if there is suddenly a big change in performance, new bugs, etc.

So it is important that your PR descriptions include, first, a *brief description of the impact on the end user*, in terms that an end user (or a non-programmer that's very, very familiar with the app from an end user perspective) would understand.

It's ok if you then go on to provide some technical details.   But lead with the *non-technical description*.

# Screenshots, Storybook, Swagger, etc.

When doing a frontend PR, you should include, where applicable (and it almost always is):
* Active before and after links to the published storybook.  
  - Before typically comes from the storybook for the main branch that is published on the Github pages site
  - After typically comes from the storybook link for the PR
* Screenshots of before and after; these may seem redundant with the storybook links, but they are not for these reasons:
  - The storybooks will change over time; after your PR is merged, the "before" becomes the "after", and the "after" link for the PR will eventually be purged.
  - The screenshots, though, become a permanent record of what was changed.
  - Plus: the screenshots give your code reviewers an idea of what's in your frontend PR at a glance: "a picture is worth a 1000 words".
 
When doing a backend PR that involves changes to backend API endpoints, especially when you are adding or changing the API, you should include, where applicable:
* Screen shots of the swagger api endpoints affected (before and after if applicable, or just after if it's new)
* Advice on a suggested sequence of actions to test the backend endpoints (e.g. sample values to use).

# PR Titles

These are not acceptable PR titles:
* Add CRUD operations
* Add GET/POST to backend
* Fix PUT route

These are better PR titles:
* Add backend for CRUD operations for RideRequests
* Add GET/POST for CowLots
* Fix PUT route for personal schedule

Do you see the difference? With these titles you can look and at a glance, you know what the PR is referring to.

Why does this matter? You might argue that looking at the files changed, you'd instantly know which models are being changed. So it might seem "picky" and unimportant.

Here's why it's important:
* Team members needs to be able to look over the list of PRs in the queue, or the list of PRs recently merged, and get the "big picture" of what's happening with the team at a glance.  That information is conveyed in the issue title and/or PR title.
* Later on when we are trying to figure out which code to take from which of the teams to put into the legacy code base that future students will work on, we look through all of the PRs.  Vague titles make this process much, much, harder.
* Sometimes we use older PRs as examples for future students.  We want all of the PRs we merge to serve as good examples, and to be easy to locate by topic.

So, please pay attention to the title of your PRs.

---
title: My toy project 1 - My Dear KukuClara
layout: single
categories:
- Toy Project
tags:
- toy project
- react
- javascript
last_modified_at: '2021-03-25 14:00:00 +08000'
---
> A small talk about my toy project, My Dear KukuClara

![Screenshot](/assets/images/screenshot-mdk-v1.JPG)
[Link to the website](https://my-dear-kukuclara.netlify.app/)

I have a kind of minor hobby, which is collecting vintage-style PVC dolls (the communities and users were active around 2016-7 but getting smaller now😥). For me, it was pretty difficult to find information about the collection unless I dig it up in the community forums by myself. So I thought it would be nice to have a sort of wikipedia.

## Project Requirements
First of all, in the first version, I decided to make simple features to search, filter, and sort a list of the collections.

## Project Spec
* Duration: 3 ~ 4 weeks (I learned React with this project, so bit slow)
* Main language/framework : React, Redux, Semantic UI
* Datasource: Google Spreadsheet API (but all the data typed by myself😂)
* EDR (Simple😭)
![ERD](/assets/images/erd-mdk-v1.JPG)

### Chitchat about the spec

#### Datasource
`Google Spreadsheet`: It needs to be able to be managed by non-developers, I mean like common KukuClara fans. So I decided to use Google Spreadsheet that I was working on to collect data. Google Spreadsheet is like Excel that people are familar with, and it provides APIs, so I thought it would be available right away without any DB setup for my app. Furthermore, I am planning to open the Data Source link at the bottom of the website soon, so everyone can review the data.

#### Main Language / Framework
`React` & `Redux`: I tried to learn and use React this time because React is *hot* nowadays, even though I used `Vue` in my previous company. Moreover, I love the bigger and active community of React and its syntax which just looks like a normal JavaScript module (it does not have the syntax of `Vue` such as `v-bind` or `v-for`! except `className`... I mean `Vue` syntax makes me write codes in their standard way, but sometimes i feel like i am stuck in their syntax with less freedom). I also used Redux, as a central store, to make state management between components less complicated.

#### Business Logic
I was thinking about how to make the business logic for sorting and filtering. Should I just make API calls with a query provided by Spreadsheet, or just developing them by JavaScript myself...? I thought I better call the API once to load the whole data and put it in a cash memory (because the length of the list is not that big), and handle filtering or sorting with JavaScript on a client-side. Therefore, I am using the API only once to get the list. The business logic for search/filtering/sorting for basic listing features is currently handled by [reducers](https://github.com/nh0627/kukuclara-collection/blob/main/src/store/reducers/dollsReducer.js) with my functions🤔... (I want to improve it with less complexity).

#### UI Framework
`Semantic UI`: I can make UI with CSS somehow but I am aware that I am not that good at making good UI design. Regardless of design, the library also offers lots of good features to make my app in a handy way!

## Things to update
* First of all, I think there will be a better algorithm to handle the business logic related to the listing. I need to study more to have a better understanding of data structure and algorithms.
* I should seriously start learning TDD and use it with codes in this project.
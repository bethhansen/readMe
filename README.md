# Project

#### Brief Description

#### By Beth Hansen

## Description

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.

## Specifications

Input Behavior | Input | Output |
---------------|-------|--------|
creates a new word | "hello" | "hello" |
creates a definition for selected word | "a greeting" | "Hello, Definition: A greeting" |

### Routing

| Behavior                                                          | Path                     | HTTP Verb | App.java Example                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Process                                                                                                                                                                            |
|-------------------------------------------------------------------|--------------------------|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Home Page                                                         | /                        | GET       | get("/", (request, response) -> Map<String, Object> model = new HashMap<String, Object>(); model.put("words", Word.all()); model.put("template", "templates/index.vtl"); return new ModelAndView(model, layout);}, new VelocityTemplateEngine());                                                                                                                                                                                                                | User requests page. Server sends HTTP GET request. Spark matches request to "/" route.                                                                                             |
| Display word form                                                 | /word-form               | GET       | get("/word-form", (request, response) -> {Map<String, Object> model = new HashMap<String, Object>(); model.put("template", "templates/word-form.vtl"); return new ModelAndView(model, layout);}, new VelocityTemplateEngine());                                                                                                                                                                                                                                  | User requests form to create new word. Server returns page with word form. *Form action and method must match path/verb of route below.*                                           |
| Display definitions for selected word                             | /word/:id/definition     | GET       | get("/word/:id/definition", (request, response) -> {Map<String, Object> model = new HashMap<String, Object>(); Word word = Word.find(Integer.parseInt(request.params(":id"))); model.put("word", word); model.put("template", "templates/word-definitions.vtl"); return new ModelAndView(model, layout);}, new VelocityTemplateEngine());                                                                                                                        | User requests page. Server collects selected word, renders template. Velocity loops through definitions and displays them.                                                         |
| Display definition form                                           | /word/:id/definition/new | GET       | get("/word/:id/definition/new", (request, response) -> {Map<String, Object> model = new HashMap<String, Object>(); Word word = Word.find(Integer.parseInt(request.params(":id"))); model.put("word", word); model.put("template", "templates/definition-form.vtl"); return new ModelAndView(model, layout);}, new VelocityTemplateEngine());                                                                                                                     | User requests form to create new definition for selected word. Server returns page with definition form. *Form action and method must match path/verb of route below.*             |
| Creates new word with definition when word form is submitted      | /                        | POST      | post("/", (request, response) -> {Map<String, Object> model = new HashMap<String, Object>(); Definition newDefinition = new Definition(request.queryParams("description")); Word newWord = new Word(request.queryParams("name")); newWord.addDefinition(newDefinition); model.put("words", Word.all()); model.put("template", "templates/index.vtl"); return new ModelAndView(model, layout);}, new VelocityTemplateEngine());                                   | User submits word form. Server grabs attributes from form. Uses them to create new word. Server renders the home page with all words listed.                                       |
| Creates new definition for word when definition form is submitted | /word/:id/definition/new | POST      | post("/word/:id/definition/new", (request, response) -> {Map<String, Object> model = new HashMap<String, Object>(); Word word = Word.find(Integer.parseInt(request.params(":id"))); Definition newDefinition = new Definition(request.queryParams("description")); word.addDefinition(newDefinition); model.put("word", word); model.put("template", "templates/word-definitions.vtl"); return new ModelAndView(model, layout);}, new VelocityTemplateEngine()); | User submits description form. Server grabs attributes from form. Uses them to create new description for selected word. Server renders page with all definitions of selected word.|

## Setup

* Clone this repository

* blah blah blah

## Technologies Used

* Java

* Gradle

* JUnit

* Spark

*

<p align="center">
  <img src="img/java.jpg="350"/>
  <img src="img/java.jpg" width="350"/>
</p>


## Support

If you run into any problems, contact me at beth97209@gmail.com

### Legal

Copyright (c) 2017 Beth Hansen.

Licensed under the MIT license

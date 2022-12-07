# Giphy Party Exemplar Project

Exemplar code for giphy party using Fetch API
In this lab, we will be using the Giphy API to explore making HTTP requests and dynamically adding HTML to a page.

Find the core instructions for this lab on the [CodePath course portal](https://courses.codepath.org/courses/summer_internship_for_tech_excellence/unit/3#!lab)

---

# Topic Lab: Giphy Party

## Overview

In this lab, we will be using the [Giphy API](https://developers.giphy.com/) to explore making HTTP requests and dynamically adding HTML to a page.

<iframe class="embeddedObject shadow resizable" name="embedded_content" scrolling="no" frameborder="0" type="text/html"
        style="overflow:hidden;" src="https://www.screencast.com/users/SamanthaHe/folders/Capture/media/72eca9df-a1b5-4f2a-a3a9-964db892a79e/embed" width="560" height="315" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

^^^[+]
<span style="font-size:1.6em; font-weight: 600">Project Details</span>
^^^

### Goals

By the end of this lab, you will be able to...

- [ ] use APIs to make HTTP requests and parse through responses using the Fetch API.
- [ ] identify and implement asynchronous programming with `async`/`await` functions and commands.
- [ ] create a branch using `git` commands and explain the purpose and importance of version control.
- [ ] understand how pull requests track changes and implement best practices for code reviews on GitHub.

### Student Skills

- Create semantic HTML forms
  - Understand and use semantic HTML `input` elements
  - Attach an event handler to the semantic HTML form element's `submit` event
  - Prevent the default native submission event
- Use the native `fetch` function to send HTTP requests to an API endpoint
  - Leverage `async/await` syntax to execute an asynchronous function
  - Construct a valid Giphy API URL using the form input's `value`
  - Issue a `GET` request to that URL and handle the response
- Process JSON returned from an API endpoint and convert it to HTML elements
  - Write a function that ingests the Giphy API response. It should:
    - Clear the area where results are displayed
    - Iterate over the data returned from the endpoint and create an HTML element for each one
    - Write a function that iterates over the data returned from the Giphy API endpoint and creates an HTML element for each one.
- Keep track of state and make paginated requests to the Giphy API

### Application Features

#### Core Features

- [ ] Allow the user to search for a GIF and when the form is submitted, display a limited number of results.
- [ ] Allow the user to make multiple search requests with different phrases. New results will replace old existing gifs.
- [ ] Allow the user to load more GIFs from the search
- [ ] At least one accessible feature (i.e color-sensitive choices, alt-text for images, etc)

#### Stretch Features

- [ ] Explore additional properties of the Gif Object
- [ ] Incorporate various buttons that use a different API endpoint.
- [ ] Improve CSS styles with Bootstrap framework
- [ ] Incorporate `:hover` styling and DOM events

### Resources

- [HTML input element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input)
- [Asynchronous JavaScript](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous)
- [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
- [Giphy API Docs](https://developers.giphy.com/docs/api#quick-start-guide)
- [Understanding GitHub flow](https://guides.github.com/introduction/flow/)
- [Branching in GitHub](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/about-branches)

^^^

---

^^^
<span style="font-size:1.6em; font-weight: 600"> Step 0: Set up your project (5-10 mins) </span>
^^^

- [ ] **Create a new repository in GitHub**. We suggest giving your repository a descriptive name that corresponds to your project (i.e `yourName_personal_website`).
- [ ] **Clone your repository to your local environment.**
- [ ] **On VS Code, select the `open folder` and navigate to open your cloned repository folder on your computer.**
- [ ] **Set up your project file structure.** Create 3 empty files like the structure below.

```javascript
    |- giphy-party/
  		|- index.html
  		|- style.css
  		|- app.js
```

^^^

^^^
<span style="font-size:1.6em; font-weight: 600"> Step 1: Plan your website layout (5 mins) </span>
^^^
In this lab we will focus mainly on the JS requirements but you will have the freedom to customize your websites with your own styling. We will not explicitly walk you through any CSS styling in this lab. We highly recommend you checkout Lab 1 for CSS tips and tricks.

Let’s take a moment to think about our required user stories and the actions we would like them to be able to take! Our users should have a section where they can:

- Type in a keyword in a search bar and submit once they are done.
- Based on the keyword, users should see a set number of gif results relating to their search word
- Users should be able to click a button to load more results.

Before we begin figuring out how to get the necessary information from the GIPHY API, let’s take a moment to create a quick wireframe and build out a skeleton structure in our HTML file. Remember, wireframes do not have to be detailed. It is up to you what you decide to include or not include, but in general it is best to indicate `div` sections, types of elements included, and any indications where `id`s are needed.

---

#### 📢 Now it’s your turn!

- [ ] **Create a basic wireframe for your website.** In general, your wireframe should include a title location, search area with a search bar and submit button, area to load gif results, and a button to load more results.
- [ ] **Add the boilerplate HTML and link your CSS and JS files.**
  - Remember in VSCode you can use the shortcut `html:5` to load HTML boilerplate. First, set the language of your file to HTML, then begin typing `html:5`. Next, you will notice `html:5` pop up in a dropdown column, navigate to the option and click **Enter** or **Tab** . This will automatically load the HTML boilerplate into your file!
  - Don't forget to use the `link` and `script` element to connect your CSS and JS files.

<iframe class="center-block" width="560" height="315" src="https://www.youtube.com/embed/Mvm2FtQ51Dg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

- [ ] **Update the title and add a header to your page.** Don’t forget to update the title of your website in the `head` element and use an `h1` element to add the header to your page

^^^

^^^
<span style="font-size:1.6em; font-weight: 600"> Step 2: Building the search form (10-15 mins) </span>
^^^

:::warning
🔎 **Essential Questions**

- How do we collect a variety of user information on a webpage?
  :::

Once you have your starter HTML files, let's build a simple form with an input for a search term and a submit button. The [HTML `form` element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form) represents a section of interactive controls for submitting information.

<br>

<iframe class="center-block" width="560" height="315" src="https://www.youtube.com/embed/2O8pkybH6po" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br>

**Note:** The `form` element itself sets up an area to collect user input but does nothing with the information. This is where JavaScript steps in to process the data and make appropriate actions. This is why it is important to give each element an `id`, `name`, and/or `class`.

:::info
💡 **Tip:** Check out our written guide on [**HTML Forms**](https://guides.codepath.org/webdev/HTML-Forms)!
:::

---

#### 📢 Now it’s your turn!

- [ ] **Build a search form**
  - [ ] **Add a semantic HTML `form` element to your page**
  - [ ] **Make sure to give the form an `id` attribute of `search-form`**.
  - [ ] **A text input that will be used to search for gifs.** Be sure to make this input required. You should also provide some default text. **Give the `input` element an `id` attribute of `search-input`**.
  - [ ] **A submit button with an `id` attribute of `search-button`**.
- [ ] **Fetch data from the Giphy API when the form is submitted**
  - [ ] **Add code to the `handleFormSubmit`, `getGiphyApiResults`, and `displayResults` functions as needed**
  - [ ] **Add appropriate event handlers to the form element**
  - [ ] **Use the native `fetch` function to issue the API requests**
- [ ] **Display results returned from a successful API request**
  - [ ] **Add an empty `div` section for gif results.** This `div` section should come below your `form`.
  - [ ] **When a Giphy API request comes back successfully, update the DOM to display the gifs**. Use the `displayResults` function to do so.
- [ ] **Handle paginated API requests**
  - [ ] **Display a 'Show More' button after each request**
  - [ ] **Keep track of each search query and how many consecutive times it's been fetched**
  - [ ] **Add code to the `handleShowMore` function to make it fetch the next page of results whenever the 'Show More' button is clicked**. Make sure to add those results to the DOM as well!
- [ ] **Use the DOM to create references to each of the items.** Remember that you will need to give your HTML elements selector identifiers by using the `id` or `class` attribute. You can use DOM methods such as `getElementById` or `querySelector` to create references to the HTML elements from your script file.

^^^

^^^
<span style="font-size:1.6em; font-weight: 600"> Step 3: Access the GIPHY API (20-25 mins)</span>
^^^

:::warning
🔎 **Essential Questions**

- What is an API and how is data stored and accessed?
- What are the GIPHY Endpoints?
  :::

#### What is an API?

API (or application programming interface) is a great way to access a large amount of data about users, technology, software, etc.

<br>

<iframe class="center-block" width="560" height="315" src="https://www.youtube.com/embed/Yzx7ihtCGBs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br>

When using any APIs, it is important to follow developer guidelines. Most specifically it is important to understand how to apply for an API key, identify important endpoints and their syntax, best practices for using the API, and attribution.

:::danger

#### DO NOT SHARE YOUR API KEY!

An API Key is a unique identifier used to identify and authenticate a user. An API key grants you use of an API and also lets the database know what type of user you are. This can help distinguish between access rights which is important when considering the security of the database’s data and its users.
<br><br>
There are many types of access given depending on the type of application you are accessing. Some API keys may be tied to an account with a credit card or other sensitive information. It is best practice to keep this information secret and to never share your key with anyone. API keys can be used indefinitely and are not secure. Hackers or malicious attacks may potentially use your API key to compromise your system or information.

<br>

What does this mean for this course? It is important to always generate your own key and to remember to **remove** your key when submitting your work on GitHub or even to CodePath! Always replace your API key in your code with a generic String.
:::

<br>

<iframe class="center-block" src="https://giphy.com/embed/3o6gbbuLW76jkt8vIc" width="480" height="270" frameBorder="0" class="giphy-embed" allowFullScreen></iframe>

#### Giphy API Endpoints

As you may recall, APIs are used to interact with multiple software and/or hardware applications. An **API endpoint** is considered a touchpoint or a way to communicate between the API and servers. Developers create different endpoints to specify the type of request.

Let’s take a look at some of the [GIPHY API Endpoints](https://developers.giphy.com/docs/api/endpoint#search).

- **Trending Endpoint**: returns a list of the most relevant and engaging content. This list is constantly evolving as their targeted audience’s preference may change daily.
- **Search Endpoint**: returns a list of gifs relevant to a specific phrase or word.
- **Random Endpoint**: returns a single random gif relevant to a specific phrase or word.
- **Upload Endpoint**: allows users to upload their own content to GIPHY.com. _Note: developers using a rate-limited key can only upload 10 gifs per day._

When using an endpoint, it is important to also pay attention to the request parameters. There are some parameters that are required for an API call. Since we want our users to be able to search for gifs using our application, we will need to use the Search Endpoints. Let’s take a look at the related parameters:

- `api_key`: This **required** parameter is quite common for use of API endpoints.
- `q`: This **required** parameter is the search phrase or word that we will use to find related gifs
- `limit`: This allows us to specify the number of objects to return. There are a lot of gifs on the GIPHY website. This is a great parameter to utilize to make sure our users are not overwhelmed by the number of results. We think that `9` results may be a good place to start!
- `offset`: Specifies the starting position of the results. The default value for this parameter is `0` and has a maximum value of `4999`.
- `rating`: Giphy provides ratings for the gifs uploaded to meet the needs of certain populations. They are similar to movie viewing ratings (G, PG, PG-13, etc. ). **To ensure no explicit gifs we highly recommend setting the `rating` parameter to `g`.** Read more about [GIPHY’s rating system](https://developers.giphy.com/docs/optional-settings/#language-support).
- `lang`: Specify a default language using 2-letter abbreviations. Read more about the [languages supported by GIPHY](https://developers.giphy.com/docs/optional-settings/#language-support).
- `random_id`: This id can be used to specify a user.

You may be thinking, how do we actually make a request with all of this information? The answer is **HTTP**!

For example: Let's say we want to search for "puppy" gifs using the Giphy API

1. Apply & receive a Giphy API Key.
2. Open up the [Giphy API Endpoint](https://developers.giphy.com/docs/api/endpoint/#search) documentation. Within the API, there are two URLs available. The `api.giphy.com/v1/gifs/search` is the path used for searching for GIFs.
3. Build your request, remember that HTTP requests follow this syntax: `http://hostname/endpoint?param1=value1&param2=value2`

```http
http://api.giphy.com/v1/gifs/search?api_key=MY_API_KEY&q=puppy
```

- _Note: `MY_API_KEY` is just a placeholder for the actual API key which may be a string of numbers, letters, and symbols._

:::warning
A good practice to use when making API calls is to store parameters in separate variables. This makes your code easier to read and gives easier access to values that could be used multiple times. Take a moment to look at the list of parameters for the Search Endpoint and think about which parameters may be useful to implement when filtering results.
<br><br>
Don't forget that when combining strings & expressions to variables we need to use [template literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals). We use the symbols `${expression}` to indicate an expression within a String.
:::

:::info
💡 **Tip:** Check out our written guide on [**Intro to APIs**](https://guides.codepath.org/webdev/Intro-to-APIs)!
:::

---

#### 📢 Now it’s your turn!

- [ ] **Apply for an API Key.** Create a GIPHY API Key by clicking “Create an App” on the [Developer Dashboard](https://developers.giphy.com/dashboard/) (you need to create an account first).
  - _Note: All API Keys start as beta keys, which are rate-limited (50 reads per hour and 100 searches/API calls per day.)_
- [ ] **Add attributions for the use of the Giphy API.** In order to use the GIPHY API, the company asks developers to conspicuously display "Powered By GIPHY" attribution marks where the API is utilized (see [SDK attribution guide](https://developers.giphy.com/docs/sdk#design-guidelines)). You can find approved [official logo marks](http://giphymedia.s3.amazonaws.com/giphy-attribution-marks.zip).
- [ ] **Add your API Key.** At the top of your `app.js` file, create a new `const` variable containing the API key created for you in the [Developer Dashboard](https://developers.giphy.com/dashboard/).

^^^

^^^
<span style="font-size:1.6em; font-weight: 600"> Step 4: Fetch data from the GIPHY API (30-40 mins) </span>
^^^

:::warning
🔎 **Essential Questions**

- How do we query our API for data?
- How does program flow and execute for code sequentially for actions that may take some time?
  :::

#### Asynchronous JavaScript & Fetch API

Sometimes you have functions in your code that rely on information or data from another step in your program flow. You see this quite often when you are loading a web page on a browser and you see the spinning wheel 🔄. You don't want your users to only see a blank screen, instead, there may be other things your server can do to load other parts of your webpage while they wait for results. This is exactly the basis of **asynchronous programming**. Asynchronous programming relies heavily on the blocking of code to separate functions that are dependent or independent.

<br>

<iframe class="center-block" width="560" height="315" src="https://www.youtube.com/embed/670f71LTWpM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br>

:::info
💡 **Tip:** Check out our written guide on [**Asynchronous JavaScript**](https://guides.codepath.org/webdev/Asynchronous-JavaScript)!
:::

---

#### 📢 Now it’s your turn!

- [ ] **Add variables for the parameters that will be specified when using the search endpoint.** We want to be consistent when displaying search results, which means we most likely do not want to allow these parameter values to be redefined. Consider using the `const` declaration for parameters.
  - We recommend holding variables for at least your `api-key`, `limit`, and `rating`. Add them at the top under the `Global Constants` comment.
- [ ] **Create a new function, `getResults`, that get results from the API.** This method should use the `fetch` method with your custom HTTP request. Then convert the response to a JSON object and finally return the data of the response. You can name this function a different name that you prefer, just make note of this as you continue along with the instructions.
  - [ ] **Scan through your program flow and identify functions that are dependent.** First, identify functions and lines of code that are dependent on other processes being executed first.
  - [ ] **Add keywords `async` to function definitions and `await` to asynchronous lines of code.** Refer to the information above to determine when appropriate to use `async` and `await`.

^^^

^^^
<span style="font-size:1.6em; font-weight: 600"> Step 5: Display GIFs results (5-15 mins) </span>
^^^

:::warning
🔎 **Essential Questions**

- How do we display results without refreshing the page?
  :::

It is important to follow the developer notes of any API you use. In the Giphy API, there are various Object types that may be returned from any API call. In our case, after making a call to the `search` endpoint, the API returns an array of GIF objects. You can read more about the various types of objects in the [Giphy API Schema](https://developers.giphy.com/docs/api/schema).

<br>

The GIF object has various properties, but the one we are most concerned about is the [`images`](https://developers.giphy.com/docs/api/schema/#image-object) property.

<br>

The Image Object contains a collection of Rendition Objects. These are various formats of the same gif such as fixed width, fixed height, original, downsized, HD, etc. Check out [Giphy's rendition guide](https://developers.giphy.com/docs/optional-settings/#rendition-guide) to learn more.

<br>

Each rendition for the most part contains similar properties: `url`, `width`, `height`, `size`, etc. Some renditions may have additional properties such as `mp4` and `webp` for alternative formats. The property we are most concerned with is the `url` property since this contains the direct path to the `gif` in order to display on our webpage.

<br>

In order to retrieve a single specific gif from our response, we need to traverse through multiple paths:

1. Accessing the GIF object from a specific index of the response data.
2. Calling the `image` property to get the Image Object.
3. Selecting a specific rendition `original`, `fixed_width`, `fixed_height`, etc.
4. Finally retrieving the `url` value of the object.

```javascript
response[index].images.rendition.url
```

---

#### 📢 Now it’s your turn!

- [ ] **Create a function to handle the logic for displaying gifs.** This function will take in the response data as a parameter and inject each gif into the HTML. We named our function `displayResults` but you can name it anything.
- [ ] **For each gif in the response data, inject a new `img` element where the `src` is equal to the `url` of the gif.**
  - Remember that results of the response data returns an array of GIF objects. Therefore we need to traverse or go through each gif individually and add them one-by-one. To do this we suggest using the [`foreach`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) method on the results that was passed in as a parameter of the function.
  - Use the [`innerHTML`](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML) property of the `div` element containing the gif area and the `+=` operator to append or add the gifs to the section on your webpage.

_Note: You can also explore using the [`map()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) method to traverse and accumulate results._
^^^

^^^
<span style="font-size:1.6em; font-weight: 600"> Step 6: Activate the form submit event (5-15 mins) </span>
^^^

:::warning
🔎 **Essential Questions**

- How do we respond to a form submission?
  :::

It's time to link all of our logic to the submission event! Let's take a look at what the program flow of our application should look like:

1. User types in a search term in the text field in the `form` element.
2. User clicks the submit button.
3. Computer senses the submit button submission and stores the search term in a variable.
4. Using the search term, the computer makes an API call using the endpoint and other specified stored parameters. The computer adds the search term using the `q` parameter.
5. Computer receives results from the API in the form of a JSON file.
6. For each gif:
   - Computer parses through the data to get the image URL and creates an `img` element with the `src` attribute equal to the image URL.
   - Computer injects the new `img` element into the gifs `div` section on our website.

We have already created the logic for handling input but have no way to connect this logic back to the search form.

---

#### 📢 Now it’s your turn!

- [ ] **Create a function to run the steps when the search form is submitted.** We named this function `handleFormSubmit` but you can name this something else. This function should take in the event and execute the following steps:
  - Store the search term by grabbing the `value` attribute from the DOM reference of the search text input.
  - Make an API call using the search term.
  - Display the results of the response data.
- [ ] **Update your function to allow users to search for additional gifs with different terms.**
  - Each time a new search starts, be sure to clear any existing gifs in the gif `div` area.
  - After the results are displayed, replace the search term in the input text box back to an empty string.
- [ ] **Add an event listener to the search form that senses the `submit` event.** Once we sense an event on the search form, this should then execute the function we just created to run the program flow. Recall that to do this we need to use the [`addEventListener()`](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener) method.

---

#### ⚙️ Testing

Try running your code now by launching **Live Server** through VS Code. You may have noticed that nothing happens after you search a phrase! No need to be worried just yet, what you need to implement next is asynchronous JavaScript. We will get to that in the next section!
^^^

^^^
<span style="font-size:1.6em; font-weight: 600"> Step 7: Loading more GIFs (5-15 mins) </span>
^^^

:::warning
🔎 **Essential Questions**

- How do we query an API with an **offset**?
  :::

The last component is to implement a "Show More Gifs!" button once you have loaded search results. In order to do this, it requires a little bit of math.
<br><br>
When making a call using the search endpoint, the Giphy API allows an `offset` property to be included. This will allow us to receive additional gifs without repeating the ones we already received. Before we dive into the math behind calculating the appropriate offset, let's take a look at an example.

#### Example: Calculating Offset

When making a call to the search endpoint, we recommended you use the `limit` property to set the maximum number of objects to return. Let's assume that our limit was set to 9 gifs.
<br><br>
Therefore after we make our request, the API processes the request and returns only the first 9 gifs in the result.

```json
offset: 0
result: {[gif_0, gif_1, gif_2, gif_3, gif_4, gif_5, gif_6, gif_7, gif_8]};
```

If we want to make a request for another 9 gifs, we should receive:

```json
offset: 9
result: {[gif_9, gif_10, gif_11, gif_12, gif_13, gif_14, gif_15, gif_16, gif_17]};
```

...and another request

```json
offset: 18
result: {[gif_18, gif_19, gif_20, gif_21, gif_22, gif_23, gif_24, gif_25, gif_16]};
```

Let's focus on the offset values.

Limit = 9

| Iteration | Offset |
| --------- | ------ |
| 0         | 0      |
| 1         | 9      |
| 2         | 18     |
| 3         | 27     |

See the pattern? The offset is just multiples of the limit number we set. In order to keep track of our offset, we need to also keep track of how many iteration, or times, we made a call to the API. We often refer to each iterations as `pages`, just like when you search a term on a search browser and you have to open a new page to get additional results.

```javascript
offset = pages * limit
```

---

#### 📢 Now it’s your turn!

- [ ] **Add a new `button` element in the HTML document after the gif `div` element.** Be sure to give this button a `class` name with the word `hidden` included.
- [ ] **Add a DOM reference to the new `button` element in the script file.**
- [ ] **Implement a style rule for `hidden` class to change the `display` property to `none`.**
- [ ] **Create a new variable to store the current page number and set it to 0.**
- [ ] **Add an `offset` variable to keep track of the offset value when making a `fetch` call.**
- [ ] **Create a new function to handle the "Show More" button.** This function should call the `getResults` function with the _same_ search term, then call `displayResults`. Don't forget to increment the page number as well!
- [ ] **Update the logic for when a form is submitted**. Be sure that after the initial search results are added you unhide the show more button by removing `hidden` from the `classList`.
      ^^^

^^^
<span style="font-size:1.6em; font-weight: 600"> Step 8: Exploring Git (30-40 mins) </span>
^^^

:::warning
🔎 **Essential Questions**

- What is version control?
- How can we use git and GitHub to collaborate with others?
  :::

#### What is version control?

**Git** is a version control system. It helps keep track of your work, explore changes when it was made, and compare different versions. **GitHub** is a cloud-based hosting service that allows you to store and manage Git repositories. There are many cloud-based hosting sites such as [GitLab](https://about.gitlab.com/), [BitBucket](https://bitbucket.org/product), [SourceForge](https://sourceforge.net/), and many more.

<iframe class="center-block" width="560" height="315" src="https://www.youtube.com/embed/8Dd7KRpKeaE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

#### Git & VSCode

You also have the option to use **git** within our VS Code editor. In fact, you can also use VS Code with GitHub as well. This is optional but you may be interested in learning more about these options. Check out the following resources:

- [How to use Git inside of VS Code](https://youtu.be/F2DBSH2VoHQ)
- [Working with GitHub in VS Code](https://code.visualstudio.com/docs/editor/github)

:::info
💡 **Tip:** Check out our written guide on [**Version Control with Git**](https://guides.codepath.org/webdev/Version-Control-with-Git)!
:::

---

#### 📢 Now it’s your turn!

- [ ] **Practice creating a new branch using `git checkout -b <new_branch_name>`.**
  - A short, descriptive branch name enables your collaborators to see ongoing work. E.g: `add-about-page`, `fix-pagination`.
- [ ] **Make a change to a file and push the changes to your new branch**
  - Use `git add` to add all files that were changed & then commit the changes using the `git commit` command
- [ ] **Create a Pull Request for your branch changes.**
  - Use `git push origin new_branch_name` to push your local branch into Github and then navigating back to GitHub to create a pull request.
- [ ] **Add a comment to a code and merge the changes.**
- [ ] **Delete your branch.**
      ^^^

^^^
<span style="font-size:1.6em; font-weight: 600"> Optional: Stretch Features </span>
^^^

#### Take advantage of more properties available in the Gif Object

- Take the time to also include `alt` text in your `img` element by utilizing the `title` string for Gif Objects.
- Display the gif `title` and `user`

Explore more properties by looking up the [Giphy Schema Definitions](https://developers.giphy.com/docs/api/schema).

#### Add more buttons to make different API calls

There are many different endpoints available with the Giphy API. Try exploring them and possibly adding a new button that makes a different HTTP request.

Here are some ideas:

- On `onload` your application automatically loads the top `trending` gifs.
- Allow users to get `random` results instead of the most relevant gifs.

Explore the [Giphy Endpoints](https://developers.giphy.com/docs/api/endpoint) list to get more ideas!

#### Add more CSS Styling

Enhance the styling of your application, you can mimic a similar aesthetic as [Giphy](https://giphy.com/) or you can make your own design! We also encourage you to explore the [Bootstrap framework](https://getbootstrap.com/) or [CSS Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)!

- [Google Fonts](https://fonts.google.com/)
- [Free visual guide to CSS](https://cssreference.io/)
- [Customizing Colors](https://tailwindcss.com/docs/customizing-colors)
- [Trending Color Palettes](https://coolors.co/palettes/trending)
- [30+ San Serif Fonts Perfect for Website Headings](https://www.elegantthemes.com/blog/resources/30-sans-serif-fonts-perfect-for-website-headings)
- [The Comprehensive 8pt Grid Guide](https://medium.com/swlh/the-comprehensive-8pt-grid-guide-aa16ff402179)
- [5 minute guide for the non designer](https://medium.com/startup-grind/how-to-not-suck-at-design-a-5-minute-guide-for-the-non-designer-291efac43037)
- [Customizing Spacing ](https://tailwindcss.com/docs/customizing-spacing)

#### Incorporate `:hover` styling and DOM events.

Add some more flair to your application by incorporating different style changes on hover, or inject additional information like the title of the gif or user who created it when you hover your mouse.

- [`:hover`](https://developer.mozilla.org/en-US/docs/Web/CSS/:hover) CSS Styling
- [`mouseover`](https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseover_event) DOM Event
  ^^^

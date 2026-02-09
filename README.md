# Scala Play Framework and React Tutorial

## Scala Play Framework

### Seed Project Example

- Apadted from [Introduction to the Play Framework in Scala by baeldung](https://www.baeldung.com/scala/play-framework-intro)
  - [GitHub](https://github.com/Baeldung/scala-tutorials/tree/master/play-scala)
  - [GitHub - Introduction to the Play Framework in Scala by baeldung](https://github.com/Baeldung/scala-tutorials/tree/master/play-scala/introduction-to-play)

NOTE: Best to edit the Play Framework code in IntelliJ

#### Project Setup, Installation, and Command-line Tools

```properties
# console
cd ../playReactTutorial
sbt new playframework/play-scala-seed.g8

name [play-scala-seed]: playTutorial
organization [com.example]: com.quoalacode (can be empty)

cd playTutorial
sbt run
```

Open http://localhost:9000 in browser

#### Project Structure

In our project directory, we see four directories created by the sbt template: , , , and .

- `app/controllers`: The controllers directory is where we will store our Scala code
- `app/views`: The views directory is where we’ll save our HTML templates (we will not be using)
- `conf`: The conf directory contains our router configuration which maps a request URL to a specific class and method
- `public`: Finally, the public directory contains the static content served by the Play Framework server

#### Making the First Change

The Play Framework provides us with a “hit refresh workflow.” The idea is that we can update our code and refresh the page in the browser to see the changes without restarting the server.

- Make new file under `app/view` directory called `firstexample.scala.html`. Add the following code:

```scala
// ../app/views/firstexample.scala.html
@()

@main("Welcome to Introduction to Play Framework!") {
    <h1>Welcome to Introduction to Play Framework!</h1>
}
```

In addition to modifying the HTML file, we have to update the Scala code. Let’s open the `app/controllers/HomeController.scala ` file and change the line: `Ok(views.html.index())` to `Ok(views.html.firstexample())`

#### How to Define a New Action

**Action** can be a GET, POST, etc.

In the previous example, we made some changes to the existing code and saw the results. Now, let’s look at Play internals to understand how it works and what else we can do.

When the Play server receives a request, it checks the config/routes file to determine which controller and method will handle the request. The method defined inside a controller and used in the routes file is called an action.

Let’s say that we want to **define a new action** in the `HomeController` class and **configure a new route**. Our code will get two parameters from the URL and print a value based on those two parameters. To keep things simple, we’ll read two numbers provided in the URL and display a page that prints the sum of those numbers.

To implement a new action, we open the Scala file (`HomeController.scala`) and add a new method that accepts two parameters, calculates their sum, and passes the result to the view template:

```scala
//  ../app/controllers/HomeController.scala
def printSum(first: Long, second: Long) = Action { implicit request: Request[AnyContent] =>
    val sum = first + second
    Ok(views.html.index(sum))
}
```

Now, let’s open the `index.scala.html` file, add the sum parameter on top of the file, and use it in the content:

```html
<!-- ../app/views/index.scala.html -->
@(sum: Long) @main("Add two numbers") {
<h1>The sum is @sum!</h1>
}
```

We just defined a function that generates a page. The first line of the view file describes the function parameters. The other lines are the code that generates the output.

The sum is calculated in the controller and passed to the Ok function which returns the content with the status code 200 OK.

Finally, we’ll need to open the routes file to add the new path and action:

```properties
# ../conf/routes
# NOTE: Do this in IntelliJ, VS Code messes things up
GET     /sum/:first/:second         controllers.HomeController.printSum(first: Long, second: Long)
```

The route consists of three parts. First, we specify the HTTP method. Next, we define the path and its variables. In our case, we’re using two variables that denote the first and the second number of the sum we want to calculate.

Finally, we’re specifying the controller and which action should be used to handle the request. Note that we’re using the path variables as the parameters of the function.

In the browser, when we open the following URL: http://localhost:9000/sum/5/15, we should see this page: The sum is 20!

## React Tutorial

Very similar React tutorial

```properties
# console
cd ../playReactTutorial

npx create-vite@latest

Need to install the following packages:
create-vite@8.3.0
Ok to proceed? (y): y

Project-name:

◆  Select a framework:
│  ○ React

◆  Select a variant:
│  ● TypeScript

◆  Use Vite 8 beta (Experimental)?:
│  ● No

◆  Install with npm and start now?
│  ● Yes / ○ No
```

This will also run `npm run dev`.
If not:

```properties
cd vite-project
npm run dev
```

Go to http://localhost:5173/ to see React project.

#### Project Structure

- `../src/main.tsx`
- `../src/App.tsx`
  - `useState`

# The Course Project Intro
    This is a project that we will build throughout the videos and learn how to use the different files and folders working with Angular. 

    The app we are building is a recipe book and a shopping list app. This will be two sections to seperate the two ideas. We will be able to manage our recipes adn view in detail and also push ingrediants needed to our shopping list. Now before we start coding these... we need to have a plan on what we want in them and how to execute them.

# Planning the App

    The first step is to lay out the structre of the app and the components we will need. This is just a rough idea of what we might need or want in it. It may be that some components will need to be added while coding or we might be able to merge two components together. So be flexable!!

    So lets start with the features of the app and we are going to have two sections the shopping list and the recipe book section.  

    The components we will need for this are:

Root for holding our overall application (the app component) every Angular app has this!

Header component so we can navigate between the two sections of the app. Since this will hold a lot of information and also contain a drop down menu it will be best to have this as its own component. 

    Now lets start with the individual features:

Shopping list component to hold the actual list and then in that component maybe a sub component to allow us to add and edit parts of the list. Also need an input field and a button to make it work with its own logic. So two seperate components in this section the Shopping List and the Shopping List Edit that will be nested inside of the List component. 

Recipe List component to show a list of all the recipes and then later on might be able to put each recipe into its own item. Thus because it holds a bit more information than just one line of HTML code and recipe-detail area.

    Not adding an area to be able to add new recipes yet bc thats a little advanced and we just want to display them for now.

Sub components off of the recipe book will be the Recipe Item and the Recipe Detail but nested into the main componet of the recipe book. 

    What models will be used in this app??

  Ingredients will need to be put into its own class type so it can be used later on and presents a clear interface or definition of what the data looks like. This will make it easier for the components to talk with one another.

  Recipe model that will contain things like the title, description and ingredients, etc. 

Lets start building the app and filling things in with dummy data we can adjust in the end.

# Setting up the Application

    To start the project must create a file/folder in main termainl...

ng new ____ --no-strict

    then open in VS code and run...

npm install --save bootstrap@3 

Now once all of that is complete open up the app.ts and remove the info in the class section and then delete all info in the app.html section.
  
    Now add the bootstrap to help with the CSS in ther termainal.

npm install --save bootstrap

      Then add the bootstrap link to the angular.json file in the "styles" section:

   "../node_modules/bootstrap/dist/css/bootstrap.min.css",
              "src/styles.css"

#  Creating the Components 

    Create the new folder for the header and add the files of:

header.component.ts
header.component.html

    Dont forget to add the component by importing and adding the selector and the URL to the .ts file. Then add the app-header tag to the top of the app.component.html file... finally you must add it to the app.module.ts

    import the headercomponent and then add it to the NgModule as well.

Ok lets add some more files and folders using the terminal...

ng g c recipes 

    This will generate the new files and folder for the recipes component and then deleted the spec or test file. Don't need it.

ng g c recipes/recipe-list (folder) this will nest the folder inside the main reciepes folder. 

ng g c recipes/recipe-detail
ng g c recipes/recipe-list/recipe-item

    generate all of these folders to be held inside of the main recipe folder. 

Shopping list needs to be created as well...

ng g c shopping-list
      and...
ng g c shopping-list/shopping-edit
    Dont forget to delete the test file as well.

# Using the Components 

    In connecting the files and folders together we need to add the tag to the app.component.html file.

<app-recipes> and 
<app-shopping-list>

    In order to place the components inside the same file and next to each other in columns. you have to add this to the recipies.component.html

<div class="row">
  <div class="col-md-5">
    <app-recipe-list></app-recipe-list>
  </div>
  <div class="col-md-7">
    <app-recipe-detail></app-recipe-detail>
  </div>
</div>

    Then inside the recipe-list.component.html must link the:

<app-recipe-item>

    Now lets work on the shopping list...
<div class="row">
  <div class="col-xs-10">
    <app-shopping-edit></app-shopping-edit>
    <hr>
    <p> The list</p>
  </div>
</div>
    Adding the above to the shopping-list.component.html. 

# Adding the Navigation Bar

    Starting in the header lets add some real content so it starts to look like a real web page. Add this to the header.html file in order to make the links clickable.

<nav class="navbar navbar-default">
  <div class="container-fluid">
    <div class="navbar-header">
      <button type="button" class="navbar-toggle" (click)="collapsed = !collapsed">
      <span class="icon-bar" *ngFor="let iconBar of [1, 2, 3]"></span>
      </button>
      <a routerLink="/" class="navbar-brand">Recipe Book</a>
    </div>
    <div class="navbar-collapse" [class.collapse]="collapsed" (window:resize)="collapsed = true">
      <ul class="nav navbar-nav">
        <li><a href="#">Recipes</a></li>
        <li><a href="#">Shopping List</a></li>
      </ul>
      <ul class="nav navbar-nav navbar-right">
        <li class="dropdown">
          <a href="#" class="dropdown-toggle" role="button">Manage</a>
          <ul class="dropdown-menu">
            <li><a href="#">Save Data</a></li>
            <li><a href="#">Fetch Data</a></li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</nav>


# Creating a "Recipe" Model

    Create a file named recipes.model.ts

    then we will use this to hold the makeup on how we will set up the model of how the recipes look.

export class Recipe {
  public name: string;
  public description: string;
  public imagePath: string;

  constructor (name: string, desc: string, imagePath: string) {
    this.name = name;
    this.description = desc;
    this.imagePath = imagePath;
  }
}

    This is the model set up and all the comands that we will start with.


# Adding content to the Recipes Components


    Lets start in the file recipe-list.component.ts

    in the export class section:

  recipes: Recipe[] = [
    new Recipe('A test Recipe','This is simply a test', 'https://afoodloverskitchen.com/wp-content/uploads/2021/06/disney-recipes-make-at-home-feature.jpg')
  ];

      Then in the recipe-list.component.html....
<div class="row">
  <div class="col-xs-12">
    <button class="btn btn-success">New Recipe</button>
  </div>
</div>
<div class="row">
    <div class="col-xs-12">
      <a href="#" class="List-group-item clearfix">
        <div class="pull-left">
          <h4 class="list-group-item-heading">Recipe Name</h4>
          <p class="list-group-item-text">Description</p>
        </div>
        <span class="pull-right">
          <img src="" alt="" class="img-responsive" style="max-height: 50px;">
        </span>
      </a>
      <app-recipe-item></app-recipe-item>
    </div>
</div>

# Outputting a List of Recipes with ngFor

    in the recipe-list.comp.html we need to add a few things..

 <a href="#" class="List-group-item clearfix" *ngFor="let recipe of recipes">

    for the h4 class {{recipe.name}}
    {{recipe.description}}
    im src:
    {{recipe.imagePath}}
    alt= {{recipe.name}}


    Add more items to the list and really grow this page.

# Displaying recipe destails

    Lets output the selected info about the recipe. This will go in to the recipe detail.html

<div class="row">
  <div class="col-xs-12">
    <img src="" alt="" class="img-responsive">
  </div>
</div>

<div class="row">
  <div class="col-xs-12">
    <h1>Recipe Name</h1>
  </div>
</div>

<div class="row">
  <div class="col-xs-12">
    <div class="btn-group">
      <button type="button" 
      class="btn btn-primary dropdown-toggle">Manage Recipe <span class="caret">
      </span></button>
      <ul class="dropdown-menu">
        <li><a href="#">To shopping list</a></li>
        <li><a href="#">Edit Recipe</a></li>
        <li><a href="#">Delete Recipe</a></li>
      </ul>
    </div>
  </div>
</div>

<div class="row">
  <div class="col-vs-12">
    Descripton
  </div>
</div>
<div class="row">
  <div class="col-vs-12">
    Ingredients
  </div>
</div>

# Working on the shopping list
    in the shop-list.comp.html add this:

<div class="row">
  <div class="col-xs-10">
    <app-shopping-edit></app-shopping-edit>
    <hr>
    <ul class="list-group">
      <a class="List-group-item"
      style="cursor: pointer"></a>
    </ul>
  </div>
</div>
        then in the shop-list.ts add this under export class:
  ingredients = [ ];

# Creating an "Ingredient" model
    make a new folder in the app folder and label it shared. it will be shared between the recipes and shopping..

    then make a file ingredients.model.ts
    input this info in the file..

export class Ingredients {
  constructor (public name: string, public amount: number) {}
}

# Creating and outputting the shopping list

    Now lets add info from above into the shop-list.comp.ts

    import the Ingredient info we just created at the top and then set..

ingredients: Ingredients[] = [];

    then add the new ingred. below the above info...
new Ingredients 
('Apples', 5),
new Ingredients 
('Butter', 2),
      now move over to shop-list.com.html..
<ul class="list-group">
<a class="List-group-item"
    style="cursor: pointer"
     *ngFor="let ingredients of ingredients">
     {{ ingredients.name }} ({{ ingredients.amount }})
</a>
</ul>

# Adding a shopping list edit section

    In the shop-edit.html..

<div class="row">
  <div class="col-xs-12">
    <form>
      <div class="row">
        <div class="col-sm-5 form-group">
          <label for="name">Name</label>
          <input type="text" id="name" class="form-control">
        </div>
      </div>
      <div class="col-sm-2 form-group">
        <label for="amount">Amount</label>
        <input type="number" id="amount" class="form-control">
      </div>
    </form>
  </div>
</div>


  




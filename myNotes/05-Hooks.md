# Hooks

## Creating a Search Component

Hooks is a really new feature to React. It's probably something that if you're on the Twitterspheres that you've heard of, right? And this got introduced maybe about, November is when they announced it. And it's been rolling out. And so now it's generally available as of React 16.8.

So the first thing I'm gonna tell you right now is, that's totally optional. You do not have to use Hooks right now. _But I am going to teach them to you first, because I think they're an easier way to think about writing React components._ And then we're also going to the other syntax as well which is class syntax, cuz you need to know both of them, okay?

For those of you that are watching the video, if you're watching this just to learn Hooks, there is a section here called Hooks in Depth. It's probably a good sport to jump in, right? Because that section is totally isolated from the other ones and it goes over all of the hooks.

- That will be in the Intermediate React course.

So let's go back to our code, let's make a new component here. And we're gonna call it `SearchParams.js.` It's gonna be inside the source directory as well.
And here we're going to import React from 'react'. Say const SearchParams is gonna be equal to an arrow function.

```jsx
import React from "react";

const SearchParams = () => {
  const location = "Seattle, WA";

  return <div className="search-params"></div>;
};
```

I'm gonna give it some `location`.
So this is gonna be something like Seattle, WA.
Make sure that this is an American location. The API that we're gonna be using is limited to the US. And actually I've limited the API to just Seattle and San Fransisco right now.

So maybe choose one of those.

And I'll explain why here in a second. So make a div here

### class reserved js, use className

And so one thing I haven't explained to you so far that is pretty important is I wanna give this a class name, right? So typically, I'll just say `class = search-params`, like this.

But notice it's gonna say, I don't know what class is. There's problem with using `class`. And the issue is that class is a reserved word in JavaScript. So if I say something like class Pet or something like that. Class here has a meaning in JavaScript, right? Just like I can't say, `const class =` blah, is because this is a reserved word, right?

Unexpected keyword means it's a word that you cannot use as a variable name, right? Same thing, I can't have this called const, I can't have this called let, right? `class` is another one of those. **So how do we get around that with JSX? Well, we use the name of the JavaScript API, which is a `className`.**

They didn't invent this, but this was not a limitation that React invented. And actually, it's the name of the DOM API as well, so it's consistent with what the DOM calls it. So that's why this is `className` instead of just class, right? I understand that people find that annoying, but it is what it is.

Okay, so inside of that we're gonna put a form. Inside of that we're gonna have a label and same thing here with for, right? For is another reserve word, as in for loop, right? So htmlFor.
And this is for the location.
Inside of that, I want to give it location with an input

```jsx
import React from "react";

const SearchParams = () => {
  const location = "Seattle, WA";

  return (
    <div className="search-params">
      <form>
        <label htmlFor="location">
          Location
          <input id="location" value={location} placeholder="location" />
        </label>
        <button>Submit</button>
      </form>
    </div>
  );
};

export default SeqrchParams;
```

id = "location". Location =, and then we're gonna put curly braces here because we want this location here to be put there. Sorry, and this isn't gonna be location, this is gonna be value. Value = {location}.
And placeholder = "Location".
And underneath that we're gonna have outside of that, inside of the Form button, Submit, like that.

Okay, lesson down here, export default.
SearchParams.
Last line there.
So we've made this new component, that's gonna be a little like search box. So we can search for various different facets of pets, right, against the Pet Finder API. And it has a div with a form inside of it.

And we have a input with a label for it. Some of you might find this like a little strange way to nest it. This is one way that you can do labels that you put the input inside of the label. There's other ways of doing it as well.

**But in the end, it's just good for accessibility**. So that if someone clicks on the location that it highlights the correct input, right? That's ultimately what we're going here for. And it's gonna have a value of Seattle, Washington, right? So let's go ahead and go render that out to app.js.

So instead of `app.js`,

Make sure you get this right. Yep, we can delete all this stuff that we commented out.
And here, we're not gonna import from Pet anymore. We cannot use Pet right now. We'll say, import `SearchParams` from `./SearchParams`.
We're going to delete all these pets, and just put `SearchParams` like that.

Okay, open `SearchParams` one more time, in case you missed something.
So now I need to make sure that my server is running. Mine is still running, but make sure yours is running. And then make sure you open _localhost 1234_ here. Something I kind of danced around but didn't explicitly mention was that.

You can't do that file open thing that I was showing you before, that no longer works. You have to be loading this off of Parcel's server, right? Which is why you have to open it off of the _localhost: 1234_.

So we're gonna open that again, which I have up here.
And you can see, I have a location here, with Seattle, Washington, with the Submit button there, right?

## Setting State with Hooks

I want you to try and type into this.
Congratulations, you broke the DOM. This is actually kinda difficult to do, right? [LAUGH] _And this is one of people's frustrations when they first learn to write React is like, this was so simple to do before. Why did we make something simple hard_?

Right, it's a valid thing to say. But I want you to think about how this works. Whenever I type something in here, so if I hit a keystroke right now, what happens is React captures that event. Then what happens is that kicks off a re-render cycle inside of its components.

So the first thing that happens is it re-renders app. _And then it gets done a SearchParams and it hops down into search params. Here, it says const location equals Seattle_, _Washington. And it re-renders, and what is the value of this input right here? Seattle, right? Nothing changes that_, right?

So when it re-renders again, it's still Seattle's because nothing changed it. So that's why, even when I type in there, it's not changing. **So in other words, two way data binding is not free in React**, which can be a point of frustration. I used to be an Angular developer.

I wrote a lot of Angular when I worked at Reddit. So this was frustrating for me because this used to be free to me, right? If, in Angular, just did the NG bind or something like that and it was just bound together and it worked and magical. That's no longer the case and I'm gonna argue for that.

**It's actually a benefit because it forces me to think through everything that's happening.** And I'm no longer limited by what the framework is gonna do for me. I have to do it, which I think is a benefit because later, when I come back to it, I can read everything that's happening, right?

**I don't have to know Angular super well or I don't have to know React super well to know what's happening because I can see all the code that's governed. It's very explicit**. This is actually kind of just a general trend for React. It's verbose, right? You write more code.

And that can be a point of frustration. But I argue that this is actually one of the biggest benefits of React because it's very understandable, right? It forces you to think through everything. Which means that when you come back to this a month later, you can re-read all the code that you wrote and understand what's happened, okay?

So we want to be able to change this now from Seattle, WA to something else. So how are we going to do that? Well, let's take a look at that.

Up here, where it says import React, for me, I'm gonna put comma`, { useState }`. Then I'm going to import that from React.

```javascript
import React, { useState } from "react";

const SearchParams = () => {
  const [location, setLocation] = useState("Seattle, WA");

  return (
    <div className="search-params">
      <form>
        <label htmlFor="location">
          Location
          <input
            id="location"
            value={location}
            placeholder="Location"
            onChange={e => setLocation(e.target.value)}
          />
        </label>
        <button>Submit</button>
      </form>
    </div>
  );
};

//...
```

So instead of having this location here, I'm gonna say const, square bracket, location, comma, setLocation. = useState, and then the default state, which is gonna be Seattle, WA,
Okay? Now, I have this location in this input. The thing you might notice, if you look at the console here, if I look at the console, it's probably gonna say, you provided a value prop to a form without a non-change handler.

That's why. We're going to give this a on change handler. So I'm gonna say on change = curly braces. I'm going to give it just a tiny function to run whenever an event happens. So I'm gonna say, whenever there is an event, setLocation to be e.target value. So this is a little, little tiny function, right?

And all it does it it takes an event, so you can actually put event there, if that makes you feel better about it. I just have a habit from forever that I call events `e`.

You can decide if that's useful to you or not.
And if you've ever written an event handler for jQuery or just normal JavaScript, that should look familiar, right?

It's a normal-looking event handler.

_And the other thing is if you have a single line of a function with an arrow function, the curly braces are optional_. So I could put that, and then it would look like that, which is fine as well.
So now, any time that a change happens in this input, it's gonna call setLocation with whatever is inside of the input.

So now if I go back over here and I start typing in here, it's gonna start working again. Now, why? Well, I type, it kicks off a reRender, search param reRenders. And then I have these two things up here, location and setLocation. Location is going to be the current state of location, okay?

- And then set location is an updater for that particular piece of state. So every time that that event happens, right, that I type into there, `e` is going to represent an event that happened in the input. And then I'm gonna call setLocation with whatever is inside of that particular event, or inside of that input, which is going to update that state that I'm getting here, okay?

_So then, when that re-render happens after that, location is going to now be whatever I've updated it to be_. Now it can be a little confusing that I have this string here Seattle, Washington. And obviously, that's not changing, but just keep in mind that this is always the default state, right, the first state.

And then after that, it'll be whatever it is at that point in time. **But that's, you have to keep in mind that that's what happens with these render functions for these components is they're run a bunch of times, right? Every time that you update your application, it reruns all of the renders**.

**So you want to make sure that these functions are not doing anything extraneous**, right? They shouldn't be updating any function. They shouldn't have any like side effects or anything like that. You want to keep them pretty narrow to the focus of rendering something, okay? So this is a hook, that's what the react terminology is here.

- :star: **And one thing that you need to abide by with hooks, all hooks begin with `use`**. Use state, use effect, use callback, use memo, all that stuff, all hooks begin with use. Even the ones like custom hooks, we're going to make a custom hook [COUGH] excuse me. We're going to make a custom hook here in just a second.

But if you see use something, it is a hook. So this is how you have stateful logic with React is with these hooks. So now at any given time, just to demonstrate to you, I'll just say a console.log('state of location', location).

Or even better, let's do this.

Let's just put an h1 right here.

That has location in it.
So now it says Seattle, WA right there, right? And if we start typing in there, notice that it's changing alongside of, because every time it re-renders, right, it's outputting that location there. So I could put Salt Lake City, Utah.

> > Speaker 2: Is using state different than setting state in this context, then, because it's setting a default, out of the box here.
> > Yes, so useState is like creating a hook, right? So and, when you get back a hook, you get back an array of two things. The first thing is always going to be the current state of it.

The second thing is always going to be an updater function for that particular piece of statement, right? So useState creates the hook. This is called set location because I chose to call it that, but you could totally call this updateLocation. It's a function that gives you back the updates that particular thing.

I choose to always call it set because then I can kind of see it, but that's just a convention that I have. That's not an industry best practice or anything like that. Does that answer your question? Cool. I should call out here, this might look a little weird to you.

This is also destructuring, right, because I know this is gonna be an array. This always gives back an array. And I know that the first item is always the state, and I always know the second item is the updater function. So that's why that's an array. Makes sense?

Cool.

So historically, if you've been writing React, you would have had to use something called set state, right? This is kind of supplanting the need for set state for these function components. I will show you later how to do that because it's important cuz it's still very much a part of the React ecosystem.

But for now, this is the way to do state with hooks.

## Best Practices for Hooks

An absolutely fundamental key thing that I need you to really understand right now with hooks is they never go inside of if statements, and they never go inside for loops or anything like that. Why? So I can't say like, if (something), I can't do this. This is not okay, never do this.

The way that hooks work is, basically, they're keeping track of the order that you're creating hooks. So if I have another hook underneath this, like for example, like for the animal, and setAnimal. And we'll make this dog or something like that. The way that they're keeping track of each individual piece of state is they're keeping track of the order that you're calling these things in, right?

So if I call these things out of order or if I have an if statement, and then, let's just imagine [INAUDIBLE], if something

If this is true on the first call and false in the second call, this will be the first thing called, which means that this is going to get location instead of animal, which is going to mess up everything.

So even if you're ignoring what is in useState, you still have to call useState outside of the if statement, outside of a for loop. So I'm actually gonna introduce you to an EL Synch rule that want to make you do that. But I just want to very much underscore the fact that you cannot put in an if statement and you cannot put in a for loop or really any sort of conditional or unpredictable logic.

Inevitably, someone at this point in time is going to ask me like, but what if I'm very careful that it's called in the same order? Just don't, I will find you and then I will shame you. [LAUGH] Just kidding, I don't know, but please don't. It's actually underscored in the docs, so it's just something like just never do it.

Always make sure that they're outside of that.

And this applies to all hooks, not just useState, all hooks in general. Make sure you are always using use something, right? That's a convention that React, if you use this convention, then the ES can help you enforce some of these rules,

## Configuring ESLint for HOoks

Open your console for just a second. I'm gonna stop my server, but you could just open a new terminal as well. I'm gonna say npm install -D eslint-plugin-react-hooks.
This is official rules from the React team about writing hooks.
So I want to introduce you to a couple of these.

So open your ESLint config really quick, and here inside of the rules, we're going to add a couple of them, react-hooks/rules-of-hooks, and we want that 2 error. So 2 will make it error on that,
And we also I need to add it to plugins as well.

react-hooks, like that.
Okay, and I am missing one of them here in my notes, let's just go find it. ESLint React, plug-in React hooks, this one.
And I have another one here that we should have in there. These ones, exhaustive depths.
So put in that one as well.

And we'll do 1.
So this one is going to force you to, we'll actually about later, but it has to do with the facts. So again, just to remind you, 0 is turn off, 1 is worn, and 2 is make it an error, right? So anytime that you mess up rule of hooks through an error, anytime that you have an exhaustive depths thing, it's just worn.

So let's take a look at what that actually does for us. If I say,
if {false}, or something like that, I don't know, and then I put this in there, it's gonna say, hey look, or this one right here, where is it?
There we go.

React hook is called conditionally. React hooks must be called in the exact same order in component renders. And you can see that comes from rule of hooks.

Rules of hooks, that makes sense? So it's gonna prevent you from doing stuff like that.
Now honestly, once you get used to doing that, and you just know never to do it, it's not really that helpful.

But as you may imagine, if you ship this to your coworker that doesn't know about that, this will prevent them from doing things that you don't want them to do.

## Calling the Pet API

Actually gonna show you a cool trick that parcel can do for you. So, we need to install a new client library to make requests against an API.
So, what I'm gonna do here, I'm gonna say, import,
ANIMALS like this from @frontendmasters,
/pet like that.

Now, you and I have not installed this, right? This was not in our package.json, but parcel is smart enough to say, hey, this is out on the NPM registry, I'll just go grab it for you. So you don't have to NPM install it, it'll just do it for you.

So if you see here, if I say save, it's gonna say Installing frontendmasters/pet right there.

And, while it's installing, it will rebuild the project, and now it's available to us on a project. Okay, so we installed this frontendmasters/pet. If you feel more comfortable, you can just say npm install @frontendmasters/pet.

But you can also have parcel just do it for him which is kind of a fun feature that it does for you.
And, again, if you look in package.json you can see that it installed it. Here, frontrendmasters/pet and save that in their forest.
Magical.
Okay, so now we have this ANIMAL's array which is just an array of strings I believe.

And here, we're gonna say const animal, set animal = useState and we're gonna start with a dog,
Okay?
Then we're gonna go down and then we are going to make underneath our input there, another label,
htmlFor = animal.
And inside of that, we're going to select Animal.

And, we're gonna put a select inside of that. So select,
id="animal",
value= animal.
onChange = e, and then setAnimal e.target.value.
So I'm gonna show you something pretty cool that we've done already. So it's saying, hey, if you're gonna do onChange, I need you to have onBlur as well.

Because some screen readers, when you're tabbing across things, don't trigger onChange events. Which means that your code would not work when being used with a screen reader, which is obviously a big party foul, right? And I love the jsx ally, just catches up for you and says like I'm not gonna let you go forward until you fix this, right?

Obviously like, this is so distracting to see so many red lines, I just can't even handle myself, right? So, we can fix that by saying onBlur = e, setAnimal,

e.target.value, as well, right? And now, it's all happy again cuz we fixed our accessibility issue,
Okay? And then we're gonna put a bunch of options in here of different types of animals that we can search for.

So the first one, we put in here, is just a blank option. This is gonna represent when we search for all animals, right?

I guess you could put in here as well,
Something like this,
And put All as well. That's probably not a bad idea.

And then here, we're gonna do curly braces and we have an array of animals here, right? And we wanna have one option for every animal in there.
So what we have is a list of strings, and what we need back from it is a list of components, right?

It makes sense? Like, we have a list of strings and we wanna turn those list of strings into a list of option components. Or option tabs or whatever you want to call them.

Well, luckily, there’s something built directly into JavaScript that translates one array of things to another array of things, right, and it’s called map.

So if I say animas.map, right, cuz it’s an array, then you give it a function that takes an item in that array and transforms it into something else. So I'm gonna take this string, right? Or, we'll just call it animal because that's what it is.
And then we're gonna have that return in option component,

With the value of that option component is going to be the animal. And, also that it's going to display animal.
Okay, it'll get a red line here for just a second which we'll fix in just one moment.
So does this make sense? First of all,

With arrow functions, you could have them implicit returned, right? So in this particular case, I had the arrow function and I have no curly braces, which means it’s implicitly returned. So this would be equivalent if I deleted this parentheses and deleted this one.
And I said return,

Like that.
Those two things are the same, but because I have the parenthesis which means continue on the next line, right, it's an implicit return. Does that make sense?
So those two things that I showed you are exactly the same.
So now I'm gonna have one option for every animal.

And indeed hopefully, if you go back and look over here, it's still upset but you can see,
I have a list of various different options. It's just a tiny bit bigger. So there's a barnyard, bird, cat, dog, horse, rabbit, scales fins, other and small furry, which are the type of animals that can be able to search for a crosses API.

## Unique List Item Keys

So it's saying, hey, I need a key, so let's talk about that for just a second. So how does React work in terms of like rerendering it? Everytime that something changes, it runs the rerender function here, right? So it runs this searchParams function again. I want you to imagine that maybe these options were more complicated.

Maybe they were deeply of necetries of DOM structures, so let's say I had the ability to resort these options one way or another. Well, what React would typically see is, this is different than it was before, I'm gonna go rerender everything. But if I'm just resorting them into a different order, that would be a lot of a necessary work, quite slow, potentially.

What would be really useful, is like, hey, React, I just reordered these. I didn't actually create and destroy anything, they're just in a different order now. And the way you can do that is you can say, key = some unique thing about that particular item. In this case they're all strings and I know they're all different.

So if I say key = [animal] then it's happy, because then it says if dog was here, but now it's down here. It's like I'm just going to take that option, I'm not gonna destroy it, I'm just gonna move it down there, so that's what key does. So it's a little performance thing that's really easy to do.

So the key here is, it needs to be some sort of unique identifier about that particular object, right? So maybe if you're sorting user objects, you can sort it by the email, or their user ID, or something that's gonna be unique per user. Then if it moves here, and then it moves down here, it is the same thing.

So that React can tell it's the same thing, makes sense? Now something that's really important is it has to be unique, so if I put 1, right? Now all of these are gonna have a key of 1 and is going to freak out.

It's gonna say, hey, I encountered with the same key 1.

That doesn't make any sense to me, so it'll do weird things if you do that.

In this case, it actually is rendering them, so good for that, but sometimes it just won't render them. So make sure it is actually unique about them.

## Breed Dropdown

We're gonna do the same thing but for breed. So breed and setBreed and we're just gonna make this initial state to be an empty object.
And then it's gonna look really similar to animal. So underneath this label here, above the submit button, I'm gonna say label, htmlFor equals breed.

And then we're gonna say, breed and another select.
And then here we're gonna have inside of that id equals breed. Value = breed,
From they're, we're gonna have onChanged = e returned e.target.value and we have to put that inside of setBreed.
Then same thing for onBlur, onBlur.

There's one more thing we wanna do, if I switch from,
Like cats to dogs, right? They have different breeds so I have to be constantly refreshing that list of breeds to reflective to of whatever the current animal is, right? So I can't have a poodle cat and I can't have a tabby dog.

That sounds weird but you can't, right? So sometimes it'll be switching between these things because I'm gonna have to be constantly getting that from the API. So what we're gonna do is when I give it a disabled, so disabled = breed.length. So if breed.length is zero, then disable it, right?

Then you want that to be true. You could also do this, breeds.length === 0, or,

Yeah.
We'll define breeds here in just a second, cuz that doesn't exist yet. But does this make sense, and the other thing this is another ligature that was talking about. It's three different equal signs, but it's put together.

So now this will always be disabled, like people will not be able to click on it if breed.length is 0.
Okay, and then we're gonna do another thing where you can select all of them. So I'm gonna say option,
All and then underneath that, we're going to have another one of these for loops or maps up there which is gonna be breeds.

Again, which we'll define here in just a second, .map(breed, and then return for that an option.

And inside of that option we'll have breed. Let's actually call this something different than breed cuz that's confusing. This would be like,
Breed string or something like that.
So breed string, breed string like that.

And we have to get that as well the key of breed string and value of breedString.

It's pretty similar to above. Again, we'll define breed in just a second, but I'll let you catch that up. Okay, so come back up here to the top. Also underneath breed and breedString, we're also gonna have to keep track of breeds and setBreeds.

And then it's initial state is gonna be an empty array, right? Because we're gonna be requesting against the APIs like I have a dog, give me back all of the dog breeds. So this is gonna be constantly changing depending on what the user is selecting.
Does that make sense?

So for now, breeds is just gonna be an empty array. So no matter what, if you go look over here, you'll just see that it's always disabled. And set to all because we're never changing that.

## Custom Hooks

Before we get to requesting against the API, I wanna show you how to do with something that's called a custom hook. So right now we've just been using useState all over the place, but if you notice HTML for animal, or this one here right animal and breed.

These are almost the same thing, right, to the point that like, it'd be nice if we could have some sort of like reusable bit. That would do like a drop-down for us, and we didn't have to do all this song and circumstance. And we could maintain them together, so let's actually go do that.

So make a new file here, and call it useDropdown.js.

Okay, here you wanna import React from 'react'.
And we're also gonna use useState.
Okay, and then I'm gonna say const useDropdown, this is gonna be our hook that we're gonna create. And it's gonna take in a label, some sort of default state, and some sort of a list of options to put in there.

Then down at the bottom we're going to export default useDropdown. So we're gonna say const state, useState, so we're gonna make this like a generic dropdown.
So not useState but setState
Equals useState, and the default state of this is going to be whatever they pass in, so default state.

We're gonna get some sort of ID, so you just need it to be something unique, because we have to give things keys and such. So I'm gonna use template strings, so I'm gonna use backticks, backticks are the ones next to 1 on your keyboard. Then we'll say use-drop down-\$ curly braces and then JavaScript expressions can go in here.

So, I'm gonna say, label.replace, so take any spaces out of the string and also make it lowercase.

So like if label here was something like Best Dogs Ever or something like that, right? What this would do is it would make this
Look like that, right, that's what this would output there, right?

Doesn't matter that it's readable, it just matters that it's unique.

Okay, and then the component that we're gonna make is called a Dropdown, so const Dropdown equals an arrow function. And we're just gonna use that implicit return again with the parentheses, equals label htmlFor equals the ID.

And then here, this is gonna have an ID, we need to put a label inside of that label which is coming in here from the parameters. And then we're gonna put a select inside of that.
And we have to give that select an ID as well, so id= [id], value = state which we created up here, so state.

OnChange, we're going to call e and we're gonna say to setState to be e.target.value. And then the same thing for blur, onBlur.
And then we have to give it that disabled thing as well, disabled equals options.length triple = 0. Here we're gonna give it an option of all, which is gonna have no value, right?

Which means it's going to have nothing selective when it's on all. And then here we're gonna say options.map and do the same thing with map. So this is gonna be some item in the array of some option, we'll stick with item. Use our implicit return with parentheses and say option key=[item], value=[item], and then item right there as well.

Get my parentheses all matched up, here we go.
So now we have this generic drop down component, right? That's gonna take in a label, some default state options and make a dropdown component. So now what we're going to return down here at the bottom, is we're gonna return the state, the Dropdown.

And then we're also gonna return this setState function as well.

Like that, and now we can use this just like we used a hook, because this is gonna give us the state. The Dropdown's gonna handle all of the setting and unsetting of the state, right? And then just in case as well for later, we're gonna return this setState function.

So that we can programmatically update it, in addition to using the Dropdown. So I understand this is a little abstract, we've taken the animal Dropdown and the breed Dropdown. And then we've just formed it into this kind of generic Dropdown hook.

Good so far? All right, so let's go ahead and go back to the search params.

And what we're gonna do, instead of doing animal and setAnimal, what we're gonna do is we're gonna say const.
First thing is you have to import up top, so Import useDropown from ./useDropdown. We still need breeds so we'll keep track of that, but now what we're gonna do is we're gonna say const [animal, animalDropdown].

And we'll actually just leave it at that for now, = useDropDown, and we'll give it Animals the label.

We'll give it dog as the default state, and we'll give it Animals as a list of options to choose from. Then for breeds we're gonna say const,
Breed, BreedDropdown and we'll leave it at that for now equals useDropdown with "Breed" empty string as a default state, right?

And breeds which again we'll handle this from the API here is just a second later. So now I have this animal Dropdown and this breed drop down, so rather than having all of this label stuff here for that. I'm gonna delete Animal and I'm gonna delete Breed.

So now I just have the location one, which is different, we don't wanna make that generic right now.

But what's cool is I just have an AnimalDropdown and a BreedDropdown.

And that's pretty cool in my opinion, we've kinda taken out this logic, we extracted it out to this useDropdown hook. And now we just get these little AnimalDropdown, BreedDropddown, self contained dropdowns. So if I save this and I go back over to my code this all works exactly the same way now.

But it's using this kind of shared generic class, or hook, as it were.

And what's great about this is now I can write all sorts of unit tests,and I can use this all over the place. And I can kinda guarantee to my future self that this is a really good piece of code that I can reuse over and over and over again.

Now we have a bunch of errors around unused variables, we will fix this momentarily, but you should expect to see that right now.

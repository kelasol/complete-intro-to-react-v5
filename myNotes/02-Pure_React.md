# Pure React
## Getting Started with Pure React
```javascript
// within your your embedded script tag below your react/reactdom "includes"

const App = () => {
    return React.createElement(
        "div",
        {},
        React.createElement("h1", {}, "Adopt Me!")
    );
};

React
```
 
So what we've done here is we've created a component called `App`. _And a component in this particular case is just a function that whenever it returns a result of `react.createElement`._

### Components in React are like Stamps
So let's chat for a second about what `createElement` is, or what app is for a second rather. I like to describe this as a rubber stamp, right? So here we have created our own rubber stamp called `App`, right? Now, you can go to the store and you can buy a rubber stamp, but a stamp by itself is not in and of itself useful, right?

It's only useful when you actually want to stamp it, right? So here we've created one, we haven't actually used the stamp, we've just created the stamp. So that's what this function does, is it allows you to basically stamp this as many times as you want, okay? `React.createElement` in here, what this is actually doing is it's stamping something here, right?

So anytime that app gets called, it's going to stamp a div, and inside of that it's going to stamp an h1.
**So that's really all components are in React, is it's just something that returns markup basically**, right? So again, we've created App, but this in it of itself doesn't do anything, right?
- We still need to render it...

### Using our Stamp
This is the creation of the stamp, so we actually need to go create it. So we're going to go render this to the DOM by saying `ReactDOM.render`. `React.createElement(App)` and then we're gonna tell it where to render it. And we're gonna say `document.getElementById` `root`.
So this is actually going to stamp our App because of this `React.createElement`.

So the `React.createElement` can take an either stamp that you've created, or it can take in a string like this where it's actually going to literally make an h1, right? Whereas this is going to be something that we've created, this is going to be literally an h1 that we're going to output to the DOM.


And as you may guess, it's going into root which is going to be this root up here.
So this is about the simplest React App you can build. So if I save this,
And go back over to my browser here, you can see here that you get a nice little Adopt Me logo.


So just say now replaced that with CSS, right? So that's where the h1 went, this is actually the h1 that we put up there.
So now we're done with the workshop and you can go home, I'm just kidding. I'm gonna use that joke five more times, so don't even worry about it.


So, this is the power of React is one, this is not very complicated in my opinion. You can be the judge to that, but at its simplest, this is what React is. It's taking a component and just using it, right? And the power here is that I can make components that I put inside of components that I put inside of components that I put inside of components, right?

So you kinda have this composability model with React.

## createElement Arguments
Questions so far? Yeah.
>> Speaker 2: Yeah, so I believe on line 12 you still have that div id root not rendered? On line 11, sorry.
Yep.
>> Speaker 2: Where did that go?
Where did the not rendered go?
>> Speaker 2: Yeah.
When you say render, like here, it blows away anything that's inside of it.

So it just overrides it. So for example, like if I put in here, throw new Error,
And then I go back over here, you'll see it actually just blue it away. It's still blued away.
Because it did try to render it, but let's, actually if you put it outside of that,


Then it'll say not rendered, right? Because it didn't get cleared out. So this just kind of helps to see that your JavaScript is loading. Not, it's just something I do, it's not necessarily like a best practice or anything like that.
This is the best error right here, by the way.


Okay, other questions? Yeah.
>> Speaker 3: In your app declaration you have it returns something which I'm assuming is whatever magic React is doing when you run that in the background. But then we're passing at another React.create element? What's up with that?
Yeah, good question. So let's talk about the three parameters that React.create element gets the first one is what kind of tag is it, right?

So you can see here, I've called it three times, react.createElement. I've called it here, I've called it here and I've called it here.
The first one is what kind of element it is. This is a div, this is an h1, and this is what you would call a composite component, which is a fancy way of saying a component that you and I created, right?

The second, which right now is an empty object, empty object, and undefined, cuz we're just not defining it here, right? Is all of the attributes that you want to give the component. So if I wanted this to have ID of something important,
Now this ID is going to be passed into this div.

So just to prove my point, if I refresh and come over here, and I look at Inspect Element, you can see here that this now actually has an idea of something important. All right, so this is the attributes that are gonna be put on the DOM element. Or if I gave it to app, this is going to be the attributes that are going to pass down into app that I can use.

We'll talk about that in a second. But suffice to say this is whatever you want to pass into the child element, in this case, the div. The third one is the children. So inside of div here is an h1, all right? And so that's what this third one is, it's whatever children you want to be passed into this particular element, right?

So in this case, the children of the h1 is just to text Adopt Me, right? But I totally could have pulled a span in here, right? Or something like that. Now, this can be either singular, or this can also be an array. Cuz a DIV can have 15 children, right?

So here I could also have, let's just do it for fun,
Okay? Now I have two h1s with Adopt Me, so if I go back over here, you can see that there are two h1s passed into this.
So technically this doesn't have to be an array, you can actually just pass these in all the parameters, it still works.


It's called variable verity, which is a stupid computer science word that I learned and I wanted to impress you with.
It just means that it can accept as many extra perimeters and it'll use all of those as children. Now I would say in your brain model this as an array because it'll make it simpler in your brain, because we will not be writing React like this for very long, so.

Just wanted to point that out, before someone online points it out for me.
Okay, so we're gonna go back to this.



## Reusable Components
All right this is really feeling gross to write this inside of a script tag, does everyone feel sufficiently gross inside? Good, that’s what I wanted you to feel this morning. So what I want you to do is I want you to open a file called App.js, just put it in the same source directory.

One thing I wanted to point out at this point as well. React is extremely flexible. It's not very prescriptive at all about pretty much anything. I like this because it allows me to make technical decisions for myself and not rely on the technical decisions of others, but that's a philosophy that I have, right?

And you don't necessarily have to share that. Which means we can organize our project however we want, React doesn't care, React has zero opinions on the matter of how you organize your project. I have organized this project just for simplicity, it's not a very big project. So, I'm not saying that this repo that we're gonna end up with is incredibly well organized, I'm just gonna say it's simple.

So that's one thing I wanted to throw out there, that's not something I'm intending to teach you with this workshop. Okay, so take everything from your script tag here, cut that out, and put this inside of your app. Delete that comment as well. Say that. Go back over to your index.html and put your src ="./App.js".


Okay, so all I did was cut that entire script out of the source here and I put that inside of app.JS.
Next thing we're gonna do is we're going to create another component.
We're gonna say const Pet = another arrow function
I'm going to return React.createElement.


Another div.
Another empty object, and inside of that another array and we're going to describe a pet very quickly.
So I'm gonna say react.createElement. Gonna make this an h2, lets make it an h1 actually cuz that's my notes have, empty object and you can put whatever your pet's name is there, mine's name is Luna, okay?


And then I'm gonna put three different lines in here, and this is gonna be an h1 and two h2's. And Luna is a Dog, and her breed is Havanese.
So I've created another stamp here, right? I have not used the stamp but I've gone to the store and I've purchased one and I'm just kinda holding it, not doing anything with it yet.


Okay, so here, inside of App, I'm gonna make this into an array so I can put multiple children in it.
And here, let's make this look nice.
I'm gonna put three instances of the pet item.
So I'm gonna put React.createElement Pet, then I'm gonna put this three times.


Now notice I'm not putting the rest of the stuff in there as well. You can if you want to. You can put empty object and empty array or something like that. You don't have to. It's optional. If you don't give it anything, it just assumes that it has no attributes and has no children.


So I made a rubber stamp, and I stamped it three times, right? So now, what do you expect to see when we render this? Well, I expect to see a div, right? Inside of that div, the first thing we see is an h1, and then I'm gonna stamp Pet, okay, so I'm gonna go inside of Pet here and I'm going to inspect a div, an h1 and two h2s here, right?

And I'm gonna see that this pattern repeated three times, make sense? It's now on 3, if we go in here, you should see Adopt Me, Luna Dog Havanese, Luna Dog Havanese, Luna Dog Havanese.
So this is what's cool about components is they are inherently reusable, right? I made one pet component and I stamped it three times.


Which is pretty cool, except for the fact that this is not very flexible at all, right? It's not flexible. There are other dogs besides Luna, I'm told, so we probably need to make this a little bit more flexible.


## Passing in Component Props
So I wanna make this more flexible so that I can have a different name, I can have a difference type of animal, and I can have a different breed, right? So what I wanna do is I wanna pass attributes into the pet component which we kinda already saw a little bit earlier with this ID thing, right?

This is how you pass it into like a div and we can use the same methodology to pass information into the pet component. So what I'm gonna do here, I'm gonna use multiple cursors with a VS code. So I'm gonna click and then hold alt, and click again underneath it like that.

And now I can write in three different places at once. So I'm gonna hit comma, and then I'm gonna pass in a name which for now is going to be Luna. A animal which is gonna be a dog and the breed, which is gonna be lavanese. And then I'm gonna had that reorganized so it's little bit easier to read


Okay, so now this information is being passed down. Now I'm gonna change this so they're not all Luna. Let's make this one my bird from growing up, which who's name was Pepper, and Pepper was a cockatiel. And we're gonna name this after my friend's cat which is the most amusing name I've ever heard for a cat which is Doink.

Doink is mostly blind, so Doink just kind of runs into walls and Doinks the wall, hence the name. Doink is a cat and the breeds like stray or mixed or something like that we'll go with mixed.
Okay, so now all this information is being passed into the pet component, but we have to use it, we're not using it yet anywhere.

So what this does is it takes this information and it passes it in as a parameter here called props.
So instead of saying Luna here, I'm gonna say props.whatever I called this here, which is props.name. So instead of saying dog here, I'm gonna say props
Instead of saying dog here, I'm gonna say props.animal is what I called it, okay?

And then here, I'm gonna say props.breed. So now what do I expect to see when I go look at the browser? It's gonna look relatively the same, except I'm gonna have three different pets instead of Luna three times, right?
So if I refresh the page, you can see here that I have Luna, Pepper, and Doink.


## Destructuring Props

Now, I'm gonna show you how to make this email a little bit easier. So writing props dot gets very old very quickly when you're writing React, so there's a thing that you can do called destructuring. So what I can do here is I can replace props, I know that the thing is gonna be called animal, breed, and name, right?

So I can actually just pull this out, so I'm gonna delete props here, put the parentheses back. And then inside of that, I'm gonna put curly brackets, like that. And then I'm gonna say name, animal, and breed like that. And this is going to pull out these particularly named properties within these objects and make them available as those variable names, right?

So instead of saying props.name, I'm just gonna say name.
Same thing here with animal,
And breed.
Makes sense? It's called destructuring,
And everything should work the same way, which it does.
Okay,
So that's the first section. So congratulations, you know a little bit of React now.

And the good news is this is kind of most of it. I'm going to show you a bunch of other stuff, right? I have to earn what they're paying me [LAUGH] but this is kinda like the core idea of what React is.
So there's a commit point here, so if you're falling behind and you wanna come up to this point, you can actually just move to the first commit in the repo, and this will take you to this point in the workshop.

The next thing we're gonna do is we're going to start introducing some tooling to help us out. Because you don't wanna write React like this, you can actually make React much easier to write. But again, this is still the core concepts of what React is.




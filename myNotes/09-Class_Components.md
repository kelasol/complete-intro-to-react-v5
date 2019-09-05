# Class Components

## Class Components

All we've talked about so far are hooks, right? How to do state with hooks? It used to be called **stateless functional components** and now people just call them **function components**. But if you see that terminology, those mean the same thing, right? It just means that a function that's not a class.

### Class Components

I'm going to show you how to do the other way of doing components which are class components. And they function in one most ways very similarly and in other ways, a bit differently.

So we're gonna make the details page be a class component.
So what I'm gonna do here is I'm gonna say class Details extends React.Component,

```javascript
import React from "react";

class Details extends React.Component {
  componentDidMount;
}

export default Details;
```

Okay?
**So, this is a JavaScript class**. There's nothing special about this yet, right? It extends React.Component which means that it has some inheritance that it's gonna get from a react component.
But other than that, it works relatively the same way. **The one hard requirement of every class component is it must have a render method**.

_It will not work unless you have a render method. And then this render method works mostly like how a function component works_, right?
So one thing to keep in mind as well is that,
**You can't use hooks with classes**, right? So `useState` will just simply not function inside of a class component.

Okay,
So, we're gonna put in a `render` method here in just a second.
But let's go ahead and put in a `componentDidMount`.
So, component, you can see here that it's actually gonna try and complete it for me cuz it knows it's coming from React.Component, that's how it knows all of these methods.

These are called lifecycle methods.
And, right today, we're gonna talk about `componentDidMount`. And `componentDidMount` is a very, very similar to use effect in the sense that it runs when it first start up, but then it stops. It doesn't run anymore after that, okay? Whereas use effect, you have to give it the dependencies and things like that.

ComponentDidMount just as like I'm gonna do this once when I first get created and then I'm done doing this thing, okay? So that's what we're gonna do with `componentDidMount`.

`ComponentDidMount` is useful for things like doing Ajax request, which is exactly what we're gonna do, right, when someone loads the page.

We wanna go to the API and get the pet information back from the API, right?.

So, that's exactly what we're gonna do when we say pet, which we are going to import that from import pet from frontendmasters/pet.
I wanna say ``, it's a single animal.
And then we're going to pass it.

We want to pass that the ID that we're getting from here, I like it from /details/1, right? We wanna pass it this number 1 right there, right, that ID that we're getting from the URL. So the way we're gonna do that is with this.props.id. So rather than getting that in as an argument like we were with functions it comes up this.props.

You can be assured that anything that's passing from the parents is gonna come in from this.props. The one thing to keep in mind with this.props is its immutable, you can't change it. So, a child receives props from its parents, and it can't change them, it can only read them, right?

They're read-only in that sense.

Does that make sense, yeah.
Okay, and then after that, this is a promise. I'm gonna say .then and we're gonna get the animal back from the API.
It's a pair function here.
And we're gonna say this.setState.
And we're going to get the name is going to be animal.name.

You could put like a return here, it'll just stop giving you all the red lines. We'll fix that in a second and I'm just getting sick of the red lines. [LAUGH]
Name,
Animal.name will do, animal is,
Animal.type.
Here will do location which will be a template string because we have to put a couple things together here.

We're gonna do animal.contact.address.city.
Space, animal.contact.address.state.
Description will be animal.description.
And the media will be animal.photos.
And breed will be animal.breeds.primary.
And then the other thing that we're gonna do here is we're gonna say, loading false.
So we're gonna say, loading false.

So, when we first load the page, we're gonna put it in a loading state, right cuz you're grabbing something from the API, right? And then whenever this comes back from the API, we're going to set that to loading false. Now the way that we're gonna set it to be a loading state is we're gonna say constructor up here.

Let's say, constructor, and constructor will take in the props. And you have to say super props. This is just something kinda, it's an odd ritual that you just have to do. It's going to be constructed with properties, and you have to handle those properties up to react, right?

So that's what this does. The super props says, hey call the constructor on my parent class which is a React.Component. Is that make sense? If you don't do this, react will yell at you. So, just get used to doing it.

Okay, here, I'm gonna set an initial stage, some would say this.state =,

Loading, oops,
True.
So let's talk about this.state versus to this.props. This.props is information that you get from your parent class that's handed down to you, right? This is, again, what was coming in via parameters before. Now again, we don't have hooks. So we don't have any way to keep stateful things using hooks, right?

So the way that we do that with class components as using this.state. Whereas this.props immutable and only comes from the parent. This.state is self-contained within the class. So no other components can modify its state, its master of its own state, right?

So in this particular case, I'm instantiating it like I'm creating the first set of state but everything after that I'll do with this.setState, right?

So after I call this .setState here, this will update this state up here, right? So this will get a bunch of new state from all this stuff, right? And then this loading true, will be set to loading false.

Make sense? Okay, so the thing to know about when I call this .setState, this is what's called a shallow merge, right?

So, I mean, it might even literally just says Object, you can ignore this but just showing what it does. Object assign,

oldState,
newState, right?
So that basically what that means is if any of these collide, like this one does with this one, it will over write this one, right?

But everything else will just be additive. So if this had some other thing,

This would not be overwritten, this would still exist afterwards, right? But it is shallow, right? So if I have deeply nested objects, those won't get overwritten, right, so it just does the top level.

And that's how you do state with class components. This is how I've been doing state for a really long time until hooks came along.
Something else I wanna call out here, notice these an arrow function here instead of saying function here.
You’ve probably noticed that I use a lot of arrow functions just by the nature of how I code, this in this place, it's actually required.

I don't wanna say required, it's very difficult if you don't do it this way.
So why? Why is this a problem here? Well, if I put a function here, what is this?
The answer is not what you would want it to be. [LAUGH] I don't actually know it's gonna be, but it's not gonna be what you'd want it to be, right?

When I put function here, it creates a new context when this is invoked. This.then is going to be invoked somewhere else. That might be Window, it might be the promise itself. I'm not actually sure what it gets invoked on. But, if I do an arrow function instead this will get.

It will not create a new context, which is what arrow functions do, they don't create new contexts, right? So this will be correct.

Does that make sense?
Some of classic components, what this is very important, right? It's actually one of the reasons why they chose to go the directions of hooks is because this is kind of hard to teach, right?

It can be.
There's just like a handful of things that you need to be aware of. And I think after that it's pretty to move past what this is.
And, you can also put here in the then, you can put console.error. So if there's any errors in the API, so it will just log it out to the console.

You should have better error handling than this, right? You should report it to your service and show that your error are some useful error message. This is not a course on error handling. They have a course on that, you should watch that. [LAUGH]

## Rendering the Component

So now, that we've done all of this, let's go make this, let's do the render now, right? So what I'm gonna do, the first thing we're gonna say is if (this.state.loading) then return an <h1> of loading.
Now, we could make this all pretty and have like a nice spinner and everything like that, right?

But I'll leave that to your imagination, right? For now, we're just gonna show a loading indicator, right?

If that's not true, then what we're gonna do,
Is I'm gonna do some destructuring in here, because this is how I prefer to do it. But this is just my preference here, I'm gonna say const {animal, breed, location, description, name} = this.state.

Okay, now, that I've pulled all of those out of this.state, I'm gonna say return inside of a <div>, and <h1> with the {name, I have to have two divs here. Two divs, <div className="details"> that to the end.
Up right there, I got that curly brace, okay.

So, yeah, make sure you have two divs here. I think I had to do that for styling purposes, so none of you have ever done that before, just put a random div, just so you could style it better? Okay, good, it's just me.

> > Speaker 2: [LAUGH]
> > All right, instead of that, put an h2, and then I'm gonna put these curly braces, and I'm gonna do same sort of ritual here, animal.

[breed][location].
Okay.
Under that we're gonna put a button that says Adopt [name].
And then we're gonna <p>, and then inside of that, we'll put the description.
So again, no hooks in here, you have to use this.state and set state. Instead of using update state or set state or set location, like we do with hooks, right?

We have one function that corresponds to one piece of state, you just use this .setState everywhere. So you'll get very familiar with this type of set state. Now, I'm trying really hard to refrain from calling this the old way of doing things, because I think this is going to be around forever.

I think that hooks and classes are around to stay. We have no indication that classes are gonna get deprecated. I'm of the personal opinion, this actually a really great API and this is still a valid way to write react and definitely a tool that should be in your toolbox.

But I will say that it is definitely easier to start with hooks, right? It's just functions and use state, so let's go see if this works now. This won't work, because details one is not a real place, so let's go click on Fat Boy Slim here. There you go, Fat Boy Slim is a rottweiler in Stanwood, Washington.

And his sweet nature and and has playful ways.

And then we'll make a button here in just a second that you actually be able to go to the adoption page, if you do want to adopt the animal as well.

## Configuring Babel for Parcel

Now I wanna show you how to do something, in my opinion, pretty cool here. This is a bit burdensome, to have to write out a constructor and construct a state like this. It also is, TypeScript can't figure this out, right? And so there's a better way of doing this that I wanna show you really quick, to instantiate your state.

If you have control of your Babel config, then you can do this. If not, then you may not, so it would be super useful if we could just do state = { loading: true }.

Wouldn't that be a lot nicer, if you could just do it that way?

Well, you actually can. But the thing is that this is actually a proposal for a JavaScript, and it's not actually a real thing quite yet, but you can make it work. So this will land in JavaScript, I think it's actually going to land in 2019 or 2020. So I'm gonna show you how to modify your Babel config, if you have to, with React.

So the first thing I need you to do is open your command line here.

So you can see here it says, Support for the experimental syntax 'classProperties' isn't currently enabled. And we're just gonna go enable that really quick.
So I want you to do npm install -D, and you have to install quite a few things to make this work.

babel-eslint @babel/core @babel/preset-env @babel/plugin-proposal-class-properties. I don't name these, I'm very sorry. And @babel/preset-react.

You're all done typing that now? I'm just kidding, it's a lot to type.
So what's going on here?
All this stuff is built into Parcel, and Parcel has just been handling this for us.

However, it gives us the escape hatch that if we have custom needs, which in this case we do because it doesn't have this one, the @babel/plugin-proposal-class-properties ,that we can say, hey Parcel, use our config instead of your config. Their config is basically like, let's target modern JavaScript, basically, everything that has already shipped with valid JavaScript.

In general, I don't say ship to production experimental JavaScript, except I'm okay with this one because this one's definitely gonna land. In fact, I believe it has already landed, and if I remember reading correctly, last week it landed.

But in general, that can bite you in the butt.

So we'll install that.

It should take a second to go through and load all that stuff.
And I guess while this is finishing, there, it finished.
So I want you to create a new file here. And I want you to call it dot, not inside the source, inside of adopt me, the root directory the project.

Call it .babelrc.

Okay, yes, used on.
Okay, inside of here I want you to put presets, and then we're gonna put two things here in presets. One of them's gonna be, @babel/preset-react. And one of these is gonna be @babel/preset-env.
Under that we're gonna put plugins, and inside of that we'll put @babel/plugin-proposal-class-properties.

So let's talk about what those two things are. presets babel react is brings with it all the things that you need to transpile React, right? So in understanding JSX, it also brings Flow. Not that we're using Flow at all, but that is included in the preset for React.

It's a bunch of transpilations around JSX. @babel/preset-env, this is a pretty, and I should mention that, a preset is a group of plugins, right? So in this case we're bringing one transformation, but our preset is a bunch of plugins, which is a bunch of transformations. This will transpile your code for the environment that you specify.

So luckily, you and I have already specified an environment, and that is in our package.json. Remember when we did this?

So this preset-env is gonna look at this browsers list, and say, cool. I'm gonna transpile all the JavaScript so it works in these browsers.
So that won't be very many things because, cuz of JavaScript works in these browsers because these are very very new browsers, okay?

But there's pretty cool stuff you can do. You can actually import your Google Analytics into preset-env, and it will actually transpile it specifically for your users, right? So you can say, hey, here's my Google Analytics. Transpile it so that 99% of these people can see my website.

That's built into the browserlist package. We're not gonna do that today, but it is possible. Okay, and then the plugins here, this is what's actually going to allow us to do that syntax that I just showed you, okay? I need you to do one more thing here.

So save this to your .babelrc. I need you to open you .eslintrc file, and we have to add a parser option. So parser, and I need you to put babel-eslint. So up to this point, eslint has been able to understand all the code that we have been using.

But now we've added a new experimental feature that eslint would choke on, so we have to say, use Babel to understand this code. And that's all this does.

Now, this might seem like a lot of ritual to use one feature, but I typically wouldn't do it just for one feature like this.

But this is actually to be more instructive on how to use Babel and Parcel together.

Okay, so now that you've put in that line 17 there, let's go back to our SearchParams page. And now, not SearchParams, we were on Details rather. Now it's fine with this.
Pretty cool, right?

Now, if I'm not mistaken, you should be able to say this.state., and then it knows that you have loading on there. That's because now TypeScript can understand your component, right? Notice it doesn't actually know that you have media, and breed, and load, and some of these other ones, because we didn't instantiate it up here.

But TypeScript has the ability now to go and run on your code and understand, okay, you have these things on your component. I can autocomplete these things for you. So if I want in here and set name: blink like that, just set and instantiate to be some sort of default thing.

That means I can come down here and say, this.state., and then notice now a name is in here as well.

It's the magic of TypeScript, and VS Code for that matter.
We'll get to that later, though. There's a whole section on TypeScript, so.
What if it doesn't work?

I'm just kidding. [LAUGH] Let's see what happened here.

This .state.return, did I leave a this.state in somewhere? Yeah, that's weird.
There it goes. That was just for me showing this.name and stuff like that, prettier than just wrap it onto that line.
Cool, so yeah, now that's still working with the public class property.

It's actually what that's called.

## Creating an Image Carousel

I want you to go make a new file now called carousel.js.
So you want to make like a nice Carousel so that people can like see the various different pictures of the animals, right?. So first thing we're gonna do here is we're gonna say import React from 'react'.

And then we're gonna say class Carousel extends React.Component.
Okay, so this is gonna have two things we're gonna have an array of all the various different images, and we're gonna have which one we're currently showing, the active one, the active index. So we're gonna say state =, and the photos is gonna be an active array, and active is going to be a number.

So we're gonna by default select the first one.

Okay, and then let's go ahead and make the render,
So when I say const photos and active = the stats state and we are going to return a div class name = carousel.
Carousel is a word that the more I type the more it looks strange, I just can't, don't know I don't understand it.

Then we are gonna put and image and the source is gonna be equal to photos, active, right?

So, photos active, this is gonna be an array of photos and stuff I select the second one, that will be two, right? And I'll select that one. And then, the alt text here will put for it is animal or something like that.

And then we are gonna put do class name = carousel- smaller.
And then here inside of that we are gonna put photos.map,
And then map has two parameters that it provides. One of them is the photo, right? But it also gives you a second one that is the index.

So when you grab that index as well,

And then we're gonna do an implicit return here.
If we were being more attentive to better accessibility practice is here. Probably what we'll do is to make this little button, right? Like to see we'll click on the smaller buttons and that would cause an interaction over here.

Cuz buttons handle focus a lot better for just the sake of time don't do this in production but I'm gonna show you just to put the event listener directly on the image.

So the key is gonna be the photo.
And then onClick where gonna have to do something with that.

So we're gonna say this.handleIndexClick, which we will build here momentarily.

When you give it the data- index, and what we're gonna do with this is here instead of the handle index click if someone clicks on the button, then we're going to pull the index off of the image here.

This is source equals photo className =. So, if the index is triple = to the active then we want to give it an active class. Otherwise we don't wanna give it a class okay, and then the alt is going to be animal thumbnail.

Okay, and this is gonna say you did a really bad thing just belong interact developments with quick handle must have at least one keyboard listener.

So here you can do something like on.
On key op or something like that, equals handle something like that. We're not gonna do that right now. For now, we're just going to ignore this.
I like hesitate to teach people that you can do this, it's like you can ignore anything, cuz one of these is eventually gonna be my core work and am gonna be so upset at you.

I went through and did this correctly and it takes a lot of time to get the accessibility correct on this, so for now I'm admonishing you to do it correctly, but we're just gonna move on for now.
Okay, so now we have to go make this handle indexClick.

Let's go ahead and just do the export at the bottom because I always forget this. So export, default, carousel, like so and then now we're gonna go make the handle indexClick. Well, let's do the derive state first this is kind of a fun one. So the photos are gonna be passed in from the parent component into the carousel ride, so it's not gonna get request in the details page, it's gonna request that, and then we're going to set that here in carousel, right?

But the pair is gonna give us a large object full of lots of photos in various different sizes and they actually just want to weed out. So just the sizes that we need. So, I'm gonna show you how to use static getDerivedStateFromProps, I'm gonna grab media out of this, so this is a special react method that it must be static, okay.

And what it's gonna do is, it's gonna take in a set of props and give you back a new set of states. So I'm gonna say let photos equals new array full of another place correlate picture. Place corgey.com/600x600 like that. So this would be the default image if it doesn't have any images, okay?

Otherwise, if media.length, then I want you to say photos = media.map and I'm just gonna pull out all the large photos.

Large and return that.
Right, so these photo objects will have small, medium, large and full, and we're just grabbing the large photos out of them.

So now photos will just be an array of strings of URLs, okay? Then down here we're going to return whatever object that we want to be merged into the state. So we're gonna say return photos.

So, again, getDerivedStateFromProps takes in a set of properties, does some filtering on them and then passes that on to the component.

So this component's actually never gonna see the media props. It's never really gonna use them, right? It's gonna use this photos which is gonna keep in state. So if you have any derived state, this is a good way to handle those situations. You don't have to do it this way.

I totally could have come down here and said, instead of photos dot map, I would have said this stop props.media.map. And then here I'll set photo.large and photo.large. I'll leave it to you decide if you think this is a good idea or not, I like it because it abstracts out some of the logic into this kind of handler, but

Up to you.

## Context

So one more thing, now we have photos, which we know is going to be an array of photo strings, okay? Now we just have to make this handleIndexClick function.
So, let's go ahead and do it this way first, we're gonna build it wrong first and then we'll show you how to make it right.

Okay, handleIndexClick, this is gonna take in an event of some sort like this.
And here we just wanna call this.setstate, with active being the event.target.dataset.index
So there's two things wrong with this, let's talk about both of them. The first one, if you've never seen dataset before, this is not a react API, this is a dumb API, right?

And dataset allows you to get two things that are on the data, on the each note tag, right? So I had this image tag here right, and I had this data index. So this dataset that we're referring to, let's close you. [BLANK AUDIO] There we go. So dataset index, that's going to refer to whatever is here, right?

So it'll have zero, one, two, three and four in there. That make sense? But the thing to keep in mind here is active needs to be a number because we're using as a number down here, right? Anything that comes react from the dumb is always gonna be a string, so we need to convert this into a number, we need to coerce this into a number.

There's a number of ways of doing this. You could do parseInt or something like that, or you can just say Plus. If you put what's call the unary plus right there, that will turn it into a number.

Okay? So that's problem number one solved. And I said this, sorry, this.setState right there, that's a third problem.

> > Speaker 2: Download?
> > I think it's nothing. I think it's undefined. You're on the right track that it's not correct, right?

We need it to be the component, right? We need it be the carousel component because we wanna call a setState on the carousel component, and this is either Window or I think it's undefined. I think react makes it undefined. Regardless, it's not what you want it to be.

So how would I make this correct? There's two methodologies here, I'll show you both of them. If I had a constructor up here, so just say I had constructor (props), and you don't have to copy this one, I'm just showing you this one, super(props). What you could do here if you don't have public class properties enabled in your project which many of you will not.

You can come in here and put, this.handleIndexClick=this.handleIndexClick.bind(this). This looks ridiculous, right? But what is this actually doing, right? It's binding the context of handleIndexClick to be Carousel, because we know what this is inside the constructor would guarantee it's gonna be the correct context, right? So this means that handleIndexClick can then be called, and this will always be correct, right, so this works.

There's an even easier way to do this, though, if you have public class properties like this.

I can just turn this into-
An arrow function.
Now it's correct again, right? Because we talked about arrow functions, right, they don't create new context when they're invoked, which means that it gets it lexically, which is not actually technically correct but effectively is correct, right?

So this is determined when you write it, right, so this is going to be wherever it was written. Whereas if I you call a function like this function here, right? It's going to be whether it's invoked, now recognize it's probably not a kind of an odd distinction to make but suffice to say, this will have the correct this because this event listener's not gonna create a new context.

So I'm gonna give you just kind of a rule of thumb here. Whenever you are passing functions down into children, right? Or whenever you're doing event listeners, use an arrow function,
Because that will guarantee what this is to be is correct. Like notice here in our componentDidMount in details and this one, notice that we didn't have to do any magic for this.setState for componentDidMount that's because componentDidMount, we already know it's gonna have the correct context.

Same thing with render, render is always gonna have the same correct context. So it's really just event listeners and functions that you're passing into children, that's it.

## Index Click Q&A

> > Speaker 1: Could you explain the plus sign in front of eventTargetDataSetIndex again?
> > When you get back something from the data set, it's gonna be a string, right? Like a string five. And I need it to be a number, not a string, right? So if I put +string5. I get back the actual number of five.

> > Speaker 1: Okay, so of course, it's an integer.
> > A number, yeah. So you could have also just said parseInt("5",10) which just means you want it to be in base ten. And that would give you the same thing as well. But plus signs is far less work, so. Very well there might be something like this, stop buying this here.

So.

> > Speaker 3: And then adding index to that call.
> > Yeah, and you could have done this as well right, for sure and then not had the data set here.
> > So then this would have had worked like this instead of getting an event.
> > There would have been an index like this and then you would've just been calling index.

Yes, this works. So let me tell you why people have historically not done this, and then I'll tell you why that's silly that people haven't done it this way.
So this does work. People did not used to do this, because this calling bind used to be very expensive, far more expensive than you would have ever expected.

It used to be one of the slowest things you could do in Chrome. Now about two years ago, Chrome fixed this and made dot bind much faster. But why is this different from doing it in the constructor? This is different because every time I call render, this is calling bind, right?

And if that was really so that means you slow down your renders, which means that you're slowing down the performance of your entire application. So people have established the best practice of, don't do it this way. But the good news is, they fixed it. It is much faster now.

And so this does actually work okay, but we still have to deal with old browsers and so in old browsers, this is still really slow. So it works and it's slow, it's creating and destroying functions every single time. That you run this, which hooks do now anyway. So I'm not really too sure if that's a big deal anymore.

But the real answer to that question is the dot bind ends up being expensive.

## Carousel Implementation

> > Brian: So go to your Details page,
> > Brian: And we're gonna import Carousel from ./Carousel.
> > Brian: And we're going to put this on the detail page. It's going to go, it's the first component inside of .details, so right here. Carousel, and just pass in media, so media=media. And we have to grab that out of this.state.

> > Brian: So import Carousel at the top, on line 27 grab media out of this.state. And then, again, this is coming from the API, if you remember. And then here, on line 31, be out of the Carousel component with media=media that we got from the API.
> > Brian: And that should be enough, now you should see a nice looking Carousel when you go to your page.

So let's go take a look,

> > Brian: Aw, look at that pup. And so now you can click on both of these, right? And it'll change which image you're looking at.
> > Brian: I just wanna pet that dog, that's all I wanna do right now.
> > Brian: Well, we have gotten up to another Commit point here.

So we now have done add Details route, add custom Babel config, and add the Carousel. So if you're behind, feel free to jump up to this Commit point.

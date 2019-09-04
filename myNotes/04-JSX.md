# JSX

## Converting to JSX

So we're going back to React, away from tooling for a while. So I'm just gonna leave my server running in the background here.
So far, I've been showing you how to write React without any really transpilation or anything like that just raw React underneath the hood.

**But I wanna show you how to use this feature called JSX, because we're using parcel now we can use JSX, whereas we could not before because parcel was not running on our code. And parcel do transformations using a project called Babel**

So here we have, let's actually go do `Pet.js` first.

Okay, so you're looking at this project right now, and you can see that this is gonna create a div with an h1 and two h2's inside of it, right? **So we're writing JavaScript to mimic markup**, right? So inside of your brain when you're thinking about okay, well, I need to have a div inside of that I need to have an h1 and h2.

### Value of JSX

**You have to think about the HTML that you want and then have to translate that in your brain to JavaScript that React can do, right? Wouldn't it be nice if we could just write the HTML that we wanted in the first place rather than having to have that translation layer in our brain?**

**Well, that's what JSX is and like that is all JSX is. It's not anything else, there's not additional features beyond just what I just told you**.

So I'll comment this out for just a second just like this. And I want you to say return, and then I want you to write div like this, okay?

```javascript
return (
  <div>
    <h1> {name} </h1>
    <h2> {animal} </h2>
    <h2> {breed} </h2>
  </div>
);
```

And then inside of that div I want you to put an h1 and then inside of that h1, I want you to put curly braces like that and put name. Then an h2, and instead of curly braces inside of that, we could do animal. And inside of another h2, probably guessed breed, yeah?

> > Speaker 2: Are there any Emmit shortcuts for writing in JSX?
> > There are, yeah, for sure. Do I have it, yeah, so
> > I'm pretty sure the way you have to do that right now is,
> > Let's just try it.
> > Yeah, so if I change this to be .jsx, it would just work out of the box.

There's a way to enable it for JS files, and I forgot how to do it. But so let's just talk for a second about why I'm not changing everything to be .jsx, the real reason I'm not doing that in _teaching that too is because the React core team said that they don't think it's necessary, so I don't do it and that's it_.

But if you do changes it be .jsx you'll get some of that stuff for free.

- :star: The other way is just to change the type in VS Code to JavaScript React from JavaScript. So on the bottom there it's says JavaScript, if you change it to JavaScript React.
  That'll work as well.

### HTML in JS JSX is not That

**I will personally tell you that I think this is far more readable**, right? There's less code, it's less dense, there's not objects and quotes and things like that. But when React was first starting out, this was a big barrier for a lot of people. It was a big barrier because we took a long time getting JavaScript out of our HTML, and now we're putting HTML into our JavaScript, right?

And that just feels wrong. But I'll tell you that this is better because it's not the same. Putting JavaScript inside of your HTML was a terrible idea, and whoever started doing that, they set us back like five years, if we're being totally honest, right? But whereas **this, we're just writing the HTML that we actually want in the code**.

And now I want you to know that this little div tag here, literally gets translated to this. If you go look at the transpiled output, right? So after this gets ran through Babble, everything here is just being translated into `React.create.Element`Calls, right? So there's no mystery here. It's not doing any sort of black magic or optimization or anything like that.

Literally what gets put it in the code is this,oops not that, this. That's why I have you write all this stuff first so you understand that this is all just `React.createElement`Calls, and there's nothing amiss here. Does that make sense?

And I promise you, there's nothing else in JSX, this is really it.

Anyone else have any questions, yeah?

### JS doesn't Support Multiple Returns

> > Speaker 4: I have noticed that sometimes if you try to make multiple divs in your return and your JSX it yells at you and you need to have something to wrap it all.
> > Yep.
> > Speaker 4: Is there specific reason? I mean, I understand the idea of returning only one thing but.

I mean that's precisely it, right? So if I put like,
If I put this here, right? It's gonna say, I don't know what to, adjacent JSX elements must be wrapped in enclosing tag, thanks, ESLint caught it for us, right? So let's talk about this for a second.

What does this get translated to if I have this? Well, if I uncommented this it would be like having,

React.createElement or contextElement, stop it element each h1 right, something like that.
And this doesn't make any sense because you can't return two things, right? I can't say return 2, comma 5, right?

JavaScript does not have this ability, some other languages have multiple returns, but not JavaScript. So that's why React requires you to return one top level thing because that's what JavaScript can do. Now there is a way to accomplish this which we'll get to later which are called fragments, but you return one top-level fragment which encapsulates two things, does that make sense

It's just everyone in the React community is JSX and people like it enough that even the Vue community some of them use JSX as well, right? So it's it's a pretty good pattern.

## Configuring ESLint for React

So let's address 'React' is undefined but never used. Well, that's not actually true if you think about it, right? What is div being transpiled to?
Well, it's being transpiled to React.createElement, right? Which means that React is being used. So anywhere that you have jsx, you actually have to have React in scope, that's a hard requirement.

**And the reason being is everything's being transpiled to React.createElement. But eslint doesn't know that**. So it's saying you're importing this and never using it, so what the hell?

So let's go actually fix that.
We'll just do that right now, really quick.
So come back to your,

Desktop right here,
And say npm install -D babel-eslint eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react.

`npm install -D babel-eslint eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react`

So that's a few things, but we need all of these tools to make sure that it understands React correctly.
I'll give you a second to type that out.
So let's talk about what these packages are.

babel-eslint allows eslint to be augmented by Babel, which is the transpiler, right? So out-of-the-box, typically, it doesn't understand React super well.

So that's what babel-eslint does. esIint-plugin-import gives you some new rules around importing and exporting things, just so you have good habits with that kind of stuff.  
eslint-plugin-jsx-accessibility, which is what a11y stands for, is just a bunch of kind of no-brainer things to do for accessibility, right? Like, don't make divs clickable, right, for example. This will just kind of help you catch those really easy accessibility things to do.  
And eslint-plugin-react is going to actually help us with some other additional React rules that we need, okay?

So install all that stuff.

And while it's installing, we're gonna go to our package.json.
Or not package.json, rather, but our eslint plugin, this one here.
So let's put this on multiple lines, so it'll be a little bit easier to read.
Okay,
So underneath eslint:recommended, the order of these is not super important.

:star: **The only thing is the two prettier ones have to come at the end**, right? So everything above it can be in whatever order we want. These one just have to come at the end because all these two rules do is turn things off, right? And you need them to be last so that they're off, right?

Whereas if I put eslint:recommended first, the last thing that will happen will be turning things on that prettier's trying to turn off.

So the first one's gonna be plugin:import/errors.
plugin:react/recommended.
And plugin:jsx- a11y/recommended, like that.

> > Okay, so this is just gonna be a bunch of rules that are gonna coming in from those plugins that we installed.

We're gonna install a couple of plugins here. One of them is gonna be react, one of them is gonna be import, and one of them is going to be jsx-a11y.

**So extends our sets of rules, right, and plugins are new abilities for eslint, right? So import, this is going to allow it to associate that if this file exports something, this other file can import it.**

And if it doesn't export, then it can't be imported somewhere else, right? That's kind of what import does. This is going to do some more abilities with understanding accessibility. And react is going to fix a lot of our React problems, okay?

Then we're gonna have another one here called rules.

This is where we can actually turn on and off specific rules. We're not gonna be doing prop-types today. So go ahead and turn off react/prop-types,

```json
"rules": {
    "react/prop-types": 0,
    "no-console": 1
},
//....
"settings": {
    "react": {
      "version": "detect"
    }
  }
```

Which is what 0 does, it turns it off.
prop-types are like a very weak type checking that React can do for you.

We're gonna get to TypeScript later in the intermediate React workshop. So prop-types are a useful when you're using TypeScript.

And then another one, we're gonna say, no-console, that one, just turn that one on 1.
Whoops.
I frequently use console.log to debug things, right? And so if you have no-console enabled, it will not let you, and it will error out on that.

Whereas 1 will be a warning, right, so it'll be green underlined instead of red underlined.

Cool, so those are the two that we're gonna turn on right now.
Okay, and then down here we gotta do one more thing, one of them is underneath env, here, settings,

And react.
And then you have to tell eslint which version of React you're using. But you can also just say, can you just figure it out yourself? So that's what detect does.
Which means it'll figure it out from your package.json.

**So at this point I'll tell you, this is my React config that I use on almost all my projects. It's pretty good. The one thing I'll say here is eslint react/recommended has some rules that I don't necessarily agree with. And I think we'll actually end up turning a few more of them off later.**

So just because react/recommended says something is a rule, you can question it a little bit.

Whereas don't question anything in eslint:recommended, that's gospel truth right there, right? That one you can just, everything it says is great. react/recommended, you can question what's in there.

Okay.
So now, if I save that, you'll notice now that this is not red anymore. And actually if I comment it, it's gonna say, hey, React has to be in scope or this isn't gonna work, right?

So it's actually gonna help you out with more React stuff now.

## JSX Composite Components & Expressions

### Converting App.js to use JSX

So let's go convert app.js really quick, cuz we don't want this to be,
Just we want it to be JSX. So I'm gonna say return. Let's talk about the parentheses for just a second, why do I put parentheses here? Well, if I just say return and then put something on a new line, and I put it on a new line so it's easier to read.

**Well, the way the JavaScript works is if it sees a new line, it just ends it right here after `return`**. So it actually works like that, where it just ends, right? So if I surround this in parenthesis, it's saying hey, I'm not done yet, continue on to the next line.

Okay, and so h1>Adopt Me!, like that. And then now I wanna use this Pet component that I made up here, right? So how am I gonna use that? Well, it works like this, Pet. So I actually can use a composite component as if it was real HTML, which is really cool.

And then if I wanted to add that ID back here, so this ID would be, I called it something important, right, like that. **That works the same way, and attributes or properties for this pet component works exactly the same wa**y, so I can say name = "Luna",

Animal = "Bird", or no, "Dog", and breed = "Havanese".

Now, you see this self-closing tag thing, right? I know in HTML that that's optional and frequently I leave it out, cuz again, I'm lazy and don't type things like that. But **I'll tell you that in JSX they actually are required, right? You need to let JSX know that this is a self-closing tag so you have to put that trailing slash**.

Okay, I'm gonna put three of those. This was "Pepper", "Bird", "Cockatiel", and this was "Doink", mixed "Cat".

What is kinda fun though, with JSX you can even do self-closing divs as well, like that. Which is not legal in HTML but is legal in JSX, which is kinda fun.

And actually, Prettier will just do it for you. If I do that, when I save, it's like, no, you really meant that, which is kinda fun.

> > Speaker 2: So JSX would take this and turn it into a React.create, with the first argument being div, the second one being emptyObject, and the third one being a list of React.creates with all of those?

Yep.

> > Speaker 2: So what's the benefit of writing XML to turn it into JavaScript, to turn it into HTML?
> > Yep.
> > Speaker 2: Why don't it just write HTML?
> > Ultimately, this is a template of some sort, right? Kind of falsely so, right? Cuz it's not actually a template, it's actually just function calls.

But in the end, this is actually imperative, cuz it's being executed, right? Whereas HTML is declarative, it's not something you can execute, right? So everything I've shown you so far, this is all very static data, right? But you can imagine here, instead of having Luna equal this, I could have API result, right?

And now I can pass dynamic information into Pet. **It gives me the power of JavaScript to manipulate this**. Does that answer your question?

> > Speaker 2: Yeah, thank you.
> > Cool, yep.
> > So actually, along those lines, I think something that I skipped over explaining were the curly braces over here, and let's address that really quickly.

So right now, if I go over and look at my site, I think everything should be fixed again, hold on, one more thing to fix here. Rather than having a React.create link down here, make this app like that.

So again, line 31 there, just make that React.create... `render(<App />)` like that.

Okay, so now that I've done that, go back over to Pet.js. And if I go over to my app, hopefully it's still running. No, not that one, this one. Did I stop it from running? I did, npm run dev.
Refresh the page. So I have Luna, Pepper, and Doink, right?

What happens if I remove the curly braces here?

Now it's literally gonna be the name, right? So if I save this and go back over here you'll see that it says literally the word name here, right? **So what the curly braces do is you're letting JSX know this is a JavaScript expression in here.**

And the term expression means anything that can be on the right side of an assignment. So if I say `const x = something`, let's just say, I don't know, named.toUpperCase}, right? So anything that can be on the right side of an equals sign here, this is considered an expression.

So for example, you can't have an if statement on the right side of it, right? So a `const y = if`, this doesn't work because an expression and a statement are different, right? A statement is a whole idea, right? So all of line three would be considered one statement, but everything here on the right side is considered an expression.

Does that delineation make sense? Okay, so that means here inside of name, I can say `.toUpperCase` and invoke that right here, or this could be invoking animal, the function, or something like that, or this can be + animal, right? So anything that can be on the right side of an equal sign, but I can't put a full if statement in there.

But you can use ternaries, right? Cuz ternaries are technically expressions, and a ternary is like the question mark thing. I'll use them later. They're fun or not fun, depending on who you ask. I think they're fun. So anyway, and again, yeah, now I've messed up everything, right, so now Luna is all capitalized, and you have HavaneseDog and CockatielBird, right?

So that's what those are about. And it's just a single curly brace there, that's how it works.
And so you can mix and match them too, so I could have name like that. And if I go back here, it says Name: Luna, Name: Pepper, and it does that concatenation for you.

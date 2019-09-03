# Tools

## npms & Generating a package.json File

So far we've been talking about Just React, and you'll never see anyone using JustReact, right? Like we've been doing so far, that's just not a very common pattern for writing React, there's always tools involved

- Always tends to be tooling...
- We're gonna introduce you to like, three or four tools, and then we'll get back to writing React. So the first one I wanna introduce you to, you may already be familiar with is NPM. Which does not stand for node package manager, but sort of stands for node package manager.

You should use the _LTS which stands for long-term support_, I think. Or I'm making that up and you can believe me. Okay, so with node comes mpm, if you don't have these tools installed right now. Just go to nodejs.org, and you can just install it right after there as well.

`npm init -t`

So pro tip, if you put `-y`, it won't ask you any questions and it just generates a file for you. Otherwise you get this interactive prompt. Like what's the name of your project? Who are you, blah blah blah, and I just can't be bothered. So, now if you look at my project, you can see here that I have a package.json.

But there's a couple of things that we're gonna be concerned with here. First one, we're gonna have dependencies and those dependencies are gonna be track in here, right?

So then, whenever I say `npm install`, **it's going to grab the same dependencies**, right? So if me and Start working on a project together, I can show this with her. And we could work together on that project, right? Something like that.

## Prettier

### Tooling continued... prettier

he first one that we're going to install here is going to help us keep high code quality: one of them is going to be Prettier.

So the first thing I'm gonna say down here is I'm gonna say MPM install -D, which is gonna mean it's a developer dependencies, right?

So when I'm deploying my code to production I don't need to have Prettier go with it. This is just for me on my local environment, and I'm gonna put prettier like that. Now you can say npm install like this, again, I'm a lazy person, so I like to type less, so I'm gonna put `npm i -D`, like that.

So now I have Prettier installed, and Prettier is going to do things where I can format my project consistently, right? I'm sure many of you have worked on projects where some files have tabs, some of them have spaces, some of them have trailing comments, some of them don't, so on and so forth.

**So Prettier is a project that kind of just takes all the conversation out of that and just standardizes on a format**. Now, I recognize, for some people, they don't wanna let go of their format, because it's the best one, and they thought of it first, and we should all use their format because they're much smarter than us, right?

**We all know that person, and none of us like them. So what Prettier does is it takes away the whole conversation, it's like, no, everyone's gonna use the exact same formatting, and we're all stuck with it. And it's all slightly different than we would have chosen it, but we're all on the same format.**

It's actually one of my favorite tools, because I actually really don't care what my code looks like as long as it's well formatted, right? As long as it has a format that's consistent, I don't care. And the great thing about Prettier is it just does it for you.

I've now introduced it at every company that I've worked at, and I will continue doing it to every company that I will work at.

## npm Scripts

So inside of your package.json, there's a thing called scripts. Here we have one called test, which we don't have any tests for this project yet, so we don't have anything like that.

But you can see here that it'll run echo, no test specified. So if I say npm run test, right? It's gonna run whatever is in here, and it's gonna echo error no test specified, right? So you can see right there error, no test specified. So that's what this script is for, it allows you to put some sort of Bash, or ZSH, or PowerShell command in here.

And then it'll run that whenever you say npm run test, or format, or whatever you put inside of here. So we can put anything in here. I'm gonna put one called format.

And what format is going to do is it's gonna say prettier, so it's gonna run this prettier...

```json
"scripts": {
    "format": "prettier \"src/**/*.{js,html}\" --write",
}
```

So what this is gonna do is this is going to run Prettier on any file and any directory, that's what this \*_/_ means, inside of the source directory that has either a JS or an HTML extension. You need the backslashes here because this'll pass it into Prettier and it allows Prettier to resolve this rather than having Bash resolve it for you.

And then you come here at the end.
Okay, so if I run this, it's actually not gonna write to it, so I should be able to say npm run format.
And you see that it's actually printing it out, which is not what I want, I want it to actually write.

So what we're gonna do here is we're gonna say `--write`.
And you can see there now I have `src/app.js` and `src/index.html`.
So this is helpful because there's gonna be someone on your team that doesn't want to integrate with your work flow. So this allows them to just run this command right before they commit and then push it up, right, because you want everyone reading this command on your team.

## Prettier Setup

### Run Prettier on Save

Now as you can see here, I haven't been using that. I actually have it runs prettier every time I run save. So I'm gonna show you how to do that. So inside of VS Code, go to the Extensions, which is this one here, and I have one called prettier.

### Two VSCode Settings to Change

And then you need to turn on two things for me. One of them you wanna turn on is Format on Save.
So the editor format on Save, check that one.
The second one that I want you to check is require config. So prettier down here, you can see, mine's not checked.
So prettier, require config.

So now that I've done that, this project doesn't have a config yet, we haven't made one. So if I go and do this, I'm saving it, and notice that it's not fixing it. That's what we want right now, right? We only want it to run on projects where it has prettier.

So the next thing we're going to do is we're going to create a config file. So create a new file save it to the root directory here adopt me and you have to call this call it dot.prettierRC.
`.prettierrc`

And then I need you to put two magical characters in here, empty object: `{}`

Now there are a few things you can configure about prettier, you know, if you want to be tabs or spaces, do you wanted to have spaces here, or not have spaces there? There's a few things. I told you, I don't actually care, I just want it to work.

So this is just saying, give me the default config. But if you want it to have some sort of config in here, you could say, "singleQuote": false. I only wanna have double quotes or single quotes, true. I only wanna have single quotes, right? It'll be things like that, but, again, I don't care, so I'm just gonna put empty object here.

So now if I go back over two app.js and I save, now it'll actually use. It'll run prettier on every single time that I save which is what I wanted.

This can be done with sublime. This can be done with other editors as well. Just read it off of prettier's website.

They'll tell you how to do it.
Questions about that? Is that working for people? Cool. Again I love this because it means I get to shut down like a part of my brain that thinks about formatting things.

You just get to shut down that thread of your brain and focus more on code. There aren't really very many alternatives for prettier so if you want to have a code format or if that's something that you want prettier's by far the standard. There may be others but it’s either this or nothing.

ESLint has a thing called fix which you can use that as well but it’s not the same thing.

## ESLint Setup

So down here we're gonna say `npm install -D eslint` `eslint-config-prettier` like that. This is going to install two different things for us. It's gonna obviously eslint, which is a code linter.

### Difference between ESLint and Prettier

Let's talk about what the difference between prettier and eslint now. Because people kind of confuse the two and understandably so, there's overlap.

**Prettier is purely concerned with is there a space here?**

- Is there return here? How does this file star, it's very mechanical, right?
- **It's very much, how is this formatted, but it doesn't care about what the code actually does, right?**
  So it doesn't look like does this variable exist? - Does this you know, are we using the wrong method here? - Are we using old JavaScript here? - As long as it parses like prettier doesn't care.

Eslint is much more concerned with style, right. It's concerned with what methods are you using? You know, accessibility friendly, right? It can check kind of those things.

Does that make sense? So you can have eslint check some of the mechanical stuff. But it doesn't have the power that prettier does for that kind of stuff. So that's why we're going to install the prettier config, to basically say hey eslint. That stuff that you sometimes worry about like spacing, don't worry about it because prettier has it, right?

So install both of those.
Okay, and now we have both of these. Eslint-config prettier, eslint, and now we're going to go create A eslint-rc as well. So make a new file, save it. And call this .eslint-c.Json.
They require you give it the extension, whereas .prettierrc does not.

Because you can also configure this in YAML, as well as in JavaScript as well. But we're gonna do the JSON way of doing it right now.
And yes, I use a period. Did you have a question?

> > Speaker 2: When I ran the command in the terminal, it created a new file called package walk, is that JSON?

Yep, it should do that. All right, so let's let's just address that briefly. If I go back over here, it created a new file here called package Lock. So package lock is a lock file. [LAUGH] So what it actually does is when you deploy your code to production, it's actually locked down the versions.

If you look at this you can see that it has integrity checks, and like where to download it from and what version it's on and stuff like that. And you want it to have this, because now I can install exactly the correct versions in productions. So, what I'm running in my computer, is exactly what's running on production.

So, the way that you do that when you're running in production, don't do this on your local computer, but if I do it npm, oops, npm ci. It'll actually use the package lock and sort of package of JSON to install exactly the correct version, right? Whereas if you do NPM install see if I got a package of JSON here.

Let's say you know next week they release 1.17.1, right? If my file looks like this. It'll actually install at 1.17.1. Reason being it's because that's a patch version, so it should be compatible, right? Does that make sense? Whereas if I do MPMCI, it'll actually install exactly the versions I was using.

So it'll still install MPM 1.17.0. Does that answer your question?

> > Speaker 2: Yeah. Thank you.
> > Cool. Yep, it's the same thing as a Yarn log file. The packaged log and Yarn log accomplish, as far as I know, exactly the same thing.

## ESLint Configuration

So back to our eslint.json.
So, we're gonna create a file here, this one we do have to configure a little bit. So, the first one we say is extends, and we get an array of things that extends, right? So this is like sets of rules to use.

So, the first one that I'm gonna say is use eslint:recommended.
Then we're gonna use prettier and prettier/react.
So, what is extends, right? So ESLint is configurable down to the rule, right? So there is probably hundreds of rules that you can use with ESLint. We're going to be using, basically, like the bare minimum set here, which is eslint:recommended.

Like everything in eslint:recommended everyone should be running all the time. I don't think it's a controversial opinion to state, right? It's a pretty bare minimum set of things, like don't have variables that you never use. That's one of them, right? Or don't use with or something like that, right, which is like a super old construct in JavaScript.

Now, there is a bunch of ESLint configs, right? There's standard, which I taught previously before. There's airbnb, which is one that I taught as well before. And those ones are much more opinionated. And so I've kind of just started using esl recommended because, again, it kind of goes along with my methodology that anytime that you introduce friction to a developers' ecosystem, they start writing codes slower because they're fighting with tools instead of writing code, right?

So, in general, I want developers to write code however it flows into their brain, right? And not hinder them, and only hinder them on things that are totally necessary, right? So this will catch bugs, but it's not gonna force you to write code in a specific way. Does that make sense?

And how opinionated you wanna get about that is up to you.
Okay, so this is those, we're gonna say plugins. We're not gonna give it any plugins right now, but just lets go ahead and put that in there, we will put some in there later.
ParserOptions,

Okay, so the ecmaVersion we're gonna be using, let's do 2018.
So we're gonna be using the latest version of it that it understands, which is 2018. I don't think 2019 is quite out yet. SourceType. We're gonna be using modules, ecmaFeatures, we're gonna be using jsx, which is to true

So, ecmaVersion 2018, this means we can use things like async/await, we can use things like things like that. Module means that we're gonna be using import and export, right, es modules. EcmaFeatures, jsx in a second, we're gonna be writing jsx here. So we're just going to put that in there so it understands that.

And then two more things down here at the bottom. Env, we're going to be using es6, so it's not going to choke on things like a async/await, for example.
So, es6 true, one of them is going to be browser true. So this means there's going to be things like setTimeout and document and window and things like that.

And node, cuz eventually we will be writing node later in this class. So, don't choke on things like HTTP and require, and things like that. So these are your defining global variables, okay? I use this ESLint file frequently, so this is a pretty good just like baseline ESLint file, it's not super opinionated.

Okay, next thing I want you to do inside of your package.json, we're gonna put another command in here. And put lint,
And we're going to put eslint, and we're going to put that inside of.
Quotes here, and we're going to put it in everything inside of src\*_/_.js and jsx.

Except we're not even gonna do jsx today in terms of pass, whatever, you can leave it like that. That's what my notes have. And then you can put in here --quiet, it's kind of noisy and quiet just kind of removes some of the noise from that.
So, now, whenever we run ESLint, it's gonna run ESLint across our app.js file as well.

But whatever js files we put in there, it will run.
So, just to kinda prove my point to you, we're gonna say npm run lint.
And looks like we have something. Which we should, right? It says react is not defined because it doesn't know where react is coming from.

So, if we come into our app.js, it's gonna say, hey, what's react? I don't know what that is. So where did that come from? Which is what it should say, right? Because it doesn't know.
So, we'll fix that here in a second, but now this is working.

Now, again, I don't run that npm run lint command very often because now it's just inside of my editor, right? I can see that red underline, I can hover over and say, this is not defined, you need to fix this. So, I'm gonna show you how to do that as well.

There's an extension for all major editors, but coming here to extensions, search for one called ESLint, and it's this one. Which has about almost 20 million downloads, so install that one as well and that should just work. So, once we have the ESLint 1 installed here, ESLint, like that, you should start seeing these things inside of your editor.

So, if you don't like ESLint 1, you should, cuz I think it's a great tool. It's, again, one of my favorites. Cuz it really does help me to be a more productive developer, right? If I say things like const x = 5 and then never use it later, it's going to say, hey, no one used variables, right?

You created this very well and you never use it, so why do you have it, right? And often that's a case of, let's say, I went down here and I accidentally set React.createElement(Ap) with one P, right? It's gonna say, I don't know what that is, right? So, it immediately highlights these errors like this, or if I put three Ps in there or something like that.

It helps me catch a lot of really common dumb errors like that very quickly. As opposed to when I go to play into production and everything crashes because I put an extra P in there, not that I've ever done that. So, big fan. So, I like ESLint because it's very extensible.

So you and I can both write custom ESLint rules. When I worked at Netflix, we had a ton of custom ESLint rules. But there are other tools, one of them would be JSHint which has been around forever. There's JSLint which Douglas Crockford created. But I'll just say that ESLint is very much the standard and it's the one I suggest that you use.

It's actually been adopted by the JS Foundation, which used to be the jQuery Foundation and is now called the OpenJS Foundation, so.

## gitignore

We are going to create one more file here. This is going to be a gitignore file. So inside of your source directory, create a file called .gitignore.
Like that. Not inside your source one, this is going to go inside of your root directory inside of adopt me.

And here if you are not familiar with get, this is just telling get is like, here is a bunch of stuff, I don't want you to keep a track of inside of my repo. Okay, so .getignore yes use dot. So the first thing you never want to track is node modules, because that's why you can npm install them wherever you want, right?

And then also if you're on Mac you should always ignore DS_Store, which is a file that Mac creates for dumb reasons, let's not talk about it. Let's just say that they're dumb reasons. And then for later parts of the course, you're going to ignore your cache. You're going to ignore dist.

You're going to ignore coverage. You can ignore the dot VS Code directory or not, that one's up to you. It's just where VS Code keeps track of all your personal preferences for the project, and then you're also going to ignore the .emv file. So this is just telling VS Code, ignore all this stuff, never commit this stuff.

This is stuff that I just have for me and not to be put in my get repo
Okay, so there's another commit point here. So if you fell people behind the tooling you can feel free to just jump up to this commit. It's something called like add npm scripts and ES Lint and prettier and things like that.

## Parcel

So the first thing I wanna say about Parcel is that I have taught, historically in this class, I have taught Webpack and Webpack is a phenomenal tool. It is part of the OpenJS Foundation as well. There is a great course in Frontend Masters about it. If you wanna learn Webpack and React together I teach it with React V3.

And that's still totally valid if you wanna check that out. But I'm gonna use a different packager today that is called Parcel. The reason why I chose to teach with Parcel is it's extremely hands-off. You just point it at a file and it just kind of figures it everything out by itself.

There's no configuration to it. Webpack is phenomenal. It's super powerful. If you have crazy things you need to do with it, Webpack is your friend in doing crazy stuff like that. But it's kinda difficult to set up. It's inevitable that with power comes complexity, right? So suffice to say I love both tools.

I'm just choosing Parcel today so that we can focus on React and not necessarily focus on the bundler. What we're gonna do now is we're gonna say npm install D parcel- bundler like that. That one takes a second cuz there's a lot of stuff that comes with it.

This is the actual tool that will bundle every code together, and get it ready. 1 for your development environment, and 2 for production. And it's really smart. You just point it at your index html file and it discovers all the paths just by figuring everything out. And it figures out like this is a TypeScript file, or this is a JavaScript file, or this is a CSS file and it just neatly packages everything for you.

It's a pretty impressive tool.
It's one I actually I use quite frequently. And both Webpack and Parcel definitely worth supporting. They both have open collectors, so that's something you feel inclined to do. You can see that they actually drop a link in there for you.
Frontend Masters does, thanks Frontend Masters.

Okay, so now that we've done that, I want you to go into your package.json. And we're going to add another script in here that's going to be dev.
And this is gonna say parcel src/index.html. So again, all you have to do with Parcel is you just point it at the index.html file and it just figures everything else for you.

So now I can go into my adopt me. Well, so first thing I wanna mention here. This was confusing to me for a long time until someone pointed it out to me. As I was like, how does it know what parcel is, right? I don't think I have parcel available here, right, it says parcel command not found.

So like how does it know that? Well if you go inside of your node modules here, which is where all of your node, when I say npm install bundle there, that's where it goes into node modules. And there is a secret.bin directory her. Of all the various different binary tools I can use, right?

And one of them in here is called parcel, which is connected to parcel-bundler. So that's how it finds it.
Echo's not in here right, for example, Echo's just part of like Mac. But it is able to find parcel and prettier in here. So, just so you know that that's how that gets connected together.

So now I can say, npm run dev.
And it's gonna build all the stuff together. And it's ready in 1.76 seconds. You can see here that there's now a dist and a .cache director. That is something that Parcel creates for you. You can just basically ignore it, and I can open now.

So if I Cmd + click this, it'll open in my browser. And you can see, magically, I'm running on localhost:1234, but now this is being packaged by Parcel.
Now there's some pretty cool stuff about this. If I go into app.js and I change this to be,
I don't know, maybe add another Adopt Me in here, and I save this.

It automatically refreshes my page for you. So it does a hot model refresh for you out of the box for free. You don't have to do anything about it, it just works.
And that's really it, we're not gonna configure parcel anymore than that. It's smart enough to figure everything else out.

## Installing React & ReactDOM

Now let's go fix this error that React doesn't know what this is. What we're going to do, if you don't know, to stop the serve you hit Ctrl-C. I think that works on any platform. You send an interrupt command to it and say stop this, right?
So here I'm gonna say now npm install without the D because these are production dependencies, react react-dom, like that.

So this is gonna go install our two packages off of the npm registry.
Take a second to do that.
Okay, now instead of going back in my index.html, I'm gonna delete these two script files. Cuz I don't wanna load these off the CD anymore, I wanna load them off of my local computer, so delete that.

So all we have is the root and our app.js.
Okay, now we're gonna go back into app.js.
And we're gonna say up here, import React from 'react'. So this is going to import the default export from the React package, okay? And we're going to say import and I'm gonna say {render} from react-dom.

Now, some of you might not be seeing this autocompletion here. That extension is called NPM Intellisense, which again is here. NPM Intellisense, right there,
Quite useful. So import render from react-DOM is where we want that one to come from.
So I show you this, I could've just done import without the curly braces here and said react-DOM like this.

And now this would work because this is called reactDOM down right here, but I wanna show you how to input the specific thing, so I wanna import just render from reactDOM. So this is saying reactDOM has a specific export called render and I want you to input just that, okay?

And then down here just erase the render, so it's just render like that. So I wanna say this is similar to destructuring. It's technically not destructuring, this is just how modules work. But this is just saying react-dom has a specific instance, export render equals something, heah, question?

> > Speaker 2: When you're using an import statement, how do you know whether or not you should use the curly braces?

Is that just for if you want to import one specific feature?
Yes.

> > Speaker 2: Okay.
> > For example here from React, I can actually import specific things. So like, I cannot actually just import creed element, because it specifically exports that, right? And then I wouldn't be using, I would just be using create element like that.

In general, I would encourage you to do specific exports most of the time because parcel will do a thing for you called tree shaking. It actually uglifies the actual thing that does the tree shaking, but what that does is it's live code inclusion. So it will only include code that could ever potentially run.

So in this particular case, let's say react-dom had 1,000 methods and we're only importing 1, right, it would not include the other 999. If they packaged it correctly which is a big if because most of them don't. But like a good example that would be like low dash right?

Low dash is a huge library has like 200 methods right? And you don't, no one ever uses all 200 methods right? So what you wanna do with that is you wanna import just a few methods that you use and then it won't include the other ones, right? That is like the benefit there, potentially, it doesn't always work out that way.

For me it just helps me to be explicit that I know this only uses render from react-dom. So what I wanted to get to is, this actually isn't helpful, because if you include react-dom you get the whole thing, because it's not packaged for tree shaking. And then the other thing is that there's not a lot of wasteful stuff inside react-dom, so there's not a lot to tree shake out anyway.

So now if we save this and go back over to our project, it should still work, right? So now, you have to run the project of course, npm run dev, like that.
Once it's finished building, you can see this looks like a JS file that's loading, it's only loading this app.js file.

And it's not loading anything else, it's not loading like those other files from the repo. So you can see that that reacts now being included inside of our app.js instead of being loaded from some other CDN. And you can see that it's much larger than it used to be here, now it's 965 KB instead of being, like the probably 5 it was before because it includes React.

Now keep in mind this is the development environment which means it's massive. If I patched this for production it would be much, much smaller. So don't worry about file sizes until you actually do the production builds, so just keep that in mind.
Right now, this project would probably be 35 KB, I guess, cuz React is about 32.

## Separate App into Modules

So now we have a bundler, we can do whatever we want, right? Now we have more leeway to do things. So the first thing I want to do here is I want to split pet and app into two different files, right? I can't think of a reason why you would not have one component, one file.

It's always that way. You don't ever have two components in a file. I've not really seen a good reason to do that before. So one component, one file. So I'm gonna show you a pretty cool trick that VS Code can do for you. So I'm gonna highlight this and then I get this little light bulb here.

This light bulb is called a code action. So I'm gonna click that and there's a couple things here. The one that I want is move, you might not see all of these because I have other extensions installed. But the one that you wanna do is move to a new file, which all of you should see, right?

So click move to a new file. And all the sudden I have a new Pet.js file which has an export in it, and app is importing from that file. It's pretty cool, right, you like this, cool? Okay, cool. So what's really cool about it is, it's actually TypeScript that does that for you.

It's not VS Code. TypeScript is actually running on your code, even though we're not writing any TypeScript right now. VS Code is constantly running TypeScript against your code, to understand how your code works. And so that's what's actually able to do that. Now, I prefer default exports, so I'm gonna change this to get rid of those curly braces, and save that.

And then here, instead of saying, export const Pet = blah, I'm gonna say export default function blah like that. And let's give this a name like so.
Now why do I do that? It's just kind of a pattern that I had that the default export for components is always the component.

I would say it's a decently common pattern, but I'll leave you to judge it for yourself.
As far as changing it to a named component, this is useful for when you're debugging things. Because if there's a stack trace, you'll see pet has the error, which makes that a little bit easier to debug later.

So now, we have two different files, right? We're importing pet from pet. This should still work the way it should. It does. But now they're a little bit better organized now that we have an app component and a pet component, and they're in separate files and we can maintain them separately.

There's another commit point here, that if you've fallen behind, you can go ahead and come up to I think this commit. Let's just take a look and see what it's called. It's right there.
So this one is the add Parcel, build process and extract out Pet components so this is the one that you'd want to move up to right now.

Okay and so we used Parcel. I told you could use Webpack this would 100% work with Webpack as well. You could also use Browserify, which is another great project for bundling code. It still works really well despite what other people might say. It's a bit older, but it still works great.

Or you could use Rollup as well. Roll up is a bit more unwieldy sometimes a little bit harder to use, but works well, as well. At this point, now we've introduced a package.json so if you're moving forward and commit points in the course, make sure you move forward in the commit, and then you run npm install afterwards, right?

So if I come to my terminal here, not this one, this one. And I say, if I moved forward in the commit, I would have to say, npm install, just like that. And it's gonna go run and install everything off of the npm registry. You don't have to do this if you've been following along, but just so you know, make sure that you're always keeping up with the npm installs as well.

Otherwise, things won't work.

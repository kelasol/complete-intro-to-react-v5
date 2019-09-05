# Dev Tools

## Environment Variables & Strict Mode

There's a couple things that I wanna call out here. One of the big things is when you're compiling your code, it's really important that you set the `NODE_ENV`.. Now, the good news for you is if you're using Parcel, Parcel just takes care of this. So when you're in development mode, it'll keep it in `NODE_ENV=development`.

And then when you do a Parcel build `index.html`, it'll set that to production. With Web pack and browser file, you need to be a little more explicit.

So the reason why you do this is when you're in development mode, it'll give you more descriptive errors. It'll kind of help you along the way.

It'll prevent you from doing bad things. And then, when you put it in production mode, it cuts out as much code as you want or as it can. So it drops all of the debugging code, which makes it smaller and faster. But you don't get the useful error messages.

**You don't get source maps. You don't get a bunch of the stuff that helps you write code. So it's just key to make sure that both of those things are set in the appropriate environments.**

Slack, famously messed this up, that they were shipping the development environment for a long time.

_So it's worth keeping an eye on cuz it's four times larger and 40 times slower if you use the development environment._

Okay, strict mode, there's a thing that you can wrap entire application in `React.Stric`t. And what this will do for you is it'll help you future proof your application.

So React has some things that they're trying to deprecate. And if you do `React.Strict`, it won't allow you to use them anymore. Whereas if you don't have React in strict mode, it'll let you use these things that they're going to shortly deprecate. And the cool thing is it's a component, so you can make part of your application in strict mode and part of it not in strict mode.

So if you have a new part of your application, you can put that in strict mode. And if you have an old part that does use the old part of React, you can still have that not in strict mode. So just to show you how to do that.

In fact, we can just do it really quick and leave it in wrap. Go to wrap.JS, and just here you can say React.StrictMode. I guess I got that wrong in my notes. So yeah, React.StrictMode like that.

_React.StrictMode doesn't render anything, it doesn't add any page weight or anything like that, so this is totally fine to ship this to production_.

_In production, this will just do nothing, the strict mode part of it. But now, if we try and do anything like use any of the unstable APIs or something like that, it'll give you additional warnings about things that you don't want to do_. So we're teaching you all the latest in JavaScript.

**So we won't trigger any of these warnings. But if you're in legacy applications, this can be helpful.**

## React Browser Dev Tools

Last thing I wanna talk about here is dev tools, which are absolutely essential.
So I would just invite you to google React dev tools and then just put Chrome or Firefox. I'm on Firefox, obviously, so.
Here it says **React Dev Tools**, and I'm sure there's one for, Google Chrome's right there anyway.

So you just come in here and you say I already have them, you can see them right up here for me, right? But Chrome as well, you just click that, and you'll install that on Chrome.
I think these are the only two that exist right now.

Edge doesn't have them, and Safari, I think they got rid of them. So you either have to be on Firefox or Chrome to have them. The new Edge will have it, the Edgium, as it were. Okay, and let me show you a little bit how to use this.

So this is a React application. You can see up there that it has React in developer mode because it's in red.

And then I can open my dev tools here, and I have a new React tab right there. So I'll click on that,
_And now I have a DOM explorer, and I can explore as if I was exploring a DOM tree_, right?

So you can see StrictMode there, an app, then I can see my searchParams thing and I can highlight it, right? And it will show me that component on the page. Inside of that I can see the drop downs. And what's cool is here, do I have anything passing params around?

I don't really. _But you can see here, you can see some of the props here. I can see all the children that it has, it's a useful kind of DOM explorer for a React application_, right? Let's say I have a big application I need to find drop down, so I can just type in here, drop down, and it'll actually search for drop down there, which is useful as well.

I can click this thing right here, and I can figure out where this is coming from, so I can find this input and click on that. And it's like, okay, this is the input you're looking for. I can see the properties that it's getting, the change handler, the placeholder value, and so on and so forth.

Something else cool you can do, let's say I'm just on the page here and I want to find this Submit button right here. So you can right-click on it, say Inspect Element, just like you normally would, right? This will take you to the inspector, but if I click on the React dev tools, it will still be highlighted, right?

And then last thing here, I can actually go into the console, and if I wanna mess around with it, I can put `$R`, **and whatever is selected in the React dev tools will be \$R inside of my console. So I can programmatically manipulate it there as well**.

And just so you know, you can actually do that with the inspector as well.

So if I click on that and I put `$0`, you can do that with just the normal inspector as well. And I think you can do \$1, that might be a Chrome-only thing, but that'll grab the previous thing that you have grabbed, right? So the dev tools are very very helpful in doing React applications, something you wanna have installed for sure.

> > Speaker 2: If we're voting the production version of the site, I get a warning when I click on the icon for the tools, warning that we're using the production belt or the development belt. Is that the development belt of the tools or development belt of React?
> > Where are you seeing that?

> > Speaker 2: In your extensions, clicking on that.
> > Right, so what's it? If I go to Netflix.com,
> > This homepage is built using the production build of React, right? So it's just letting you know hey, you're in development mode, you should not be shipping this to production. It's okay to have in your developing environment, as you should, but this is what you should see when you go into production.

> > Speaker 2: Isn't Parcel transpiling and munifying everything, and then what we're rendering here, what we have opened is the production version or no?
> > It's still the development version, which is what you want, right? Cuz if I didn't have the development environment, then I wouldn't get all the useful error messages that React has for you.

It would just say an error happened, and good luck, right?

Instead of saying this broke at this line in this way.

> > Speaker 2: Okay, thank you. So even though we're running it out of the dist folder, it's not production.
> > Right.
> > Speaker 2: Okay.
> > Yeah, I'll show you how to build it for production later.

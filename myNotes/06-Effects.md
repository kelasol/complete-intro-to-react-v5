# Effects

## Effects

_So what we're gonna start doing here, is we're actually gonna to start reading live data from an API_.
Which is gonna be exciting, so we're gonna see pets to adopt her. And so this is gonna actually come from Petfinder which is like one of the easiest ways to find pets to adopt.

### So I'm gonna show you now how to handle asynchronous code inside of React.

Okay, so what I want you to do first, again I mentioned earlier that while you can put in different locations up here, I actually have, at least temporarily, limited this to Seattle, WA, and San Francisco, CA. Reason being is that we have one developer key and we don't wanna hammer their API, so that's why we're kind of limiting ourselves to just a couple of geographical areas.

This might change in the future, if we can figure out better ways of doing this. But just to be on the safe side right now, that's what we're gonna do. Okay, so let's go ahead and start using some data here. So inside of `App.js`, sorry, this isn't `App.js`, this is inside of SearchParams.js.

We've already got an animals here, but we're also going to get the pet client up here.
And underneath all these use dropdowns, and things like that, we're gonna use another thing from React here called `useEffect`.

### useEffect takes place of several lifecycle hooks

Now, if you're familiar with React, already, **`useEffect` is gonna take the place of several of the lifecycle hooks**, right?

So, it's gonna take the place of `componentDidMount`, `componentWillUnmount`, and `componentDidUpdate`. So if you don't know what those are, then that's fine, you can learn these for the first time. But if you're coming in with some familiarity, that's what this is gonna replace. So here I'm gonna say `useEffect`, and then I'm gonna give it a function.

And then here I'm gonna say `pet.breeds`,
dog. This is gonna return a promise. You can actually see that it returns a promise.
That returns a breeds response. And then here, just for now so we can see what it's doing, I'm gonna say console.log and console.error.

And what this is saying, if the call is successful then log output whatever the response is, and if it's not successful, then send it to console.error.

So what's happening here? So `useEffect` is disconnected from when the render is happening. So what this is actually doing is this is scheduling this function to run after the render happens.

So what's gonna happen is it's going to render the first time, it's going to schedule use effect to run, but then it's going to render first. So all of this stuff gets rendered first before anything happens inside of `useEffect`. Good so far? All right, so this does not happen immediately.

As soon as this happens, as soon as searchParams renders for the very first time, t's then going to run this effect, okay? And it's not synchronized its not like this happens and then immediately this happens, it happens and then soon thereafter this effect will run. Now, why do you wanna do this?

Well, you want to do this because you don't wanna slow down that first render, right? You wanna show your users something immediately. You don't want them to have to wait to see something, you don't want them to wait for some sort of Ajax request to come back. You want to immediately show something and then go to the API and try and request data.

So that's why we're doing this. So let's go take a look what that actually looks like. If you go over here into your petinder you should see here this object breeds, breeds, and then you should see it comes back right now with 257 breeds. So if I look at one of these you can see Husky, Icelandic sheepdog.

I didn't even know that was a breed, but apparently it is, right? And so it comes back with all these things back from the API. And if you look at your network tab you'll see that this is just JSX, XHR. This is going to the pet devs dev-apis, and it is getting that back from the API.

Which is great, right? Now we're getting all this information back from the API, so now we can actually setBreeds to be all of these various different kinds of breeds of dogs.
So what we're gonna do instead of `useEffect`, we'll just replace this and say,
The first thing we wanna do is, whenever this run through we want to update breeds, to be empty array.

Because if we're requesting new breeds and there's already breeds in that, then we want to clear them out. We're gonna update the breed.

To be an empty string. This `useEffect`, it's gonna get run whenever we're changing sets of breeds, right? So if I go from like cats to dog, I need to get a new set of breeds, right?

So the first thing I'm gonna do is I'm gonna clear out whatever breeds were in there. So if there's husky and poodle, I'm gonna clear all that stuff out of there. And if I've selected Bichon Frise or something like that, then I need to set that to be empty string, as well, because I can't have a Bichon Frise cat.

So once that's done, then I'm gonna say, pet.breeds, which is that function that's gonna retrieve that from the API. I'm gonna parse in whatever animal is right there, so animal

And then I'm gonna say `.then`,
And that's gonna give us something back from their API, and I know inside of that object it's gonna have breeds.

Okay?
So we're just structuring out this breed cuz I know that's gonna come back from the API. And then I'm gonna say, if you look at these objects, if we go back here to our console, notice that they are objects, right? So name, Fox Terrier, links, something else, right?

We actually just want the names. We want to throw away all those links, we just want the names. So we have a list of objects that we wanna transform into a list of strings. So how do we do that? Map.

So what we're gonna do is, we're gonna say `const, breedstrings = breeds.map`, and we're gonna turn,

Name into name.
And then here, we're gonna say setBreeds to be breedStrings.
So what's going on with this? Well, we just structured out the name, right? So we grab poodle out of that and then we would just return to poodle, right? You also could have had to spend like breed, object, and then be breedObj.name, right?

Same thing. I just think this is a little bit more elegant.

Okay, and just in case there's an error from the API, you just put console.error there. So it'll just feed whatever the error is into console.error.
This would be the same as doing like error, console.error error, right?

Same thing.

Okay.
Yeah, I have these as set, rather not update
So change this to be set, not that.

## Declaring Effect Dependencies

Getting closer. We have one problem here, that setBreed's not defined. So what we're gonna do is, if you remember, we did pass that here and use drop down at the end, the setState function, right? So we're just gonna grab that too. So setBreed, and now that'll be defined, right, cuz that's coming from the use drop down.

Not using breed yet, that's okay, but the thing that we're getting here is hey, just so you know, it contains a call to to setBreeds without a list of dependencies. This can lead to an infinite chain of updates. So the problem here is with `useEffect`, you have to declare your dependencies, which is kind of an odd phrasing this, but stick with me for just a second.

`useEffect` is going to run, as of right now, after every single time that render gets called, which is too frequently, right? So right now, every time I typed into location here, it would request a new set of breeds. That's obviously incorrect, it's not what we wanna do, right?

We only wanna request breeds when animal updates, as well as on the first time.

So what you can do here with `useEffect`,
Rather than have this run after every single render, we can say only run when these things change. So what you do is you declare the things that it depends on.

So here it depends on what? It depends on animal, right? Cuz if that changes then we need to change it. So we'll put animal there,

But it also technically depends on setBreed and setBreeds. Now, you and I both know that that's never gonna change, but,
ESLint demands that they still be there because it still technically depends on them.

So setBreeds as well.

It doesn't matter what order these come in, it's just a list of dependencies that React will check. Cuz if any one of these things changed, rerun this effect after it renders, otherwise, don't run it again, right? So now if location changes, because location's not in here, it's not gonna rerun this effect.

So let's go make sure this actually works. If I refresh this,
Now, notice that breed is no longer grayed out. If I click on here, you can see that it actually has a lot of new dogs in it, right? And notice that if I start typing in here it doesn't request new breeds.

However, if I changed the dog to be cat, notice that it's gonna gray out here for just a second.

That was very fast, but now notice here that it has American bobtail, and Calico, and Cornish Rex, and things like that. Same thing with small furry. I guess you can adopt a skunk.

## Effect Lifecycle Walkthrough

> > Brian Holt: Let's work through this whole cycle. I recognize that I have introduced a lot of steps here. So let's work through the entire cycle of beginning to end of what happens here, okay? First thing, I have search params here, right? So this gets rendered for the first time.

It gets all this information, sets all these hooks up so the first location is Seattle, Washington. Breed is gonna be an empty array and animal is going to be a dog, and breed is going to be an empty string, right?

> > Brian Holt: It's then going to schedule this `useEffect`, but this is not actually gonna happen yet, right?

This does not run on the first render, okay? Then it's going to return all of this markup,

> > Brian Holt: Right? Then its going to finish that, it's going to render that all to the DOM so the user's going to see all of this first, okay? Then after that, it's going to run the schedule effect.

Keep in mind you can have ten effects in here, right? Right now we just have one effect, but you can have many effects in here. So after the first render, it's going to call this function right here.

> > Brian Holt: So this is going to separates to be empty array.

It's gonna cause separate to be an empty string.

> > Brian Holt: And then, it's gonna go out to the API,
> > Brian Holt: With animal, and it's going to get breeds back from the API, and then it's gonna call setBreeds. But keep in mind, this is gonna take some time, right? This will take a second or something like that, right?

So what's gonna happen is it's going to render, and then a second later once this comes back with the breed strings from the API, it's gonna cause another re-render, right? But, the only thing that's changed here is breeds. Does this particular effect depend on breeds? No, right? So it doesn't re-render the next time, right?

Because breeds changed, but animal, setBreed, and setBreeds, none of these changed, right? So it just runs that effect once and then it's done, okay? So now, fathom for a second that go and I type in the location, right? So now location is updated state. And it goes here to `useEffect` and it says hey, has animal setBreed or setBreeds changed since last time I ran this effect?

No, right? So it does not schedule this effect to run again, good so far? Okay, then I go in and I select animal to be, it was dog and now it's cat. So it's gonna re-render but it says, hey, did animal change, it did, right? I changed it from dog to cat.

So it's gonna set immediately set breeds to be empty array, and empty string is going to then call the API, get the new breeds back and it's gonna re-render again after that.

> > Brian Holt: That makes sense?
> > Brian Holt: So this is how useState and `useEffect`s work together to kind of manage these kind of state updates.

> > Speaker 2: So for the dependency array that determines if `useEffect` is run, that functions run. When we put in setBreed and setBreeds, we're just saying basically if those were reassigned and then it would rerun it.
> > Brian Holt: That's funny that you bring this up. I had an at-length discussion with a couple of the React core team members of I think that's silly, because that's never gonna change.

And they basically said, we don't care, do it anyway. I would think this is better because this is more clear about your intention, right? Only at run when animal runs. But you're gonna get an error of,

> > Brian Holt: SetBreed needs to be in there. So I gave up, this is what the community's doing, so I'm teaching you what the community's doing.

I mean, in theory, it's not a bad idea, right? I guess in theory it could be updated or something like that, but whatever, I don't know.

> > Speaker 3: So it's just looking for any external variable that you're using in that function?
> > Brian Holt: Right, so the idea here being that I have setBreed, right?

And if I'm using setBreed because it's defined in here inside of this function itself, that means if any time this setBreed does change, it should re-run the effect. Which is true of Animal, right? I'm using Animal here, so any time that Animal changes, I need to re-run the effect.

So that's what they're chasing after, this will save you bugs, right? Because if I didn't have Animal in here, actually this would be a good thing to show you. So if I take Animal out of here, it will request it the first time, and I'm gonna get Australian shepherd, right?

But if I change this to be cat now, it's not gonna update. Right, because it's not gonna go back to the API because it thinks like, I'm good, right, I don't have to change, because, I don't depend on animal.

## Run Only Once

Now, I wanna show you a couple more things about this. What happens if I want this to run when it mounts, so when it first renders and then Never again?
Well, you just given an empty array. This is an array of its dependencies and it's saying, I depend on nothing, right?

So then it's gonna run once, and then this will never update again.
Right? So if you want it run once on what it first creates that's how you do that. This will be useful for things like if you need to integrate with a J query plug in.

Like when I'm sorry that's happening to you and, or like D3, that's maybe a better example, right? If you have to integrate with D3 and you need to set up all that stuff, right? This is where you would do it.

And then you could give it an empty array, it's like, okay, once this is integrated then don't update this anymore, right?

And then if you want it to run every single time something updates, get rid of that. So now, if I come over here,

It should,
What is going on here? There we go.
Yeah, I mean you can see here I've created an infinite loop, you can see that I have,

In fact I'm gonna stop that so I don't crush my API.
So don't do that please. Cuz I'm paying that bill. [LAUGH] So what what was happening there is like it's running every time something updates, right? Which means that every time that I call separates, it's causing an update, right?

Which means that it caught it's scheduled that effect again. Which is then going to update their breeds again, which is gonna schedule another effect, right? Sick of this infinite loop. So that's why actually they enforce this,

Dependencies thing, so you don't get yourself into these situations, right?

Because if it depends on animal then you should depend on animal being there and via vice-versa, you don't want to cause these infinite loops of update, and then that schedule in another effect.

## Hooks Review and Q&A

> > Speaker 1: So why is breeds not a dependency?
> > Brian Holt: So breeds, as in this breeds right here.
> > Brian Holt: Is not a dependency. I guess this is kind of misnamed right here, breeds right there. We could call this breeds, like API breeds or something like that
> > Brian Holt: There we go.

So that could've been confusing to you before. It doesn't depend on breeds because this breeds is not used anywhere inside of this `useEffect` right here. It's not read from anywhere inside of this effect, right? Now set breeds is, right? So that's why this is in here. But API, I just want you to keep in mind this breeds and that breeds are separate.

They're different things, right? So this is never used inside of use effect so therefore it's not dependent on.

> > Brian Holt: Yeah?
> > Speaker 1: Was there any problem with component did not amount those life cycle methods? Why did hooks get created?
> > Brian Holt: Well, okay.
> > Speaker 1: [COUGH]
> > Brian Holt: There's a belief that hooks are simpler than having to learn the life cycle of components and having to understand like context and some other things like that.

And you can notice I'm being non-committal with my language. It's because I have my doubts about which of these APIs is gonna be for the better, and like maybe we'll address that a bit later when we talk about class components. That's probably the better so that everyone can kind of get on the same page here.

But the short answer to that is people think that this is easier, and then I'll teach you both, and you can be the judge of which one you want to use. But no, there's no there's no inherent problem with class components.

> > Brian Holt: There's no limitations. Actually, class components can do more than hooks can.

> > Speaker 1: Currently
> > Brian Holt: Currently. They have plans to fix the gaps, but as of right now there's still some things that hooks can't do. So one more thing we should call it that we did here. So if I go and select like American Eskimo dog and then switch to Cat, notice it very quickly switches that back to be the default option, right?

That's something that we did here with this empty string.

> > Brian Holt: Normally it's just kind of understood, but I just wanna call out the fact that as soon as I call setBreed here to be empty string, because of the way of the reactive stretch and the way that we're thinking about this.

As soon as this is set, this is synced to this animal drop down down here. Or rather the breed drop down, that as soon as I send that to empty string, it immediately updates breed right here, right? So those are connected together, we've clung that together. So now it's really cool as long as we're making sure that we're calling setBreed in the right places, that it cascades that effect down to all the places that are depending on that information, right?

So that's the power of hooks and stuff like that is as long as you're playing by the React rules you get this propagation state for free. So I wanna tell you that useAffect and useState are the two primary hooks that you're gonna use. That's gonna cover about 90% of your use cases.

So useState obviously the most common use effect also being quite common, and then maybe like useRef occasionally, and then there's a long tail of other hooks that you may never have to know. So we'll definitely still talk about them, we'll get into an intermediate React. I think we'll still talk about Ref in here, but that'll be it for the React life cycle of the React host and things like that.

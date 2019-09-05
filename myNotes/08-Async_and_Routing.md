# Async & Routing

## Asynchronous API Requests

We have all the search facets that we need to be able to search for pets, but we're not actually using that to hit the API yet, right?

So what we wanna do is we wanna add the ability that we can go and hit the API and get pets back so we can display them. So we're gonna add another useState here, we're gonna say contst `[pets, setPets] = useState`, and it's gonna be an empty array, all right?

Because when you first request things from the API, there's gonna be no pets there.

Okay, here above the useEffect, we're gonna make an async function, so async function requestPets.

```javascript
asycn function requestPets() {
    const { animals } = await pet.animals({
        location,
        breed,
        type: animal
    })

    setPets(animals || []);
}
```

What we're gonna do is we're gonna say, const { animals }, which we're gonna destructure, right? Cuz we know it's gonna be called animals, and we're gonna say, = await pet.animals.

### Using Async functions

And we're gonna send the location, the breed, and the type, which is gonna be the animal.
All right, so a couple of things to unpack here, this may be your first time using an async function. **So an async function is a function that is guaranteed to return a promis**e, right?

**So anything that's an async function always returns a promise**. Even though I'm not doing anything here, **this returns a promise that will resolve whenever this function completes**. Now I'm just ignoring it, but that's beside the point. So that's what an async function does, _but the superpower that you can decide of async functions is that I get this `await` keyword_.

So `pet.animals` returns a promise itself, right? And I'm just saying, hey, wait here in this function until this completes and then give me back the data. So I could say pet.animals.then and then do all that stuff inside of there, but here I'm just saying wait for this to finish and give me back the data.

So it makes this asynchronous code of go to here, wait, go to here, wait, go to here, wait, and then finish, right? So I'm a big fan of `async` `await`, this just makes this code look really, really nice. So now I have animals, I'm guaranteed that animals will be done by the time I get down here and I can just say setPets with the animals.

Or if it comes back with nothing from the API, just set it to continue to be an empty array, all right? If I request something and no animals come back, _set it to be an empty array, and that's what this or operator is gonna do for us_. Either it's gonna be whatever is in animals or it's going to be an empty array.

Pretty cool, right? I think it's pretty cool.
So now what I can do is I can go down to the form.
So this form that we put in here, and I can say `onsubmit =`, and I need to do two things here inside of this function.

The first thing is I don't want it to actually submit a form, right, like an HTML form. So I'm gonna say `e.preventDefault`, which you all have probably done at one point in your JavaScript career or not. If not, then God bless you, you've missed a really dark time.

But this will prevent it from submitting a HTML post form. And then all we're gonna do here is we're gonna say `requestPets`.
So if we try to transpile this right now, right now, by default, Parcel is making this work for Internet Explorer 11.

### Only Modern Browswer can supoport async..await

As a representative of Microsoft, I'm sorry [LAUGH]
we don't need that, right? This is just a demo application that you and I are working on for fun, so we can just target modern browsers, right? We're okay to target the last two versions of Firefox and Chrome and call it good.

Obviously, you need to cater this to your audience, right? So make sure you're looking at your analytics to figure out this should work for 99% of my users or something like that. But for us, we're just gonna say make it work for the latest browsers and that's it.

So actually here inside of my notes, I have a really good list for you to hit all the latest browsers. So go ahead and just copy that right there, or you can type it out, but it's a lot.

So again, this is in the Handling Async. So Handling Async right there, number nine, down here, this browser's lists thing.

Okay, and then I'm gonna put this inside of my package.json. You can put it really anywhere, but here, underneath dependencies is good.
And so all this is is this is an array of various kinds of browsers that I want, Babel and PostCSS, which are both running behind the scenes inside of Parcel, compile my code to work for these browsers.

And Parcel already knows to look here, which is cool.

So let's look at the last two Chrome versions, Chrome, Android, Firefox. These are all of the, quote-unquote, alive, evergreen browsers. Now, the reason I wanted to do this is because only very, very modern browsers support async await.

Otherwise, it's going to transform this into something called a generator, which we just don't even wanna deal with, believe me.

## Using the Fallback Mock API

So you can actually do this entire workshop totally offline, which is useful to you as well. Whether that's maybe sometimes our IT guy might have an issue or you're just not in a place where have internet access. In that case, we've actually made it so the API client works 100% offline.

So I'm going to show you how to make that work really quickly. The first thing that you're gonna wanna run is this command right here, `npm install-D cross-env`. _This is to make sure that environmental variables were consistently across Linux, and Mac, and Window, so go ahead and do that_.

Go to your command line. Go to your projects, which we called ours adopt me, and do npm install-D cross-env.

Okay, once you have that tool installed, then I want you to put this inside of your package.json. `"dev:mock": cross-env PET_MOCK=mock`. This is the signal for the API to go ahead and use the mock data.

And then do npm run dev. And this will just do the same command but it'll run it in a different environment. And that's all that's going to do for you. So I'm just going to copy and paste this

Into my `package.json`. So I actually have it already here but I'll just show you this is where it is.

And I'll just put that in there.

Now, if I say `npm run dev:mock`, everything will work exactly the same.
Except all the data will be mocked, which means it will never hit the API. So if I go here to this, refresh the page, and there you can see I have nonsensical data, right?

Now, this is just returning to you random data. The good news is that it is deterministic in the sense that if I go to, notice that this second one here is called Jewelery. And if I go to Cat, it will give me a different set of breeds. But if I go back to dog,

It gives me the same set of data as well, so it's dependably the same list of random things. So if you had the same problem that I did, which is that it wasn't building in a mock mode, just do remove, or rather, what you want to do is you just want to delete the cache and dist directories because sometimes parsel gets in a strange state.

So if you just highlight those two and say delete, and then rerun dev: mock, everything should build correctly.

## One-Way Data Flow

So what's really good about this now is we have pets up here, right? And this represents a set of pets that we've gotten back from the API. Now, I'm gonna create another component here.
You can get rid of that console log.
Underneath the form here, we're gonna create something called Results, and we're just gonna pass in pets, so pets = {pets}.

`import Results from './Results';`

And then up here, at the top, we're gonna say, import results from './Results'. Again, we haven't created this yet, but we're about to. So, line 3, whoops,
import results from './Results'. So we put that in.
And then down here, we put `<Results> pets={pets} />`, there on line 54.

And we're about to go create this new file,

And start displaying our pets in a useful way.
Okay, save that. New file called results.js. Gonna import react from 'React'. Import Pet from './Pet'. If you remember, one the very first things we did in the course was create the Pet component, we're gonna reuse that.

And here, I'm gonna say, const Results = ({ pets )},

Whops double arrow. Then we're going to return.
And here we're just gonna do a bit of markup. So, we're gonna say div className="search".
And we're gonna say, if pets.length === 0, and we're gonna use the ternary.

So if it has no length, which means no results have come back from the API yet, what we're going to return is an h1 that says, No Pets Found. Okay, otherwise we're going to return something that displays all the pets, right? So we're gonna say, pets.map, and we're gonna take in a pet and we're going to make a Pet component out of it.

```javascript
// Results.js
import React from "react";
import Pet from "./Pet";

const Results = ({ pets }) => {
    return (
        <div className="search">
            {pets.length === 0 ? (
                <h1>No Pets Found</h1>
            ) : (
                pets.map(pet => {
                    <Pet
                        animal={pet.type}
                        key={pet.id}
                        name={pet.name}
                        breed={pet.breeds.primary}
                        media={pet.photos}
                        location={`${pet.contact.address.city}, ${pet.contact.address.state
                        }`}
                        id={pet.id}
                    />
                })
            )}
    )
}

```

So we need to do animal ={pet.type}. And again, remember, these are coming from the API.
Sorry, rather, you have to make a Pet component, Pet.
And inside of here I'm gonna say animal,
={pet.type}.
I'm gonna say, key={pet.id}.
name={pet.name}.
breed={pet.breeds.primary}.
media={pet.photos}.

location=, I'm gonna use template strings, so the backticks there, right?
And we're gonna say ${pet.contact.address.city}, ${pet.contact.address.state}. And then lastly, we need the ID, which will be equal to {pet.id}.
Okay, so that'll do that. Again, this is a map, so this is going to return, for every pet that I get back from the API, it will give back one Pet component.

And if it can't find anything, then it'll just say, No Pets Found. Now, it would be good to make this more sophisticated, right? It would be better if this had a nice loading indicator and things like that. That's not something we're gonna do today, but there's obviously better UX that you could do about this.

So again, remember we're getting pets here, this is coming from the parent, right? S we search for the pets in the parent, and then we pass that down into the child component, right? This is a key pattern in React.** It's a key pattern React because you have data flowing from parent to child, child to its child and child to its child**, right?

### One way data flow

**So it's this data that flows down. But notice it doesn't flow up, right? This is called one-way data flow**. This is really, really useful, because if I have a problem with search params, I know that problem is not arising from any of its child components, right? So it's not arising from Result, it's not arising from Pet, because while the parent can affect the child, the child cannot affect its parent.

It doesn't even know who its parent is.

Again, this feels limiting in some fashions, but in the end it actually ends up being extremely useful. Because if I have any bugs, I know where to start. And that's super helpful.
Now I say that it only flows one way and it can only possibly flow for some way, there actually are some ways to reverse that flow.

And it's intentionally difficult, because most of the time you should not and do not need to. It's actually really only useful for library authors, right? So someone like React Router or something like. For the most part, that's not a pattern that you should be adopting.

But in intermediate React, I'll show you how.

Last thing down here, make sure you do, `export default Results`. Save that.

> And then you should be able to come back over here. You might have some sort of error, just refresh the page, it probably will go away from Parcel.
> Okay, so, I'm just gonna hit Submit.

> And you can see here, now I'm getting real results back from the API. So we have Fatboy Slim and Cindy and Holly.

> And looks like these are mostly dogs.
> But you should be able to find cats as well. That's cuz it is only searching for dogs

> But we're able there to switch to cats, right? And now these are cats to adopt as well.

## Reformatting the Pet Component

```javascript
//Pet.js
import React from "react";
export default function Pet({ name, animal, breed, media, location, id }) {
  let hero = "http://placecordgi.com/300/300";
  if (media.length) {
    hero = media[0].small;
  }

  return (
    <a href={`/details/${id}`} className="pet">
      <div className="image-container">
        <img src={hero} alt={name} />
      </div>
      <div className="info">
        <h1> {name} </h1>
        <h2>{`${animal} - ${breed} - ${location}`}</h2>
      </div>
    </a>
  );
}
```

So right now, we have this pet component, it's pretty much empty. I deleted all the content inside of it so you and I are gonna rewrite this a little bit so it looks a little bit nicer. So this is the pet component's gonna show in the search results page, which is gonna be used here in the results component.

So at name, animal, breed, and do media, location, and id. We'll pull those out of the props, so they're gonna be passed down. First thing we wanna have is a placeholder image just in case, cuz some of these animals don't actually have

Images. So we're going to use place corgi which is my favorite place to grab placeholder images, and we'll grab a 300 by 300 pixel image, and then we'll say if(media.length).

So if media, which is the photos coming in here, has any length to it, and we'll say, yeah. If media.length, then we'll say hero = media, 0 is the first image in here and the small image inside of it. So that'll give us either the first image that we can find or look at the place corgi.

And then here, we're going to return, a href, so this is going to be a link to the details page, which will I think will be the next thing that we'll code up together. So /details/\$ {id} and className="pet". Inside of that, we'll put a div with className="image-container".

And inside of that, an image where the source is equal to hero and the alt is equal to the name of the pet.

Okay, beneath that we'll have div className="info".
And inside of that, we'll have an h1 with a name.
And h2, and here I'm gonna use a template string. You also can do this without template strings. It's kinda up to you, I found this easier to do with template strings.

So we're gonna put animal
And then dash and then breed
Then a dash and location, okay?
So a lot of React program looks like this, where it's just constructing markup, right? A lot of just front end development in general kinda looks like this. But now, if we go back over and look at our pet component, this should look a lot more pleasant.

> Let's go take a look at the Adopt Me. We'll search for something, and you can see here, > we're getting back all sorts of pets.

> And you can see here that these corgi ones, these are the ones that don't have images.
> So go ahead and jump up to the commit here.

> If you're behind, this commit was,

> This one here, async calls to Petfinder API, update Pet component. So if you can jump forward to that commit, you'll be caught up with me.

## Reach Router

So Reach Router, there's there's two major routers for React. And actually now there's probably three there's another one called NaVi that just came out that I don't really know too much about. I just know that it's up and coming and people like it. But historically there's been **React router** and **Reach router**, which are authored by similar people, Ryan Florence wrote.

Reach router and he also helps with React router as well. So we're gonna use Reach router today. I'm a big fan of **Reach router because it's very accessibility focused, right? So if you have like a page change it'll focus on the right page, and managing focus is a really difficult thing**.

And if you don't know that it's a difficult thing that means you need to work harder on accessibility probably, because it is difficult and it's also worthwhile, something you should be doing. So React router, it's not that it's bad at accessibility, it's not, but it just makes you handle a lot of accessibility things.

_Reach router handles much of that for you and they're smart about it, so it's a good project to look at_.

And that being said, they work relatively similar they're both great projects. If you're very interested in learning React router version three of this course, use this React router.

It's still totally valid, they're still on the same major version. So yeah, go ahead and check out version three if you wanna learn about React router.

### Single Page Applications

So now, what we wanna do is, we wanna add a second page, a details page, right? So we're gonna have a single page application.

Now, just a second to talk about single page applications, not every app needs to be a single page application. It's okay to have multiple different pages that load different things, right? So I'm just gonna show how to do this, so this is another tool in your toolbox. But don't feel like you always have to have a single page application, right?

I think a good example of that is the Frontend Masters website, right? It's not a single page application and they did it really well.

But something like Netflix is a single page application and that makes sense, right? It's a very app like feel.
Okay, so what I want you to do is I want you to go back to your code editor here and I want you to create a new file and call this details.js.

### Creating Details.js

```javascript
import React from "react";
import { render } from "react-dom";
import { Router } from "@reach/router";
import SearchParams from "./SearchParams";

const Details = () => {
  return <h1> hi lol </h1>;
};

export default Details;
```

Okay, instead of `details.js` we're gonna say import React from react. You're probably sick of writing that now.
And you'll say const Details equals arrows function, and for now we're just gonna return something dumb.
Just something like that. And then we'll say export default Details.
Well, obviously we're gonna fix this later, this is not what this is gonna end up looking like, but yeah.

Now, at this point we need to go install Reach router. I'm just gonna let parcel do it for me, cuz I have parcel running right here in the command line.
So at the top here in app.js, I'm gonna say import Router like that with curly braces around it from @reach/router, like that.

`import { Router } from "@reach/router";`

And again remember, that parcel if I do this and you can watch it down here let's install that for me

But if not you then you have to go do npm install reach router.
Okay, looks like it's rebuilding. So now, I wanna do instead of just always rendering search press which is what we're doing right now, right?

_I want to switch between rendering either the search page or the details page_, right? So what I'm gonna do here is I'm gonna put router.

I'm gonna put `SearchParams` inside of the router.
And then underneath that I'm gonna put Details. Now, notice I haven't I haven't imported `details` as well but with Visual Studio code it says hey, you're trying to use the `details` component and you have a file called `details`.

_I'm pretty sure you're trying to use the same thing here. So I'll just click this, and you'll notice up here that are important `details` up here for me, which is convenient right_? But again I have to do this line 5 there, import details from details like that.

And then you have to give them paths, so I'm gonna say path= /details/:id like that.

And I have to give `SearchParams` the path as well, I mean the path of /.

**So this is another way that React router differs from Reach router. React router will render everything that matches, whereas Reach router is only going to render the the thing that matches the most**.

Which is I realize a very subjective thing to say, because you can have two things that technically match the same thing. Like this, if I said, you don't have to follow with me here, I'm just gonna give you an example, some other route. And I said path = /details/1.

Let's talk about ID here for just a second. This is a variable (`<Details path="/details/:id" />`), right? **This is a very common way of doing variables with paths**, right? So if I put in, just ignore a 14 for a second. If I put in this, and I put in /details/15 into my URL, it's gonna pass that ID into that component, right?

So it'll match this, right? Does that make sense? Okay, now, if I have these two routes here, which of these routes is more specific?

Obviously some other route, like as a human, we look at that and that's very intuitive to us, right? But they've actually put like a scoring algorithm behind this that it'll choose the most specific route for you, and it's good, right?

So if I put in /detail/1, React router would render both of these, right? And Reach router will just render some other route, which I think is the intuitive behavior that we would expect, right? But that's how that works. Make sense? Okay, cool.

**So does the order of declaration here matter?**  
**It does not.**

> > Speaker 2: Okay.
> > Yeah. Good question, it does not. So with React router they use a thing called Switch. If you wanna do just one particular route in that one, it will do the first one it matches, right? So in that one it does matter, but this one it does a scoring system and then it picks the highest score at the end

Maybe I should probably be a little bit less bullish on that. It might matter at some point it might add like one point in their scoring algorithm, but in theory, I don't think it shouldn't matter. That was one of their claims to fame was scoring system in it.

Okay, cool so now we have a router. Something else that's worth mentioning about Reach router is you can have multiple routers on the page. So you can probably imagine I have like a main page and I use a router for that. But I could also have a contextual site now, right?

That like depending on which page amend the side nav changes as well. And you can also have a router over there that has different rules and different matching patterns. And those can work independently of each other as well. So it's quite flexible, it's a really powerful piece of technology.

And we are just gonna scratch the surface, I don't think it's gonna do very much more than this, right? We're gonna use this and links and that's about it from Reach router. So just so you know, this is not a course on Reach router, I'm just choosing one to show you.

Okay, so, now that I have that, let's go take a look at our page, again.
So I have this, notice that on the slash, the home page, it's going to the params page, but if I go to /details/1. Look what it says, hi lol, right? So this is working the way that we expect.

We can go backwards and forwards.

## Debugging & Reach Router Link

Now, what's cool here, if I go into details, I'm gonna show you just kinda a fun trick here. So we're gonna take in the props here. And I wanna see what's actually coming in from the props. One, probably just use the dev tools, cuz that's the easiest way to do it.

But I'm gonna show you another kind of fun trick that I did actually learn from Ryan Florence. So, I'm gonna say JSON.stringify(props, null, 4)...

```javascript
const Details = props => {
  return (
    <pre>
      <code> {JSON.stringify(props, null, 4)}</code>
    </pre>
  );
};
```

So, I used pre and code. So, pre as in preformatted and code and this is going to be code, right? And I put JSON stringify, so this is gonna take props and put it into like a nice pretty printed kinda way.

So now if I go in here and I go to /details/ something like that, right? Now this might be a little hard for you to see but I can see everything that's coming in from the routers. The routers actually giving a pretty substantial amount of information to you, right?

So, it's giving you the path, the ID, right? Notice the ID matches this ID up here, as in if I change it here, notice it will change down here as well. The URI and then a bunch of stuff location like but the port is the hash ,the state that's all coming in from the history package, if you're curious.

**So, if you do this, the pre formatted in code with JSON string if I would with obviously any object in here, this will give you a nice pretty printed view of the props. And this is also useful for doing with state as well, if you wanna see how state and props are changing over time**.

**It's just a nice little debugging technique to dump something out to the dom**. Largely I could also just go, if I just did _Inspect element and looked at the React devtools here_. I could see the exact same information. So here in Details, that same information is available on the right of my screen.

You don't need to read it, but just know that it's there. Also, look how many components reach their outputs in there, it's quite a lot. You'll see this a lot with libraries because they have to have multiple different layers to capture different parts of it, and that's pretty typical.

I don't write code like this where you separate it out into various different behaviors, like this one has like a location, location provider, right or implementation, focus handler, focus handled implementation. There's a lot going on here.

But you'll see that a lot in libraries, which is when this search functionality becomes useful.

So I can just search for details and I can find it.

### Naving back to homepage

So, let's make it so that when you click this Adopt Me that it will take you back to the home page, cuz most people expect that rise, so I want to show you how to use a link.

So we'll leave this like this for now and we'll fix it in just a second. We're gonna go back to app.js and we're going to wrap this h1 in a link. So I'm going to put link, and again I'm going to use the auto import here. Notice that imported that up here at reach router on line 3.

And I'll just close that. And I'm gonna say Link to =/, and then inside of that link, I'm gonna put this h1.

And actually let's go ahead and do it this way. Let's just,
Get rid of all the step around link, I'm gonna actually put this inside of the header.

Like that.
So all I did here is I deleted the h1 totally, and then I put header, and then inside of that I put a link. This link is ultimately gonna end up being an A tag, but the nice thing about using a link instead of A is that, reach-router will handle all of the various different routing mechanisms for you automatically.

I'm sorry. So just line 11 through 13, there.

Okay? So let's go take a look at this, so now you can see here that if I click on it, it'll take me back to the homepage, right?
All right, this is mostly what I wanted to show you about reach-router.

There's a couple other things that we'll kinda sprinkle in here for the rest of the course, but this is like the crux of it. The routers in and of itself doesn't have to be very complicated

So there's a commit point here. The commit that you wanna roll up to if you wanna get to this point is, github btholt complete v5, Commits.

We are at Add reach router, right? So we just did that one,

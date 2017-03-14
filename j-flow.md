# J-Flow
## A Bi-Directional Pattern for Program Flow
### Defining a mechanism for orchestrating the flow of data and events in modern applications.


All things flow in only one direction except asynchronous calls
Component chain flows from top to bottom or left to right
Data flows down
Events bubble up


## If There is Only 1 Direction, What Direction is It?

Forward, in a circlular pattern with occasional tangental rubber bands.

Since your program is not an open-ended cyclinder, how do we define direction in the first place?

In our context, the direction is defined by how each component type of the application stack communicates with other components, including components of the same time.  In typical the spaghetti code that runs, in essence, the world, components communicate with each other freely and without restriction.

That's great for global communication and sharing, but not so much for application architecture.

Within in the context of a single application, even a quite large and distributed application, we ultimately want to constrict and define our component communication channels.  This will reward us with a stable and predictable program, which should be the goal of every program's creator.

Ultimately, your program has an entry point.  You may *expect* it to always be the same, but in the real world it may not be.  A user should be able to return to where they left off, or jump into the middle of a populated dashboard by clickingo on a shared link for example.

Program flow begins with this entry point (discounting for now, your looping or listening server components).  Data starts migrating down the chain from the entry point (often this is a route you've defined) and trickles through some APIs, controllers, validators and hooks probably resulting in some form of presentation layer.  

This last and smallest presentation component is pretty much the end of the road for data flow, and the only things that ever flow up the chain are functions triggered by events.  Events of course, are usually initated by user actions although could be programmatically triggered using timers or when a listener is triggered by some external actor.


## So.. What You're Saying is?

To break it down succinctly..

Components shall:

  * Only send events to upstream components of one type
  * Only receive data from upstream components of one type
  * Handle their own asyncronous events tangentially to upstream and downstream flow
  * Regard a single source of truth at the top of the chain which represents the loaded application state
  * Be provided a universal source of truth for controlling application state and communicating amongst themselves within one complete, yet extensible, interface
  
Components should:

  * Alert downstream components to asynchronous process states which represent the loading or processing time as well as success or failure status upon completion.
  * Accept event callbacks and return either an error object or null and a result object that is at least set to true when they have received an incoming event or if within a promise chain, have both a method of resolution as well as rejection

A component may:

  * Engage in communication with components and services external to the application as long as the result of that communication is handled completely within the calling component and the result is then passed naturally back along the chain of uni-directional program flow.

Components shall not:

  * Communicate with components of the same type
  * Receive anything other than a boolean result flag from a downstream component


## Naming Conventions

  * **Actors**, **Classes**, **Messages**, **Prototypes**, and **Targets** shall be nouns or noun-adjective combinations
  * **Actions** and **API Methods** shall be verbs or noun-verb combinations
  * **Events** should be a combination of the action verb and the target noun it primarily operates on
  * **Properties** shall be nouns or adjectives
  
## Ontology Conventions

  * **Actors**
  * **Actions** are instigated by some actor (user clicks a button, script executes a CRUD operations) and are processed by API methods or event handlers
  * **API Methods** 
  * **Classes** 
  * **Events** occur as the result of some action and are received by a listening controller
  * **Messages** are passed between components
  * **Properties** are a sub-component of application state at any given moment
  * **Prototypes** 
  * **Targets**  are the parent nouns which hold events
  
  
## Types of Components

### Controllers

### Hooks

### Libraries

### Schemas

### Views

      Incoming events may change internal state and incur side-effects but outgoing events may not


## Methods of Inter-Component Communication

### Actions

### Events

### Listeners

### Messages


## State Management

/state machine/etc

### Application State

### Component State

### Changes in state must emit events

### Asynchronous processes must emit events


## Data Management





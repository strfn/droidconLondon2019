# Keynote build accessible apps
 https://medium.com/google-design/a-summer-designing-for-autism-5859f8096b0b

 Accessible technology, they are built with the purpose of support specific disability

 Assistive technology not purposily built for accessibility but happen to facilitate disability, for example roomba, self setting up tents, voice assistants. All not created with the main purpose of being accessible.

 Think outside of the screen.

# Jetpack compose
Existing UI framework is 10 years old and based on inheritance so a lot of duplicaiton of code. UI is scattered over fragment, activities, layout.xml, style.xml

Jetpack compose:
- is a library, unbandled form the android system and update lifecycle
- State onwnership and event flow is predefined
- NOT PRODUCTION READY
- based on @composable functions (the compiler will add extra paramters automatically to the function)
- @model annotation the enviroments knows that whe it's modified it needs to re-execute the lambda of the view where the model is used.
- state property is executed only once instead.

__IT IS EXTEMELY SIMILAR TO SWIFTUI__

challenges: 
- lack of string typing
- No reference to the view (in swiftui you do)
- Compatibility, not all the old UI SDK will be rewritten in compose.

Testability:

# Pushing Dynamic Features Your Users Want, As Quick As They Want Them

based on the Play.core library that allows to split the app in multiple packages.

Twitter created generic library that allows to install modules into the app.

## Lesson learned
- issues with android beta feature 
- gradle module issues 
- issues with KitKat, older devices, forced to deprecate KikKat in order to introduce the new functiolity
- Syncronization, the request to download the package goes into the play store queue and you don;t know what position you are in the queue

# Extra! Extra! Thread all about it!
Android VSync every 16ms 

Thread based on the concept of message queue. Threads have no visibility of each other

Looper check for new messages in the queue, handler takes cre of the delivery

All based on ThreadHandelr (name might be slightlty different, needs to update coe)

## Couritines 
same concepts but taken care by the compiler insrad of by the OS
Messaging between couritines is managed via __Channels__
which is just a queue.
By default channles have infinitive size, usually ok but might crash if queue bceomes too big.
Channels can be setup with different semantics
- block the sender if queue is full
- coalescence, only one message in the queue if new message arrives it replace the one in the queue
- block the sender till the receiver has consumes the message.

## Future
Android will not inherit priority. I.e. main thread might wait for a background thread for a result but the lower priority thread is not schedule as is a lower priority hence the main thread is blocked oding nothing and the background thread that should unlock the main is not scheduled.

## OEM optimization
interesting how HW producers try their own optimization to better use the CPU, it might affect how threads run.

# Navigation in Modular Applications with Deep Linking
Types:
- Modules by layer (we can switch easily layers implementation)
   - app
   - domain 
   - data
   - business logic
   - ...
- Modules by features, each modules contains all layers for a feature
   - dashboard
   - newsfeed
   - profile
   - core for shared components and code
- Module matrix featureXLayer
   - feature-ui
   - feature-data
   ...
# Navigation
can be done by activity, fragment transition, view composition

analysis on how modules and navigation structure affect dependency at code level and at team level (merge conflicts and dependencies)

# Deep linking 
It can help reducing cross dependency 
use http schema can be helpul to fallback to the webiste if the version of the device do not support that specific page.

deep link do not know from where the request come form -> solution could be to add content to the link so you know how to go back.

you can write your own solution or use libraries that levarage annotation, AirBnb library for example.

## Dynamic feature
Play.core functionality to load code module only when needed by the user, in this case the dependency is inverted, ithe app do not know all the features.

the navigation destination might not be available at runtime if the module has not been installed yeso the navigation module needs to change











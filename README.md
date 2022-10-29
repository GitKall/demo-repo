# demo-repo

#chatscript

topic: ~introductions []

t: Hello, talk to me!
 >:build mine
 
 ----Reading file simplecontrol.top
 Reading outputmacro: ^harry
 Reading outputmacro: ^georgia
 Reading table tbl:defaultbot
 Reading topic ~control
 Reading topic ~alternate_control
 
 ----Reading file tutorial.top
 Reading topic ~introductions
 No errors or warnings in build
 Read 302,955 Dictionary entries
 Read 304,588 Dictionary facts
 Read 110,851 Build0 facts
 Read 1 Build1 facts
 Concept sets: 1421
 Free space: 123,252,280 bytes FreeFacts: 4,584,560
 
 Hello, talk to me!
 >

 
  Hello, talk to me!
  
  >hi
  I don't know what to say.
  
  >why?
  I don't know what to say.
 
 topic: ~introductions []

t: ^keep() [Hello] [Hi] [Hey], [talk] [speak] [say something] to me!


  Hello, say something to me!

  >hi
  Hey, say something to me!

  >what
  Hey, talk to me!

  >why?
   Hello, speak to me!

  >who
  Hi, talk to me!

  >abc
  I don't know what to say.

  >def
  I don't know what to say.

topic: ~introductions []

t: ^keep() ^repeat() [Hello] [Hi] [Hey], [talk] [speak] [say something] to me!

topic: ~introductions []

t: [Hello] [Hi] [Hey], [talk] [speak] [say something] to me!

u: (what are you) ^keep() ^repeat() I am a bot.

u: (where do you live) ^keep() ^repeat() I live on your computer.

u: ([what where]) ^keep() ^repeat() Good question.


  Hello, say something to me!

  >hi
  I don't know what to say.

  >What are you?
  I am a bot.

  >Tell me where do you live.
  I live on your computer.

  >What is the time?
  Good question.

  >why?
  I don't know what to say.

  >Remind me where did you live please.
  I live on your computer.
u: (Where 'do you live) ^keep() ^repeat() I live on your computer.

  Hey, speak to me!

  >where do you live
  I live on your computer.

  >where did you live
  Good question.
topic: ~introductions keep repeat []

t: HI () [Hello] [Hi] [Hey], [talk] [speak] [say something] to me!

u: WHAT (what are you) I am a bot.

u: (tell me about yourself) ^reuse(WHAT) ^reuse(HI)

u: (where do you live) I live on your computer.

u: ([what where]) good question.


  Hello, speak to me!

  >tell me about yourself
  I am a bot. Hi, talk to me!

  >what are you
  I am a bot.

topic: ~introductions keep repeat []

t: [Hello] [Hi] [Hey], I will help you plan your travel. Just tell me where you want to go.

u: (I want to go to _*) OK, you want to go to _0. 


  Hello, I will help you plan your travel. Just tell me where you want to go.

  >I want to go to the moon.
  OK, you want to go to a moon.

  >I want to go to earth.
  OK, you want to go to earth.

  >I want to go back to the moon.
  I don't know what to say.

u: (I want to go * to _*) OK, you want to go to _0.

topic: ~introductions keep repeat []

t: [Hello] [Hi] [Hey], I will help you plan your travel. Just tell me where you are and
where you want to go to.

u: (be * at _*)
    OK, you want to go from _0.
    $source = '_0

u: ([go fly travel] to _*)
   $target = '_0
   OK, you want to go to $target .

u: (what do I want)
   You want to go from $source to $target .

   
  Hey, I will help you plan your travel. 
  Just tell me where you are and where you want to go to.

  >I am at Earth. 
  OK, you want to go from Earth.

  >I would like to fly to the moon.
  OK, you want to go to the moon.

  >What do I want? 
  You want to go from Earth to the moon. 

  >Actually, I want to go to the sky.
  OK, you want to go to the sky.

  >What do I want?
  You want to go from Earth to the sky. 


  Hey, I will help you plan your travel. 
  Just tell me where you are and where you want to go to.

  >I am at Earth. 
  OK, you want to go from Earth.

  >I would like to fly to the moon.
  OK, you want to go to the moon.

  >What do I want? 
  You want to go from Earth to the moon. 

  >Actually, I want to go to the sky.
  OK, you want to go to the sky.

  >What do I want?
  You want to go from Earth to the sky. 

  Hey, I will help you plan your travel. 
  Just tell me where you are and where you want to go to.

  >I am at Earth. 

    OK, you want to go from Earth.

  >I would like to fly to the moon.
  OK, you want to go to the moon.
  >What do I want? 
  You want to go from Earth to the moon. 
    >Actually, I want to go to the sky.
  OK, you want to go to the sky.

  >What do I want?
  You want to go from Earth to the sky. 

topic: ~introductions repeat keep []

t: [Hello] [Hi] [Hey], I will help you plan your travel. Just tell me where you are and
where you want to go to.

u: (be * at _*)
   $source = '_0

u: (go to _*)
   $target = '_0

u: (!$source)
   Where are you?

u: (!$target)
   Where do you want to go?

u: ($source $target)
   You want to go from $source to $target .


  Hello, I will help you plan your travel. 
  Just tell me where you are and where you want to go to.

  >great!
  Where are you?

  >Hod Hasharon
  Where are you?

  >I am at Hod Hasharon
  Where do you want to go?

  >I don't know
  Where do you want to go?

  >I want to go to Jerusalem
  You want to go from Hod Hasharon to Jerusalem.

  >really?
  You want to go from Hod Hasharon to Jerusalem.

  >Actually I am at Haifa.
  You want to go from Haifa to Jerusalem.

topic: ~introductions repeat keep []

t: [Hello] [Hi] [Hey], I will help you plan your travel.
   $issue = null # initialize the current issue

u: SOURCE (be * at _*)
   $source = '_0 # remember the source
   $issue = null # clear the current issue

u: TARGET (go to _*)
   $target = '_0
   $issue = null

u: ($issue=source _*) ^reuse(SOURCE) 
   # If current issue is source, then assume the 
   # user answered the question about his source

u: ($issue=target _*) ^reuse(TARGET)

u: (!$source)
   $issue = source # Remember that we asked the user about his source
   Where are you?

u: (!$target)
   $issue = target
   Where do you want to go?

u: ($source $target)
   You want to go from $source to $target .


  Hello, I will help you plan your travel.

  >great!
  Where are you?

  >Jerusalem
  Where do you want to go?

  >Actually I am at Haifa
  Where do you want to go?

  >Hebron
  You want to go from Haifa to Hebron.

topic: ~introductions repeat keep []

t: [Hello] [Hi] [Hey], I will help you plan your travel. Just tell me where you are and
where you want to go to.

u: (be * at _*)
   $source = '_0
   OK, you want to go from $source .

u: (go to _*)
   $target = '_0 
   OK, you want to go to $target .

u: (!$source)
   Where are you?

u: (!$target)
   Where do you want to go?

u: ($source $target)
   You want to go from $source to $target .

     Hello, I will help you plan your travel. 
  Just tell me where you are and where you want to go to.

  >I am at Haifa
  OK, you want to go from Haifa.

  >well?
  Where do you want to go?

  >I want to go to Jerusalem.
  OK, you want to go to Jerusalem.

  >what now?
  You want to go from Haifa to Jerusalem.

topic: ~introductions []

t: Hi, I will help you plan your travel.
 ^respond(~question)

u: SOURCE (be * at _*)
   OK, you want to go from _0.
   $source = '_0
   ^respond(~question)

u: TARGET (go to _*)
   $target = '_0
   OK, you want to go to $target .
   ^respond(~question)

u: DEFAULT ()
   ^respond(~question)

topic: ~question repeat keep nostay []

u: (!$source)
   Where are you?

u: (!$target)
   Where do you want to go?

u: ($source $target)
   You want to go from $source to $target . 


  Hi, I will help you plan your travel. Where are you?

  >I am at Haifa
  OK, you want to go from Haifa. Where do you want to go?

  >I don't know
  Where do you want to go?

  >go to Jerusalem
  OK, you want to go to Jerusalem. You want to go from Haifa to Jerusalem.

topic: ~introductions repeat keep []

t: [Hello][Hi][Hey], I will help you plan your travel.
   ^respond(~question)

u: SOURCE (at _*)
   Is your current location \" '_0 \" ?
   a: (~yes)
       $source = '_0
       ^respond(~question)
   a: (~no)
       OK, so where are you?

u: TARGET (to _*)
   Is your destination \" '_0 \" ?
   a: (~yes)
       $target = '_0
       ^respond(~question)
   a: (~no)
       OK, so where do you want to go?

u: DEFAULT ()
   ^respond(~question)

topic: ~question repeat keep nostay []

u: (!$source)
   Where are you?

u: (!$target)
   Where do you want to go?

u: ($source $target)
   You want to go from $source to $target . 


  Hello, I will help you plan your travel. Where are you?

  > at Haifa
  Is your current location "Haifa "?

  > no
  OK, so where are you?

  > at Ramat Gan
  Is your current location "Ramat Gan "?

  > yes
  Where do you want to go?

  > actually I am at Givat Shmuel
  Is your current location "Givat Shmuel "?

  > sure
  Where do you want to go?

  > to Jerusalem
  Is your destination "Jerusalem "?

  > y
  Where do you want to go?

  > to Jerusalem
  Is your destination "Jerusalem "?

  > yeah
  You want to go from Givat Shmuel to Jerusalem.

  > ...

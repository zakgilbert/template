---
layout: essay
type: essay
title: An Acquired Taste
date: 2018-09-20
labels:
  - Coding Standards
  - Programming
  - Software Development
---
<img class="ui image" src="{{ site.baseurl }}/images/unLearn2.png">

 Do you remember the first time you read some other persons code? There's only a few likely outcomes, ether their code was prettier than yours and you hated them, or your code was prettier than theirs and you hated them. After learning the basics of a coding language you begin to develop a taste for what you would consider attractive looking code.  Then some jabroni comes and enforces a coding standard, and you are forced to unlearn what you have come to think is attractive.  Which never really bothered me, I personally like having a structure to follow.  This way I can focus on solving problems rather than worry about aesthetics.  For those of you who have trouble with this, I would practice leaving your pride ,or whatever it is that makes it hard for you to to follow the rules, at the door.
 
 Needless to say I’m a stickler for coding standards as I was a stickler in my previous occupation of being a personal chef. I was basically the eslint of chefs, and I found it hard to keep assistants because I didn’t go easy on them when it came to cooking technicalities.  One time this guy I had hired, tried to pull this pork shoulder we had braised for pulled pork, with a wooden spoon (instead of a large fork), and I fired him on the spot. If this doesn’t make since too you don’t worry about it, let the chefs deal with it.  Just like if you are new to programming and hate coding standards, you have to remember this has been working for a long time, so please, be patient and try to develop your tastes. I know I still am. Please note that I did pay my assistant for the time that I promised him, I just wanted him gone.
 
 
 <img class="ui medium right floated rounded image" src="../images/8ae.png ">
# Why So Serious?
 I mean, can it really be that important?  I believe yes, and agree a hundred percent with my software engineering professor(Dr. Phillip Johnson) when he says *“that if you can only implement one software engineering technique to improve quality, it should be coding standards”.* Remember no program is perfect, which means at some point your going to have to go back and read it again.  Ever tried reading some of your old code and make sense of it?  The main thing that I’ve noticed about my old code is the wretchedness of my commenting.  When I took my program structure class, the Professor enforced a strict coding standard, one of which being that all comments about a function had to be outside of the function.  He pointed out that to many comments inside of the code will actually make the code harder to read.  He also enforced that the comments you make all follow a comment format, here’s what it was 
 ```
 /****************************************************************
 //
 //  FUNCTION NAME: deleteRecord
 //  
 //  DESCRIPTION:   Deletes a record in the data base specific to
 //                 the account number passed.
 //  
 //  PARAMETERS:    start (struct record **): First record in the
 //                                           data base.
 //
 //                 accountNumber (int)     : Account number of
 //                                           record to be deleted.
 //
 //  RETURN VALUES: -1: Account number does not exist.
 //                  0: Success!!
 // 
 *****************************************************************/
 ```

Seems like overkill doesn’t it? I think not; Imagine if someone you never meant had to figure out a program that you wrote without ever talking to you.  This is what should be in your head when commenting your code.  This way who ever is reading your program may not even have to read any code to comprehend whatever it is your program does. 

# You’re just a nobody
Though I’ve never worked on a large scale project I can assert what a coding standard might do for a development project of ten or more people.  Problems will arise, thus by enforcing a standard you will be eliminating so many problems before they can even arise.  If your one of those people who prides themselves in having a unique coding style, just remember when it comes to the outcome of a large scale project, you're a nobody.  For the love of god, display some pragmatism. The only thing that matters is the final product, and getting to that final product is much easier when you adhere to the coding standards. 

Just be grateful that you have quality assurance tools such as eslint, instead of some Gordon Ramsayesc coding standard enforcer that runs around the room pointing at your code saying stuff like, *“is that a satellite view of Beijing at rush hour?”*, or *“make sure to poke some holes in that code block so the variables can breathe.”*

# Developing Ones Tastes
Whether you are a stickler or a hater of coding standards, using quality assurance tools like eslint might seem unnecessary.  I honestly get pretty chapped about the warning messages that are constantly interrupting my thought process, but I’m realizing that its not just enforcing the coding standard but teaching me it.  In a few weeks I know I’ll be getting less errors because I will have memorized the format.  

 I’m constantly comparing my current computer science endeavors to my experiences in the restaurant industry.  Coding standards to me is like plating food, yeah its easy to make it look pretty, but in a restaurant, enforcing that every plate looks the same, is a difficult task. You're going to need that Gordon Ramsayesc chef to running around saying stuff like, *“is that a lobster or the elephant man?”*  Its the only way; I wish they had eslint for plating food, t`would be spectacular. 

While certain coding standards might have an acquired taste, the only way to acquire an acquired taste is to eat whatever your trying to acquire the taste for. So don’t be that forty-three year old who’s afraid of eating tomatoes, and realize that it’s for the benefit of your team.

 

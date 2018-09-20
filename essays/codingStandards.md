---
layout: essay
type: essay
title: An Aquired Taste
# All dates must be YYYY-MM-DD format!
date: 2018-09-20
labels:
  - Coding Standards
  - Programming
  - Software Development
---


<img class="ui image" src="{{ site.baseurl }}/images/C-Coding-Standard.png">

 Do you remember the first time you read some other persons code? There's only a few likely outcomes, ether their code was prettier than yours and you hated them, or your code was prettier than theirs and you hated them. After learning the basics of a coding language you begin to develop a taste for what you would consider attractive looking code.  Now for those people, you knows who I’m talking about…
 
 ```
 static void gameOver() {/// sets up Game Over screen.... if you play the
 							/// game, you'll see this lot
 		Theme.pause();
 		MOG.removal();
 		long t = System.currentTimeMillis();
 		EZSound sad = EZ.addSound("GameOver.wav");
 		sad.play();
 		EZImage halfDead = EZ.addImage("Mog - Wounded.gif", MOG.getX(), MOG.getY());
 		EZ.addRectangle(SCREENWIDTH / 2, SCREENHEIGHT / 2, SCREENWIDTH, SCREENHEIGHT, Color.BLACK, true);
 		EZText gO = EZ.addText(SCREENWIDTH / 2, SCREENHEIGHT / 2, "GAME OVER", new Color(190, 0, 0), 60);
 		gO.setFont("8-BIT WONDER.TTF");// was having issues getting the font to
 										// set before the text is seen. tried
 										// putting /gO/ into static variable,
 										// and
 										// making an individual function for it.
 										// tried putting it under the background
 										// and moving it up once player dies. I
 										// even tried making a class for it
 		halfDead.pullToFront();
 		gO.pullToFront();
 		while (true) {/// blocking for HERO
 			if (System.currentTimeMillis() - t >= 2000) {
 				halfDead.pushToBack();
 				EZImage dead = EZ.addImage("Mog - Dead.gif", MOG.getX(), MOG.getY());
 				dead.pullToFront();
 			}
 
 		}
 ```
 
 In all honesty that's some of my early code, from my first game I wrote, [Ninja Shepherd](https://www.youtube.com/watch?v=U4HBGTayWi0), in my first coding class and it is hideous, but its only because I was ignorant and hadn’t developed a taste for sexy code. If you show an average person who’s never adapted this taste, odds are its gonna make them want to puke no matter how nice it is, thus this changes and develops over time. In the past two years I’ve gone from liking the leading curly bracket of a function to be on the same line as the title of the function, to liking curly brackets only on their own line, and once I started taking software engineering at the University of Hawaii at Manoa I’ve gone back to liking what I originally liked.
 
 <img class="ui medium right floated rounded image" src="../images/8ae.png ">
 
 Needless to say I’m a stickler for coding standards as I was a stickler in my previous occupation of being a personal chef,  I found it hard for me to keep an assistant because I didn’t go easy on them when it came to cooking technicalities.  One time this guy I had, tried to pull this pork shoulder we had braised for pulled pork, with a wooden spoon (instead of a large fork), and I fired him on the spot. If this doesn’t make since to you don’t worry about it, let chefs deal with it.  Just like if you are new to programming and hate coding standards, remember this has been working for a long time so please, be patient and try to develop your tastes. I know I still am. Please note that I did pay my assistant for the time that I promised him, I just wanted him gone.
 
 ## Why So Serious?
 
 I mean can it really be that important?  I believe yes, and agree a hundred percent with Professor Dr. Johnson. Remember no program is perfect, which means at some point your going to have to go back and read it again. Ever tried read some of your first code and make since of it?  The main thing that I’ve noticed about my old code is the wretchedness of my commenting.  When I took my program structure class, the Professor enforced a strict coding standard, one of which being that all comments about a function had to be outside of the function.  He pointed out that to many comments inside of the code will actually make the code harder to read. He also enforced the comments you make all follow a comment format, here’s what it was 
 
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
 
dfsgdfgdfgdfgsdfgsdfgsdf


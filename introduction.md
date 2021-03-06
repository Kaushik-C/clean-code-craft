# Clean Code
- Clean Code is not  a beautiful code and has no beauty reasons
- Professional programmers are not paid for writing beautiful or pretty
code
- Code is clean if it can be understood and maintained easily by any team member.
- Clean code is the basis for being fast
	- If your code is clean and test coverage is good, a change or a new
function just take a few hours or a couple of days – and not weeks or months
- Clean code is the foundation for sustainable software and keeps a software development project running over a long time without accumulating a large amount of technical debt
- Clean code is also a key to make a happier developer
	- It leads to a stress-free life
	- If code is clean and developer feeling comfortable with it,  keep calm in every situation, even in front of a tight project deadline.
- Clean code saves money (economic efficiency)
	- Each year, development organizations lose a lot of money because
their code is in bad shape

### Why Code should be Bug Free 
- **`There is no life today without software!`**
- Board an elevator, we give our lives are in the hands of software.
-  Aircrafts are controlled by software, and the entire, worldwide air traffic control system depends on software.
-  Modern cars contain a significant amount of small computer systems with software that communicate over a network, responsible for many safety-critical functions of the vehicle. Air conditioning, automatic doors.
-  medical devices, trains, automated production lines in factories 
-  Digital Revolution and the Internet of Things (IoT), the relevance of
software for our life will again increase significantly.
- The autonomous (driverless) car.

Bug in above software-intense systems can have catastrophic consequences
Quality is under no circumstances negotiable in these kinds of systems - **Never!**

## Different levels of quality assurance measures in software development projects
These levels are often visualized in the form of a pyramid – the so-called **`Test Pyramid`**

![testpyramid](https://github.com/venu-shastri/clean-code-craft/blob/master/images/testpyramid.PNG)

>Experience has shown that the total costs regarding implementation and maintenance of tests are increasing toward the top of the pyramid.
> Large system tests and manual user acceptance tests are usually complex, often require extensive organization, and cannot be automated easily.
> large system tests, or UI-driven tests, are totally improper to check all possible paths of execution through the whole system . 
> if a test on a system level fails, the exact cause of the error can be difficult to locate

Unfortunately, in several software development projects we will  find **`degenerated Test Pyramids`**
- **Ice Cream Cone Anti-Pattern** - Enormous effort is put into the tests on the higher level, whereas the elementary unit tests are neglected .
- **Cup Cake Anti-Pattern** - In the extreme case elementary unit tests are completely missing
- 
![enter image description here](https://github.com/venu-shastri/clean-code-craft/blob/master/images/DegeneratedTestAntipatterns.PNG)

### How to  ensure High Quality of a Software System
>A broad base of **`inexpensive, well-crafted, very fast, regularly maintained, and fully automated unit tests, supported by a selection of useful component tests`**.

## Unit Test
**`refactoring” without tests isn’t refactoring, it is just moving shit around`**.
—Corey Haines (@coreyhaines), December 20, 2013, on Twitter
- A unit test is a piece of code that executes a small part of your production code base in a particular context.
- Unit Test Advantages
	- fixing bugs after software is shipped has been proven to be much more expensive than having unit tests in place
	- Unit tests give an immediate feedback about your entire code base
	- A high coverage with unit tests can prevent time-consuming and frustrating debugging sessions
	- Unit tests are a kind of executable documentation because they show exactly how the code is designed to be used
	- Unit tests can easily detect regressions, that is, they can immediately show things that used to work, but have unexpectedly stopped working after a change in the code was made.

#### What about QA?
A developer  attitude: **`Why should I test my software? We have testers and a QA department, it’s their job`**

Is software quality a sole concern of the quality assurance department?

**`I’ve said this before, and I’ll say it again. Despite the fact that your company may have a separate QA group to test the software, it should be the goal of the development group that QA find nothing wrong`**.
—Robert C. Martin, The Clean Coder [Martin11]
- QA is  second safety net

### How to write production code  for the unit test code?
**`Be Principled`**

#### What Is a Principle?
>A principle is a kind of rule, belief, or idea that guides you. Principles are often directly coupled to values or a value system

- **KISS**
	- Focusing on simplicity is probably one of the most difficult things to do for a programmer. And it is a life long learning experience
- **YAGNI**
	- Always implement things when you actually need them, never when you just foresee that you need them.
- **DRY**
	- Copy and paste is a design error
	- Referred to as “Once And Only Once” (OAOO).
	- applying the DRY principle means that we have to ensure that “every piece of code must have a single, unambiguous, authoritative representation within a system
- **Information Hiding**
	- The principle states that one piece of code that calls another piece of code should not know internals about that other piece of code.
	- information hiding is the basic principle for decomposing systems into modules
	- advantages of information hiding:
		- Limitation of the consequences of changes in modules
		- Minimal influence on other modules if a bug fix is necessary
		- Significantly increasing the reusability of modules
		-  Better test-ability of modules
	- Information hiding is often confused with **encapsulation**, but it’s not the same
	- ex:-
	```C++ 
	class  DeviceConnection { 
	public:
	enum  class  State {
	closed = 1,
	opening,
	open,
	closing
	};
	private:State state;
	// ...more attributes here...
	public:
	State  getState() const;
	// ...more member functions here...
	};
	#include  "DeviceConnection.h"
	int  main() {
	DeviceConnection connection;
	connection::State connectionState = connection.getState();
	if (connectionState == DeviceConnection::State::closed) {
	// do something...
	}
	return  0;
	} ```

>What will happen if the internal implementation of DeviceConnection  must be changed and the enumeration
class State is removed from the class? It is easy to see that it will have a significant impact on the client’s code. It will result in changes everywhere where member function DeviceConnection ::getState() is used

| Information Hiding | Encapsulation |
|--|--|
| Information hiding is a design principle for aiding developers in finding good modules. The principle works multiple levels of abstraction and unfolds its positive effect, especially in large systems | Encapsulation is OO Concept to define role and responsibilities ,often a programming-language dependent, technique for restricting access to the innards of a module ,For instance, in C++ you can precede a list of class members with the private keyword to ensure that they cannot be accessed from outside the class. But just because we use such kind of guards for access control, we are still far away from getting information hiding automatically |


- **Strong Cohesion**
	- cohesion is strong when the module does a well-defined job
	- Shot Gun Anti-Pattern.
		- form of weak cohesion
- Loose Coupling
- **Optimizations**
	- Premature optimization is the root of all evil (or at least most of it in programming.
—Donald E. Knuth, American computer scientist [Knuth74]
	- As long as there are no explicit performance requirements to satisfy, keep your hands off optimizations.
		- The subtly bugs are slipped into the code during  optimization measures
		- compilers are nowadays very good at optimizing code.
		- Whenever you feel just a desire to optimize something, think about YAGNI
- **Principle of Least Astonishment (PLA)**
	- Also known as Principle of Least Surprise (POLS)
	- Well known in user interface design and ergonomics
	- The principle states that the user should not be surprised
by unexpected responses of the user interface.
	-  The user should not be puzzled by appearing or disappearing
controls, confusing error messages, unusual reactions on established keystroke sequences  or other unexpected behavior
- **The Boy Scout Rule**
	-  Always leave the campground cleaner than you found it.
	- One of their principles states that they should clean up a mess or pollution in the environment immediately, once they’ve found such bad things
	- Developers should apply this principle to our daily work. Whenever we find something in a piece of code that needs to be improved, or which is a bad code smell, we should fix it immediately. And it does not matter who the original author of this piece of code was.
	- Advantages
		- continuously prevent the dilapidation of our code
		- Renaming a poorly named class, variable, function, or method 
	-  Behaviors
		- Decomposing the innards of a large function into smaller pieces 
		- Deleting a comment by making the commented piece of code self-explanatory
		- Cleaning up a complex and puzzling if-else-compound.
		- Removing a small bit of duplicated code
		- Collective Code Ownership.
			- Every team member, at any time, is allowed to make a change or extension on any piece of code.
			- There should be no attitude like
			- “This is not my  code, and that’s Fred’s module. I don’t touch them!”
			- It should be considered to be a high value that other people can take over the code we wrote. Nobody in a real team should be afraid, or have to obtain permission, to clean up the code, or to add new features
		
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM3NDExNzk1NiwtMjI2NDc4MDMwLDE3OD
Q2NTYyODAsOTM0MTI1MzI2LDMzOTM0NDgxMCwxMTcxNjc3NDI3
LC03MTAyODE3ODMsNTM5MTI3Mzg0LC0xOTg1NDM4MjE5LC01NT
A5NDk0MCwyMTAyNDEyODIwLDU3NzgyMzcwNSwtOTQ3OTIwNTQ4
LC0xNTE3NDcwNjYzXX0=
-->
"Welcome 😁 I guess it’s safe to assume you're a self-learning noob (like me). I am pasting this as my std recommendations I came up with for beginners like me(my goal Being low level C type programming).

This is some history/experience and the path I am following after about a years’ worth of self-learning research, trial and error, recommendations etc. This is not if you simply want to learn C, but want to consider programming, using C as your main tool. 

So maybe first a twist and a background, which perhaps will even be un-common/un-popular 🙈.First, understand that I'm a noob esp. in the pc, open systems, web world etc.

So, after a little over a year of :

- starting out with python, but then realising I like lower-level stuff more, then,

- moving to C, and then realized,

- asm is actually a good/the right starting point for C, then realized,

- I don’t know enough of the systems domain or have an efficient notes system and workflow toolset, which slows me down and irritate me, so

- I decided, bash and vim + vimscript and learning more about Linux from a systems programming perspective starting with the basics (cli, terms, gnu + kernel, window managers, file systems, device drivers, boot etc. (and currently busy here). 

Although I never did it, but I was basically in that category of people not knowing what to do next. You know the "what project can I do now that I learnt X ? ", questions. Tutorial hell was also knocking.

So, all this basically meant that I had to take a step back(unintentionally/forced whatever) from trying to get to grips with a programming language, because I realised that these “language” learnings are not the right approach for me. I was trying to access a domain I didn’t know well enough and needed tools(editors, notes system, automated things/scripts, understanding and being more proficient with my chosen platform in Linux etc) to make my learning more efficient and enjoyable.

But most of all, I realised that I wasn't getting joy trying to learn a language first and that the language was probably the easy part and I was therefore complicating things a lot more with this approach. Over and above the domain and environment learning stuff, I needed to learn programming first. So, after lots of research over this period, my final decision/plan from a programming perspective, led me to :

~Start with SICP(lisp Sicp - https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-001-structure-and-interpretation-of-computer-programs-spring-2005/index.htm

, busy here now) , then go back to asm, then go back to C and then Go. Python must wait 🤔.

This SICP approach of teaching programming approaches/thinking more than language nuances etc. is what I missed all along. And I think lisp is awesome for a newb from that perspective. I am finally enjoying this and hope this will stay as fun as it is now.

So, after the above twist... let’s say U are now ready to “specialize”. The second most important thing I feel, is not to just pick a language because people say it’s easy etc. Remember, you already know some lisp at this stage, so let the 2nd language pick itself. What you must decide now, is the domain you will be interested in(i.e., Games, data science, web, low level, business/finance, mobile Apps, embedded, iot, etc)., If you are not sure, take any domain where you already have non-programming experience in because it will help a lot. Now the language will pick itself, because if you research for example front end web you may end up with java script, games maybe c++/c#, data science maybe Julia/python etc.

So, after SICP, I will start learning C as per below, also note this is excluding learning the tool chains(i.e., editors, IDE, vcs etc), target environments (i.e., Linux, windows OS etc) 

First, is to get an effective, efficient note Taking system in place. Something that works well with your workflow, integrated into your editor, easily searchable etc.

Start at assembly, "programming from the ground up" J Bartlett - > Sets you up to understand some of C under the hood for later (edit : he released a new book "learn to program with assembly").

Now that you have basics, go to "k&r2" and together with that use "hacking the art of exploitation" - > the 2nd book helps to set you up for and learn about debugging from the beginning at hello world (yes pls redo from hello world in k&r2, reverse engineer it and debug it). So, use these two together (I. E. Do chp 1 and 2 in k&r2 and then HTAOE until the card game end of part 1,  then go and reverse engineer, debug all the k&r2 exercises done till now. 

After this, pick up some of the below or as many as possible :

modern C" Jens Gustetd, - > update to a bit of modern C ways etc. Kn King , a modern approach second edition -> update to c99 , very large book. A nice one to use also is : https://beej.us/guide/bgc/ On pointers specifically : Ted Jensen's "a Tutorial on Arrays and Pointers in C" a useful resource is also https://cdecl.org/ , especially to read others code. https://www.youtube.com/playlist?list=PLBlnK6fEyqRhX6r2uhhlubuF5QextdCSM https://graphics.stanford.edu/~seander/bithacks.html

And this "effective C" is probably a must if you ever read about people saying C will shoot you in the foot (don't let it happen to you as far as possible 😉) https://accu.org/bookreviews/2020/glassborow_1952/ Also, C traps and pitfalls by Koenig, Andrew

Always look up, read and try understand any std function using the book "the C standard library" Plauger, or https://www.cplusplus.com/reference/clibrary/  or https://www.gnu.org/software/libc/manual/html_node/index.html#toc-Introduction-1

Ccan can also help : https://ccodearchive.net/list.html

Also try this once you have the hang of things. I can't comment on code quality yet 😬 https://not.cafe/2020/10/12/getting-started-with-c-programming.html https://github.com/johnpayne-dev/MinecraftC/blob/main/MinecraftC/Minecraft.c

User  |11||11||1111 on Reddit also posted this in braces, which I like. I would say add gdb and understand how to see and follow each line of code as you go here. {r/|11||11||1111 -....

I’d start a small project and gradually add to it. The general approach is:

start by creating an array and store 1000 random double values in it

write code to calculate the min, max and average value

now write some code to sort the array

now move those 4 functions (min, max, average, sort) into separate .c files. This exposes you to thinking about data hiding (i.e., not exposing the array publicly to other C files). This will expose you to the fact that C doesn’t have scope keywords like private, public, protected. It also expands the project and opens the need to understand .h files and (if you’re not using an IDE) you need to understand how to compile and link multiple files to generate an executable - on Linux, this would be by using makefiles

now change the array size to 500 million. This will compile but, likely, will crash (or segfault) when you run it. This exposes you to heap and stack (c arrays are on the stack and the array is now too big to fit on the stack). You’ll need to move the array to the heap and deal with malloc/calloc. This will also expose you to pointers.

you can put timer code around each of the 4 operations and play with various compiler options to improve the performance. Also turn on various compiler warnings (if using gcc or clang, -Wall and -Werror). You’ll have hours of fun fixing up “problems” in your code.

if you feel adventurous, move the 4 operations into separate threads. This will expose you to multithreaded issues like sorting the array while trying to find the average (i.e., you need to protect the array using some form of mutex or semaphore). The min, max and average can all run in parallel (they don’t modify the array) but the sort operation needs sole access to the array. This is useful to understand because it forms the basis of the Rust language’s ownership model }

By now you have learnt C basics nicely and most probably already digressed or done lots of research along the way and a few projects, maybe met a few people and you can most probably now be a good and capable beginner.

Now the tuff parts begin, " the domain ", (I. E. using C in the best possible way for the domain you are interested in).

That's my path, maybe gurus can review and comment, which I will also gladly appreciate.

Good luck and enjoy the ride 🙏🏽👍
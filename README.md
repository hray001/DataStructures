#Data Structures

[Original] (https://github.com/hray001/DataStructures)

##Table of Contents
1. [Purpose] (#purpose)
2. [TL;DR] (#TL;DR)
3. [Map] (#map)
4. [List] (#lists)
5. [Stack] (#stack)
6. [Queue] (#queue)
7. [Vector] (#vector)
8. [Some Useful Things To Read] (#readings)

##Purpose
Coming out of cs14 you have been hammered with data structures against your 
will and hearing more about them is probably the last thing you want, but 
it is important to remember that they exist for a purpose and if you ignore 
their existence because you are fed up with them, you'll regret it like I 
did. Hence this simple refresher of a few data structures you might find 
useful.  

Many of these data structures exist in the boost library and I would highly 
reccomend getting used to some of the boost features. Boost has some 
rather obscure data structures that might be exactly what you need one day. 
The only reason this tutorial does not cater to the BOOST library is that 
only a few of the boost packages are installed automatically on linux and 
the lab machines do not contain a lot of the ones you would need to use 
the BOOST versions of these structures. 

####TL;DR:
*Maps are useful, REALLY useful and your professor will attest to 
their use. Stacks and Queues are less common but in certain situations they 
make your job immensely easier and reign supreme. Yes, lists can be a 
pain to deal with if you hate pointers, but if you get comfortable using 
pointers and the rules associated with them they become another tool you 
will have at your disposal. 
Don't rely only on arrays and vectors just because you're used to them, 
sometimes they aren't the answer you're looking for.* 

###Map
A map is a container filled with Pairs made out of a Key, used to reference/retrieve data, and the actual data itself. An important piece of information to remember about maps is that they are sorted by design as you add to them based off the map's comparison object. To create a map you must decide what you want to store, and how you wish to reference that data. If your `pair<const Key, data_type data>` was `pair<int, string>` you would have a map of `int` values which referenced some data of type `string`. Basically at each index of the map (`m[int]`) you would have a string value.

Here is a basic map declaration with an example assignment operation: To put it into context lets say this map is set up to contain the weekly rankings for a popularity contest. 
```
#include <map>
using namespace std;
int main(){
    map<int, string> m;     //There is a more thorough example for maps 
    map[1] = "Jack QWERTY"; //in the map directory, this just covers basic
    map[2] = "Jill UIOP";   //implementation
    map[3] = "Jan Sto Domingo";

    return 0;
}
```
That's a pretty boring idea as there is nothing actually DONE with the information, but it at least shows the basic implementation.

Now maps are by default ordered, but there also exists the unordered version
 which has a faster access time considering you know the key but searching
  through it is slow. Unordered maps are implemented through the use of 
  hash tables to allow said fast access time. Creating your own `hash<Key>`
  function is also allowed if you so desire. The interesting part of 
  unordered maps is that they implement the bucket style hash table
  where each hashed value is allowed to contain more than one piece of data.
  

###Lists
Linked lists are made up of nodes containing the data and a pointer
 to the next position in the list. This gives Lists an advantage
 over vectors when inserting and deleting since it only requires
 changing the pointers as opposed to shifting the entire vector over. 
 It should be mentioned as well that a list maintains an advantage over vectors
 in that vector expansion is costly while lists just need to dynamically
 allocate a new node.
 What you lose for this advantage is the ability of random access, making it slow to search through the list.
 To create a list you need only to deal with your desired data types. 
```
#include <list>
using namespace std;
int main(){
    list<int> l; //list from 0-99
    for(int i = 0; i < 100; i++) l.push_back(i);
    //same style of insertion as vector, you deal with 
    //pushing and popping element
    for(list<int>::const_iterator it = l.begin; it != l.end(); ++it)
        cout << *it << " "; //act on the object in the list
    cout << endl;
    return 0;
}
```
The default linked list is a doubly linked list (it contains pointers to the previous node as well as the next). If you want a singly linked list then use stl `<forward_list>`.

###Stack
(First In Last Out)  
Stacks are interesting in that they only deal with the top of the structure.
 You either push to the top, or pop off the top. A good example of a stack is
 using it to reverse something. When you push, say a string, to the stack after 
 popping all of the elements off the string would be in reverse.
 ```
#include <stack>
using namespace std;
int main(){
    stack<int> rev;
    unsigned i;
    int arr[10];
    for(i = 0; i < 10; ++i) rev.push(i);
    i = 0; 
    while(!rev.empty()){
        arr[i] = rev.top(); //just to show the order the items come off the stack
        rev.pop();
        ++i;
    }
    //can then do something with your reversed items, or you could have 
    //done something with them immediately as you popped them off the top
    return 0;
}
```
Stacks are used mostly in compilers and operating systems so if that type of 
thing is your interest, it would be useful to be used to visualizing a stack.

###Queue
(First In First Out)  
Queues can be thought of as a tunnel, what goes into the tunnel first is going 
to be the first thing to come out of the tunnel. The most common use of this 
is for job scheduling (just think of a login queue for a game, those who enter 
the queue to be logged in first are those who get in first). Just like a stack 
the main two operations for a queue are push and pop. You could use this in 
the case where you had a set of operations you wanted to execute sequentially. 
By putting them into a queue and just operating on the item popped off the 
queue you could iterate through said operations.
```
#include <queue>
using namespace std;
int main(){
    queue<int> q;
    for(unsigned i = 0; i < 10; ++i){
        q.push(i); //really simple example for pushing integers to a queue
                   //but instead think of the integers as commands you wish
                   //to execute and the queue becomes much more useful
    }
    while(!q.empty()){
        //execute starting with the first entry pushed
        /*execute( */ q.front() /* ) */ ;
        q.pop();
    }
    return 0;
}
```
There also exist priority queues (still `#include <queue>` but declared as
`priority_queue<Typename> pq;`) which instead of just pushing to the back, push 
calls the function `push_back()` of the object being pushed then calls 
`push_heap` (all inside of the original push() function) to reorder the 
priority queue. So instead of popping the very first thing pushed, what is 
popped is the item with the highest priority, the item at the top, based on
the container. So for an example where the container is an `int` the object
with the highest priority would be the highest number. 
Just like stacks queues are used in operating systems just more on the side 
of process scheduling.

###Vector
Vectors are the goto answer whenever someone thinks they need a simple 
array but they do not know how large the array will be. Internally a vector 
is just a dynamically allocated array which is reallocated any time new 
elements which would push the array out of bounds are entered. As was 
stated above in the "List" section vectors perform extremely well with 
random access but perform poorly when inserting or removing items. One 
thing to note with vectors is the ability to change either the size or 
compacity. The compacity refers to the amount of memory allocated to the 
array while the size refers to number of elements in the vector. Vectors 
are nice in their simplicity and that they cover the basic needs of 
many situations.
```
#include <vector>    //vector example is a bit too easy, just treat it as
using namespace std; //an array you can resize and check if you reference
int main(){          //an out of bounds item
    vector<int> v;
    return 0;
}
```
Vectors can be overused however when you rely on them too heavily. For 
example I have been in the situation where I thought I needed a 
`vector< vector<string>`. What I really wanted to do however was map `int` 
values to said `vector<string>` so getting too caught up in using vectors, 
I confused myself and overcomplicated things by trying to force something 
simple into something complex when I did not need to. Simple solutions should
 be preferred to complex solutions.

###Readings
[Uses of data structures] (http://stackoverflow.com/questions/1539069/practical-uses-of-different-data-structures)

[Dictionary of all you could hope to know about algorithms and data structures and then some] (http://xlinux.nist.gov/dads//)

[Nice basic tutorial, solid example programs included] (http://www.cs.fsu.edu/~jestes/cop3330/notes/datastruct.html)

[Use of data structures in your life?] (http://stackoverflow.com/questions/389216/advanced-data-structures-in-practice)

[Interesting lesser known data structures] (http://stackoverflow.com/questions/500607/what-are-the-lesser-known-but-useful-data-structures?rq=1)

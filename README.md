Data Structures
===
##*Map
A map is a container filled with Pairs made out of a Key, used to reference/retrieve data, and the actual data itself. An important piece of information to remember about maps is that they are sorted by design as you add to them based off the map's comparison object. To create a map you must decide what you want to store, and how you wish to reference that data. If your `pair<const Key, data_type data>` was `pair<int, string>` you would have a map of `int` values which referenced some data of type `string`. Basically at each index of the map (`m[int]`) you would have a string value.

Here is a basic map declaration with an example assignment operation: To put it into context lets say this map is set up to contain the weekly rankings for a popularity contest. 
```
#include <map>
using namespace std;
int main(){
    map<int, string> m;
    map[1] = "Jack QWERTY";
    map[2] = "Jill UIOP";
    map[3] = "Jeniffer ASDF";

    return 0;
}
```
That's a pretty boring idea as theres nothing actually DONE with the information, but it at least shows the basic implementation.

Now maps are by default ordered, but there also exists the unordered version which has a faster access time considering you know the key but searching through it is slow.

##*Lists
Linked lists are made up of nodes containing the data and a pointer to the next position in the list. This gives Lists an advantage over vectors when inserting and deleting since it only requires changing the pointers as opposed to shifting the entire vector over. What you lose for this advantage is the ability of random access. To create a list you need only to deal with your desired data types. 
```
#include <list>
using namespace std;
int main(){
    list<int> l(0,100); //list from 0-100
    l.push_back(101) //same style of insertion as vector, you deal with
                     //pushing and popping elements
    return 0;
}





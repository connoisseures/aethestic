# c++

## C++ coding tips 

### class

[Can a c++ class include itself as a member?](https://stackoverflow.com/questions/2706129/can-a-c-class-include-itself-as-an-member)No, because the object would be infinitely large \(because every Node has as members two other Nodeobjects, which each have as members two other Node objects, which each... well, you get the point\).You can, however, have a pointer to the class type as a member variable:`class Node {    char *cargo;    Node* left;   // I'm not a Node; I'm just a pointer to a Node    Node* right;  // Same here};`  
If a non-static object is member then declaration of class is incomplete and compiler has no way to find out size of the objects of the class.Static variables do not contribute to the size of objects. So no problem in calculating size with static variables of self type.For a compiler, all pointers have a fixed size irrespective of the data type they are pointing to, so no problem with this also.[https://www.geeksforgeeks.org/can-a-c-class-have-an-object-of-self-type/](https://www.geeksforgeeks.org/can-a-c-class-have-an-object-of-self-type/)  


* this pointer 

`class T{    int x;     void foo()    {        x = 6;       // same as this->x = 6;        this->x = 5; // explicit use of this->    }};`[https://en.cppreference.com/w/cpp/language/this](https://en.cppreference.com/w/cpp/language/this)  


### static 

[https://www.geeksforgeeks.org/static-keyword-cpp/](https://www.geeksforgeeks.org/static-keyword-cpp/)

* the scope of the static object is throughout the **lifetime** of the program.

**Static variables in a Function**: 

* When a variable is declared as static, space for **it gets allocated for the lifetime of the program**. 
* Even if the function is called multiple times, space for the static variable is allocated only once and the value of the variable in the previous call gets carried through the next function call.

**Static variables in a class**: 

* As the variables declared as static are initialized only once as they are allocated space in separate static storage so, the static variables **in a class are shared by the objects.** 
* There can not be multiple copies of the same static variables for different objects. Also because of this reason, static variables can **not** be initialized using constructors.
* a static variable inside a class should be initialized explicitly by the user using the class name and scope resolution operator outside the class as shown below:

**`class`** `GfG {` **`public`**`:`     **`static`** ``**`int`** `i;     GfG() { // Do nothing     }; };` **`int`** `GfG::i = 1;` **`int`** `main() {     GfG obj;     // prints value of i     cout << obj.i;  } //output: 1`  
**Static Members of Class**

* **Class objects as static**: Just like variables, objects also when declared as static have a scope until the lifetime of the program.
  * Now the destructor is invoked after the end of main. This happened because the scope of the static object is throughout the lifetime of the program.

**`class`** `GfG {`     **`int`** `i = 0;`     **`public`**`:     GfG() {         i = 0;         cout << "Inside Constructor\n";     }     ~GfG() {         cout << "Inside Destructor\n";     } };` **`int`** `main() {`     **`int`** `x = 0;`     **`if`** `(x==0) {`         **`static`** `GfG obj;     }     cout << "End of main\n"; } //output:Inside ConstructorEnd of mainInside Destructor`**Static functions in a class**: 

* Just like the static data members or static variables inside the class, static member functions also does not depend on object of class. 
* We are allowed to invoke a static member function using the object and the ‘.’ operator but it is recommended to invoke the static members using the class name and the scope resolution operator.
* **Static member functions are allowed to access only the static data members or other static member functions**, they can not access the non-static data members or member functions of the class

**`class`** `GfG {`    **`public`**`:     // static member function`     **`static`** ``**`void`** `printMsg() {         cout<<"Welcome to GfG!";     } };// main function` **`int`** `main() {     // invoking a static member function     GfG::printMsg(); }` 

* In C++, a static member function of a class **cannot** be virtual.

[https://en.cppreference.com/w/cpp/language/static](https://en.cppreference.com/w/cpp/language/static)  
quiz:[https://www.geeksforgeeks.org/stati/](https://www.geeksforgeeks.org/stati/)  


### &&, \|\|

&& will not evaluate the second operand if the first operand is false. `// this comment is required to explain to developers that // f2() is called only when f1() returns false, and so on...bool ok = f1() || f2() || f3() || f4();`

### define and declaration

[https://www.tutorialspoint.com/What-is-the-difference-between-a-definition-and-a-declaration-in-Cplusplus](https://www.tutorialspoint.com/What-is-the-difference-between-a-definition-and-a-declaration-in-Cplusplus)

* A declaration means \(in C\) that you are telling the compiler about type, size and in case of function declaration
* No space is reserved in memory for any variable in case of the declaration.
* The Definition space is additionally reserved in memory. 
* You can say "DEFINITION = DECLARATION + SPACE RESERVATION".

### struct 

struct & class[http://courses.washington.edu/css342/zander/css332/classstruct.html](http://courses.washington.edu/css342/zander/css332/classstruct.html)constructor and deconstructor for struct.   
important tipsplus first or plus late`- a[b++] = c[i++]  equal to :    a[b] = c[i]    b++;    i++;- a[`[`++`](https://paper.dropbox.com/doc/YiNjuKh7FPtg3I3COix2H) `b] = c[`[`++`](https://paper.dropbox.com/doc/eb8RUxFMJvR5EtBOiHRJh) `i]  equal to :    b++;    i++;    a[b] = c[i]`  
  
[https://stackoverflow.com/questions/151850/why-would-you-use-an-assignment-in-a-condition](https://stackoverflow.com/questions/151850/why-would-you-use-an-assignment-in-a-condition)It's more useful for loops than if statements.`while( var = GetNext() ){  ...do something with var }`Which would otherwise have to be written`var = GetNext();while( var ){ ...do something var = GetNext();}`  
[Remove the last character from C++ string](https://stackoverflow.com/questions/2310939/remove-last-character-from-c-string)`st = myString.substr(0, myString.size()-1);`  
Important! pass by reference can be passing by x + 1;s  
sort `//this function should not be in a class!!!bool myfunction (int i,int j) { return (i<j); }  
int main () {  int myints[] = {32,71,12,45,26,80,53,33};  vector<int> myvector (myints, myints+8); // 32 71 12 45 26 80 53 33    // using default comparison (operator <):  std::sort (myvector.begin(), myvector.begin()+4);   //(12 32 45 71)26 80 53 33  
  // using function as comp  std::sort (myvector.begin()+4, myvector.end(), myfunction);   // 12 32 45 71(26 33 53 80)`  
  
**Vector Collection** 

How to declare a dynamic 2D array in C++`int** a = new int*[rowCount];for(int i = 0; i < rowCount; ++i)    a[i] = new int[colCount];`  
initial a 2D vector in a function with a parameter, size. `int vec(int n){    std::vector<std::vector<int> > fog(    n,    std::vector<int>(n)); // Defaults to zero initial value        for(int i = 0; i < n; i++){        cout << fog[i][i] << endl;    }    ...}`[https://stackoverflow.com/questions/17663186/initializing-a-two-dimensional-stdvector](https://stackoverflow.com/questions/17663186/initializing-a-two-dimensional-stdvector)  
pass 2D array to function in C++

* There are three ways to pass a 2D array to a function:

1. The parameter is a 2D array

`int array[10][10];void passFunc(int a[][10]){    // ...}passFunc(array);`  


1. The parameter is an array containing pointers

`int *array[10];for(int i = 0; i < 10; i++)    array[i] = new int[10];void passFunc(int *a[10]) //Array containing pointers{    // ...}passFunc(array);`  


1. The parameter is a pointer to a pointer

`int **array = new int *[10];for(int i = 0; i <10; i++)    array[i] = new int[10];void passFunc(int **a){    // ...}passFunc(array);`  
vector initialization `// Initializing 2D vector "vect" with    vector< vector<`**`int`**`> > vect{{1, 2, 3},                              {4, 5, 6},                              {7, 8, 9}};// size of row`    **`int`** `row = 5;`    **`int`** `colom[] = { 5, 3, 4, 2, 1 };    // Create a vector of vector with size equal to row.    vector<vector<`**`int`**`> > vec(row);`          **`int`** `n = 3;    // Create a vector of size n with    // all values as 10.    vector<`**`int`**`> vect(n, 10);        vector<`**`int`**`> vect{ 10, 20, 30 };    // out: 10, 20, 30`   
[http://thispointer.com/creating-a-matrix-using-2d-vector-in-c-vector-of-vectors/](http://thispointer.com/creating-a-matrix-using-2d-vector-in-c-vector-of-vectors/)  
`//Will create a vector of 4 integers whose values will be 1.//Now to create a vector of 5 vectors in which each vector is initialized as above, we will use following syntax,  
std::vector <std::vector<`**`int`**`> > vec2D(5, std::vector<`**`int`**`>(4, 1));` **`for`**`(auto vec : vec2D){`    **`for`**`(auto x : vec)        std::`**`cout`**`<<x<<" , ";        std::`**`cout`** `<< std::endl;}`  
  
vector concatenation[https://stackoverflow.com/questions/201718/concatenating-two-stdvectors](https://stackoverflow.com/questions/201718/concatenating-two-stdvectors)`std::vector<int> first;std::vector<int> second;  
first.insert(first.end(), second.begin(), second.end());`  
dynamic array[http://www.fredosaurus.com/notes-cpp/newdelete/50dynamalloc.html](http://www.fredosaurus.com/notes-cpp/newdelete/50dynamalloc.html)**`a = new int[n]`**`;  // Allocate n ints and save ptr in a.for (int i=0; i<n; i++) {    a[i] = 0;    // Initialize all elements to zero.} // Use a as a normal array`**`delete [] a`**`;  // When done, free memory pointed to by a.a = NULL;     // Clear a to prevent using invalid memory reference.`  
online compiler [https://www.onlinegdb.com/online\_c++\_compiler](https://www.onlinegdb.com/online_c++_compiler)  
There is no append in vector. Use push\_back instead. Appends the given element value to the end of the container.[`std::vector`](http://en.cppreference.com/w/cpp/container/vector)`<`[`std::string`](http://en.cppreference.com/w/cpp/string/basic_string)`> numbers;numbers.push_back("abc");`  
vector usage[http://en.cppreference.com/w/cpp/container/vector](http://en.cppreference.com/w/cpp/container/vector)

* back, front

[http://en.cppreference.com/w/cpp/container/vector/back](http://en.cppreference.com/w/cpp/container/vector/back)

* push\_back
* pop\_back

`void` **`vectorname.pop_back()Parameters :`**`No parameters are passed`**`Result :`**`Removes the value present at the end or back of the given vector named as vectorname`

* insert in the front of the vector

`v.insert(v.begin(),value);https://stackoverflow.com/questions/36256216/add-an-element-into-the-beginning-of-an-vector-rest-elements-position-will-add?rq=1`

* = assignment : Assigns new contents to the container, replacing its current contents, and modifying its [size](http://www.cplusplus.com/vector::size) accordingly.

[http://www.cplusplus.com/reference/vector/vector/operator=/](http://www.cplusplus.com/reference/vector/vector/operator=/)`// vector assignment#include <iostream>#include <vector>  
int main (){  std::vector<int> foo (3,0);  std::vector<int> bar (5,0);  
  bar = foo;  foo = std::vector<int>();  
  std::cout << "Size of foo: " << int(foo.size()) << '\n';  std::cout << "Size of bar: " << int(bar.size()) << '\n';  return 0;}`Output:`Size of foo: 0Size of bar: 3`  
vector is empty[https://stackoverflow.com/questions/3863282/checking-whether-a-vector-is-empty](https://stackoverflow.com/questions/3863282/checking-whether-a-vector-is-empty)`if (Vector.empty()) { /* operations */ }`  
vector assign to a function by passing by reference  ``**`bool`** ``**`findTarget`**`(TreeNode* root,` **`int`** `k) {        vector<`**`int`**`> nums;        inorder(root, nums);        ...    }`        **`void`** ``**`inorder`**`(TreeNode* root, vector<`**`int`**`>`**`&`** `nums){        ...            }`  
2D vector example`// declare 2D vectorvector< vector<int> > myVector;// make new row (arbitrary example)vector<int> myRow(1,5);myVector.push_back(myRow);// add element to rowmyVector[0].push_back(1);`[https://stackoverflow.com/questions/9694838/how-to-implement-2d-vector-array?utm\_medium=organic&utm\_source=google\_rich\_qa&utm\_campaign=google\_rich\_qa](https://stackoverflow.com/questions/9694838/how-to-implement-2d-vector-array?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)  
[http://www-h.eng.cam.ac.uk/help/tpl/languages/C++/vectormemory.html](http://www-h.eng.cam.ac.uk/help/tpl/languages/C++/vectormemory.html)

### list

[https://www.studytonight.com/cpp/stl/stl-container-list](https://www.studytonight.com/cpp/stl/stl-container-list)[https://thispointer.com/stdlist-tutorial-and-usage-details/](https://thispointer.com/stdlist-tutorial-and-usage-details/)  
  
  
loop control 

* terminating condition
* initial condition
* think first before coding  
* start = i, number = m
  * then, end = i+m \(not included\)

`for (int k=i;k<i+m;k++){}`  
templateConsider this function that swaps its two integer arguments:`void swap(int& x, int& y){  int tmp = x;  x = y;  y = tmp;}`If we also had to swap floats, longs, Strings, Sets, and FileSystems, we’d get pretty tired of coding lines that look almost identical except for the type. Mindless repetition is an ideal job for a computer, hence a function template:`template<typename T>void swap(T& x, T& y){  T tmp = x;  x = y;  y = tmp;}`  
hash in C++

unordered container ~ p.556 c++ primer 

* An unordered container is most useful when we have a key type for which there is no obvious ordering relationship among the elements. 
* Associative containers that use hashing rather than a comparison operation on keys to store and access elements. The performance of these containers depends on the quality of the hash function

**unordered\_map** Container with elements that are key–value pairs, permits only one element per key.[http://thispointer.com/unordered\_map-usage-tutorial-and-example/](http://thispointer.com/unordered_map-usage-tutorial-and-example/)example:`// Create an empty unordered_map        std::unordered_map<std::`**`string`**`,` **`int`**`> wordMap;        // Insert Few elements in map        wordMap.insert({ "First", 1 });        wordMap.insert({ "Second", 2 });        wordMap.insert({ "Third", 3 });`          
How check if a given key exists in a Map in C++[http://thispointer.com/how-check-if-a-given-key-exists-in-a-map-c/](http://thispointer.com/how-check-if-a-given-key-exists-in-a-map-c/)count\(\): returns the count of number of elements in map with key K. As map contains elements with unique key only. So, it will return 1 if key exists else 0.**`if`** `(wordMap.count("hat") > 0){        std::`**`cout`** `<< "'hat' Found" << std::endl;}`  
map[https://openframeworks.cc/ofBook/chapters/stl\_map.html](https://openframeworks.cc/ofBook/chapters/stl_map.html)  
initialize a map[https://en.cppreference.com/w/cpp/container/unordered\_map/operator\_at](https://en.cppreference.com/w/cpp/container/unordered_map/operator_at)`// count the number of occurrences of each word// (the first call to operator[] initialized the counter with zero)`    [`std::unordered_map`](http://en.cppreference.com/w/cpp/container/unordered_map)`<`[`std::string`](http://en.cppreference.com/w/cpp/string/basic_string)`, size_t>  word_map;    for (const auto &w : { "this", "sentence", "is", "not", "a", "sentence",                           "this", "sentence", "is", "a", "hoax"}) {        ++word_map[w];    }`  


* iterate a hash/map 

[https://thispointer.com/how-to-iterate-over-an-unordered\_map-in-c11/](https://thispointer.com/how-to-iterate-over-an-unordered_map-in-c11/)[https://thispointer.com/how-to-iterate-over-a-map-in-c/](https://thispointer.com/how-to-iterate-over-a-map-in-c/)  
**Queue**

[http://en.cppreference.com/w/cpp/container/queue](http://en.cppreference.com/w/cpp/container/queue)[https://www.geeksforgeeks.org/queue-cpp-stl/](https://www.geeksforgeeks.org/queue-cpp-stl/)`queue <`**`int`**`> g;g.push(10);cout << '\t' << g.front();g.pop();`**`while`** `(!g.empty()){  cout << '\t' << g.front();  g.pop();}`  
string

string to integer: stoi\(string\)c\_string to integer: atoi\(c\_string\)s\[0\] : a char

* string concatenates with char 

string + char`string a = "aa";a += 'c';//a = "aac"`

* string erase

`string str ("abcde");str.erase (3,1);                        //str.earse(position, length)//output: abce`

* string reverse

`std::reverse(s.begin(), s.end());`string’s element comparison[https://stackoverflow.com/questions/18794793/c-comparing-the-index-of-a-string-to-another-string](https://stackoverflow.com/questions/18794793/c-comparing-the-index-of-a-string-to-another-string)    `string test = "D";    if (test == str[4]) {     // This line causes the problems        cout << test << endl;    }    return 0;`You need to convert str\[4\] \(which is a char\) to a string before you can compare it to another string. Here's a simple way to do this`if (test == string(1, str[4])) {}`  
stack[http://www.cplusplus.com/reference/stack/stack/pop/](http://www.cplusplus.com/reference/stack/stack/pop/) `std::stack<int> mystack; for (int i=0; i<5; ++i) mystack.push(i); while (!mystack.empty()) {     std::cout << ' ' << mystack.top();     mystack.pop(); }`  
pair    `pair <`**`int`**`,` **`char`**`> PAIR1 ;    PAIR1.first = 100;    PAIR1.second = 'G' ;    cout << PAIR1.first << " " ;    cout << PAIR1.second << endl ;`Different ways to initialize pair:`pair  g1;         //defaultpair  g2(1, 'a');  //initialized,  different data typepair  g3(1, 10);   //initialized,  same data typepair  g4(g3);    //copy of g3`  
hpp/h/cpp[https://stackoverflow.com/questions/152555/h-or-hpp-for-your-class-definitions](https://stackoverflow.com/questions/152555/h-or-hpp-for-your-class-definitions)  
using   


### set 

[http://www.cplusplus.com/reference/set/set/set/](http://www.cplusplus.com/reference/set/set/set/)  `std::set<int> myset;    // set some initial values:  for (int i=1; i<=5; ++i) myset.insert(i*10);    // set: 10 20 30 40 50`  


* if a set contains an element 

[https://thispointer.com/c-how-to-check-if-a-set-contains-an-element-setfind-vs-setcount/](https://thispointer.com/c-how-to-check-if-a-set-contains-an-element-setfind-vs-setcount/)[https://en.cppreference.com/w/cpp/container/set/find](https://en.cppreference.com/w/cpp/container/set/find)`// search for the iterator of given string in setstd::set<std::string>::iterator it = setOfStrs.find("at");  
// Check if iterator it is validif (it != setOfStrs.end())  std::cout << "'at' found in set" << std::endl;`  
[http://lafstern.org/matt/col1.pdf](http://lafstern.org/matt/col1.pdf)  
set equal `set<int> a;set<int> b;a.insert(1);b.insert(1);if (a==b) cout << "yes" << endl;else cout << "no" << endl;//result: yes!`  


* set of vector 

It doesn’t apply to “unordered\_set”`#include <iostream>#include <vector>#include <set>using namespace std;  
int main(){    set<vector<int>> s;    vector<int> a{1,2,3};    vector<int> b{2,1,3};    s.insert(a);    cout << s.count(a) << endl;    //result : 1    cout << s.count(b) << endl;    //result : 0}`  
[https://stackoverflow.com/questions/5034211/c-copy-set-to-vector](https://stackoverflow.com/questions/5034211/c-copy-set-to-vector)Just use the constructor for the vector that takes iterators:`std::set<T> s;//...std::vector v( s.begin(), s.end() );`  
**Struct** 

Differences between a class and a struct in C++ are that structs have default public members and bases and classes have default private members and bases. Both classes and structs can have a mixture of public, protected and private members, can use inheritance and can have member functions.I would recommend using structs as plain-old-data structures without any class-like features, and using classes as aggregate data structures with private data and member functions.  
[https://www.fluentcpp.com/2017/06/13/the-real-difference-between-struct-class/](https://www.fluentcpp.com/2017/06/13/the-real-difference-between-struct-class/) a struct can have constructors, methods \(even virtual ones\), public, private and protected members, use inheritance, be templated… **just like a** **class**.  
 **convention**. There are some conventions out there that are fairly widespread and that follow a certain logic. Following these conventions gives you a way to express your intentions in code when designing a type, because as we’ll see in a moment, implementing it as a struct doesn’t convey the same message as implementing it as a class.  
reverse a vector There's a function std::reverse in the algorithm header for this purpose.`#include <vector>#include <algorithm>  
int main() {  std::vector<int> a;  std::reverse(a.begin(), a.end());  return 0;}`[https://stackoverflow.com/questions/8877448/how-do-i-reverse-a-c-vector](https://stackoverflow.com/questions/8877448/how-do-i-reverse-a-c-vector)  
complexity [https://stackoverflow.com/questions/181693/what-are-the-complexity-guarantees-of-the-standard-containers](https://stackoverflow.com/questions/181693/what-are-the-complexity-guarantees-of-the-standard-containers)[http://www.cplusplus.com/reference/algorithm/equal/](http://www.cplusplus.com/reference/algorithm/equal/)vector equality, v1 == v2?[http://www.techiedelight.com/check-two-vectors-equal-cpp/](http://www.techiedelight.com/check-two-vectors-equal-cpp/)  
priority\_queue[https://en.cppreference.com/w/cpp/container/priority\_queue](https://en.cppreference.com/w/cpp/container/priority_queue)`#include <queue>priority_queue<int,` [`std::vector`](http://en.cppreference.com/w/cpp/container/vector)`<int>,` [`std::greater`](http://en.cppreference.com/w/cpp/utility/functional/greater)`<int> > q2;for(int n : {1,8,5,6,3,4,0,9,7,2})  q2.push(n);// 0 1 2 3 4 5 6 7 8 9 Min in the top   
//default is Max heappriority_queue<int,` [`std::vector`](http://en.cppreference.com/w/cpp/container/vector)`<int>> q1;for(int n : {1,8,5,6,3,4,0,9,7,2})  q1.push(n);//9 8 7 6 5 4 3 2 1 0 Max in the top`[https://en.cppreference.com/w/cpp/utility/functional/greater](https://en.cppreference.com/w/cpp/utility/functional/greater)how to remember: greater return true if left &gt; right. That means “true” → swap in the queue.[https://stackoverflow.com/questions/16111337/declaring-a-priority-queue-in-c-with-a-custom-comparator](https://stackoverflow.com/questions/16111337/declaring-a-priority-queue-in-c-with-a-custom-comparator)comparison function [http://fusharblog.com/3-ways-to-define-comparison-functions-in-cpp/](http://fusharblog.com/3-ways-to-define-comparison-functions-in-cpp/)  
[https://stackoverflow.com/questions/15601973/stl-priority-queue-of-c-with-struct](https://stackoverflow.com/questions/15601973/stl-priority-queue-of-c-with-struct)`struct thing {    int a;    char b;    bool operator < (const thing& rhs) const {        return a < rhs.a;    }};std::priority_queue<thing> q;thing stuff = {42, 'x'};q.push(stuff);q.push(thing{4242, 'y'}); // C++11 onlyq.emplace(424242, 'z'); // C++11 only    thing otherStuff = q.top();q.pop()`  



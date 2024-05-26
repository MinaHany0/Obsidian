# Sequential Containers

- vector stack grid queue where elements are maintained in a sequence
- store or retrieve elements based on sequence
- they don't examine elements , they just store them
# Associative Containers
- Maps , Sets
- Not based on sequence but based on relationships
- efficient smart access
- they do examine elements in order to store and retrieve data from them efficiently

# Map Class
### Collection of key value pairs
- associates a key with a value
- retrieve the value associated with the key
### Usage
- constructor creates empty maps
- use add to insert a new pair
- access elements using "getValue"
- shorthand operator [].
- browse pairs using iterator or mapping function
### Useful for
dictionary , database, lookup table, document index,...
### Map Interface
```
template <type>
class Map{
	public :
	Map();
	~Map();
	int size();
	bool isEmpty();
	void add(string key , type value);
	void remove(string key);
	bool containsKey(string key);
	type getValue(stringKey);
};
```

- Map can store any type of value but always a string key
- Maps don't have a defined null return vale for each type, so when user asks for value of non existent string -> it issues an error (because it has no idea what to return)
- maps can be accessed by using the string as an index ```
		mapname[stringVarName]```
- the map key must be a string because the string has some unique C/Cs that help in finding and mapping elements

we can use a vector as a value type for the map as to retrieve multiple values from a single key

the map iterator iterates randomly

## the set Class:
set is like a set but its less equal brother
(5,3) is the same as (3.5)


### usage
constructor creates empty sets
has add / remove / /iterators to operate on members
handy for throwing sth in the map then checking if it's there later
has no shorthand operator , you can't say give me the 5th element
you can only fo operations on sets of same elementType

### useful features:
1- fast membership operations
2- coalesce duplicates : ignores duplication automatically 
3- high level ops
	ex: 	checking if sets of student course meet new course requirements
			make 2 sets and check intersection and remove them and then have remaining req.
		compound Boolean queries (AND / OR / NOT)
			example: finding words that happen to be in 2 file: make 2 sets and intersect them : give true / false
4. the blind operation does a blindly fast check - opposite to the vector where it checks all index one by one
whether the map has 1k or 1m entries

note:
the set operator is not as unpredictable as the map iterator because it uses some sorting internally to have its operation done very fast
the set internally sorts the elements (ascending order in the lecture)

Vector vs Set
- duplicates -> vector
- indexes -> vector
- you need random access to view 5th element -> vector
- you care about sequence -> vector

# WILL BE DISCONTINUED BECAUSE I CAN'T ACCESS ASSIGNMENTS FURTHER THAN LECTURE 1
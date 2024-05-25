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
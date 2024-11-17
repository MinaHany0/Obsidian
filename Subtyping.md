Source : last lecture in Coursera Washington course Programming languages part C 

subtyping is a feature that lets us use a subtype as an argument where it is expecting some type
like for example 
- T1 = {a: Tx , b: Ty}             # T1 is a record type of two fields: a field of type Tx and b of type Ty 
- T2 = {a: Tx, b: Ty, c: Tz}     # T1 is a record type of two fields: a field of type Tx and b of type Ty and c of type Tz
up till here if we allow this in our language type system there is no problem and our language is sound 

but if we allow in-depth subtyping which is as follow

- T1 = {a: {q : Tx} , b : Ty}
- T2 = {a: {q : Tx , w : Tz} , b: Ty}
if this kind of subtyping is allowed, then our type system is not sound because of MUTATION
how and why ?
- this is due to if we had a funcion to change the q field only of the a record of the T1 record
- then implicitly we are changing the type of the record "a" from one in "T2" to one inside "T1"

code 
```
fun change (T1:{a:{q:tx} , b:Ty}) =
	q = 5;
```
here we changed the type of the T2 passed without meaning to T1 because of mutation WHILE STILL BEING RECORDED IN THE MEMORY AS T2
- so this means if we try to check it as T2 is TYPECHECKS while it is T1
- if it got changed to T1, it would be FINE but it DOES NOT because of MUTATION
### Conclusion
we CAN NOT have in depth subtyping because it breaks the soundness of our programs
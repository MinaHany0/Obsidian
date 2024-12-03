# Module 11
this module is discussing the objects
- an object has 3 things : state, behavior and identity

State of an object
1. maybe valid or invalid based on some hidden constraints
	1. valid object date : 3 October 2024
	2. invalid object date: 31 June 2023
2. the state of an object is usually all of the static properties of the object and usually some of the dynamic value properties of the object
	1. Example : Fish has a static type (it type: Bolty, Tuna) <span style="color:rgb(255, 192, 0)">which cannot change</span> , but some dynamic property which changes with time (such as its age) <span style="color:rgb(255, 192, 0)">which always changes with time</span> 

Behavior of an object
- the behavior of an object is a set of properties
- for example the behavior of an employee is different from manager is different from HR while they are all employees (they are inheriting the same base class employee)
- <span style="color:rgb(255, 192, 0)">Push and pop define the LIFO Behavior of the queue</span> 
- <span style="color:rgb(255, 192, 0)">Push, Pop, Top. Empty define the queue behavior</span> 
	Behavior can be classified into
	1. Modifiers --> changes the state of the object (Push, Pop)
	2. Selector --> which access the state of the object (Top, Empty)
	3. Iterators --> which accesses all the elements with some specific orders
	4. Constructor
	5. Destructor

Identity of an Object
- the identity of an object defines the roles and responsibilities of the object
- an employee is different from lead , also different from executive
- must be distinguishable which can be approaches in 2 ways
	1. by an ID state property (unique property inside the object)
	2. by an ID on top of the object given by the framework used
		- this may not be used if you are not using a framework in your system
		- can be achieved by the address of the object (in C++) but if the object is relocated in memory, there is the risk of the identity changing and causing issues
# Module 12 Relationships between objects
the object must work together to provide an actual product
- in an airplane, the engine doesn't fly by itself

relationships are represented by links and the direction of the link is the way of action
you can have objects be 
- a Controller object (which only requests from other and no one requests from him such as a flow controller for a valve)
- a Server object (which always servers other and will ask no action of other objects such as the display panel)
- a Proxy object (which does both, such as the valve which receives action request from the flow controller and sends to display panel its state to show )

the relationship between objects must be concurrent
	for example multiple computers sending print orders to a printer
		can only be achieved by having mutual exclusion, else pages and data will get mixed
	Concurrency (mutual exclusion) can be achieved by 3 ways 
		1. sequential control: where the printer only receives 1 task at a time and the computers (clients) solve their problems outside
		2. guarded control: in which computers will send the print orders to another object which will make a queue for the printer this reducing to sequential behavior
		3. concurrent control: in which the printer itself has a spooler which performs the queueing and manages the mutual exclusion by itself (modern systems)
- <span style="color:rgb(255, 192, 0)">when this is done properly, the system is said to  be synchronized and concurrent.</span> 
### Aggregation relationship التمليك
![[OSSU OOAD-20241004225121945.webp]]
![[OSSU OOAD-20241005000200308.webp]]
here a system is classified with the relations (links, weak aggregation, strong aggregation)

# Module 13: Nature of  a Class: Interface and Implementation
## Contents of module:
- Design by Contract
- Interface
	- Stack
- Visibility
- Implementation
	- Stack
![[OSSU OOAD-20241006203545172.webp]]
![[OSSU OOAD-20241006203702307.webp]]
- CARS vs CAR Class
![[OSSU OOAD-20241006203754835.webp]]
 - you can represent the whole college as a class but it will be very complex and it will be very big and hard to analyze so it needs to be reasonable
 - a complex system thus needs to be abide by these rules
![[OSSU OOAD-20241006204133355.webp]]
![[OSSU OOAD-20241006204435178.webp]]
![[OSSU OOAD-20241006204924384.webp]]
![[OSSU OOAD-20241006210613454.webp]]
 - the interface is not defined ONLY by the methods, NO, you need to know the preconditions, postconditions  and side effect to be able to effectively design or use the class
- the second interface remove the need for the client to abide by the precondition so this is left for the designer to decide
![[OSSU OOAD-20241006211539203.webp]]
- example we may have a method that checks whether there is enough memory to add an element but this method doesn't need to be accessible to the client.
- if we put multiple classes in one package they can see each other 
![[OSSU OOAD-20241006220329881.webp]]
![[OSSU OOAD-20241006220850096.webp]]
![[OSSU OOAD-20241006221202225.webp]]
![[OSSU OOAD-20241006221328722.webp]]
# Module 14: Relationship among classes
![[OSSU OOAD-20241006221544224.webp]]
![[OSSU OOAD-20241006222229064.webp]]
![[OSSU OOAD-20241006222326366.webp]]
- the relationship between roses and daisy is more than rises and candles, so the relationship strength is a spectrum
![[OSSU OOAD-20241006222846680.webp]]![[OSSU OOAD-20241006224407210.webp]]
1 ---> 1..* (ex range 1..5)
![[OSSU OOAD-20241006224728218.webp]]![[OSSU OOAD-20241006224940266.webp]]![[OSSU OOAD-20241006225054970.webp]]
- leaf classes are called so because they have no more specialization
- a class is abstract if it's not possible if we can no instantiate an object from it.
- a non leaf may or may not be an abstract class but this is not good design
- a leaf class is always a concrete class
![[OSSU OOAD-20241006225807146.webp]]
- an ostrich is bird which cannot fly, while all birds can fly
- a square is a restricted rectangle
so keep in mind that inheritance doesn't always mean extension, it could mean restriction

![[OSSU OOAD-20241007204740656.webp]]
we can NOT apply getNumberOfWheels for the base class Vehicles because it is an abstract class.

- getNumberOfWheels can Not be implemented in vehicle
- drive can Not be implemented in two wheelers or its peers
![[OSSU OOAD-20241007205804891.webp]]
![[OSSU OOAD-20241007210148952.webp]]
![[OSSU OOAD-20241007210726492.webp]]
![[OSSU OOAD-20241007210844642.webp]]
we should try to avoid multiple and repeated inheritance in your design if possible
![[OSSU OOAD-20241007211158635.webp]]
![[OSSU OOAD-20241007211417637.webp]]
![[OSSU OOAD-20241007211446978.webp]]
- same concepts are repeating o both objects and classes
	- in objects we are talking about concrete entities that exist
	- while in classes we are talking about abstract planes of existence where objects will be created during runtime and within the lifetime of a class, several objects will be created, used and destroyed

# Module 15 How to build quality classes and objects
![[OSSU OOAD-20241007212006095.webp]]
- if 2 classes are very tightly coupled (using shared data rather heavily, maybe they should have been in the same class)-> meaning -> <span style="color:rgb(0, 176, 80)">inter-class coupling should be kept to a minimum</span>
- this contradicts with inheritance (because base and derived classes are tightly coupled) but inheritance is good because it gives us good hierarchy
- so you need to optimize between inheritance and loosely coupled classes 
Cohesion:
- whether the data inside one class should really be together?
- are we putting too much data into one class  ?
<span style="color:rgb(255, 192, 0)">Note: our goal is to have the traffic between models as low as possible while the traffic within the module to be high</span> 

sufficiency: for example don't make a double push method on your stack, it is against the minimalist aspect

completeness: if your stack doesn't have an EMPTY method, then your class design is incomplete 

<span style="color:rgb(255, 192, 0)">
NOTE: sufficiency and completeness complete each other</span> 
![[OSSU OOAD-20241007215811269.webp]]
![[OSSU OOAD-20241007215825561.webp]]
- don't make your functions too fine: like a function just to increment a value
- don't make it too course also, if I'm designing for a bank account management like one function where an account is created and the data is set and printed and secured with checksum then this method is too coarse.
- an example in stack is whether to have POP return the top element and remove it at same time, or make it into 2 methods (POP to remove and TOP to return)
	- <span style="color:rgb(255, 192, 0)">having POP remove and return is some kind of double work where in come cases I want to only remove (so better design is to have two seperate functions)</span> 
![[OSSU OOAD-20241007220746518.webp]]
![[OSSU OOAD-20241007221017643.webp]]
![[OSSU OOAD-20241007221539920.webp]]
![[OSSU OOAD-20241007223903487.webp]]
![[OSSU OOAD-20241007224013083.webp]]![[OSSU OOAD-20241007224119546.webp]]
![[OSSU OOAD-20241007224358877.webp]]
![[OSSU OOAD-20241007224600880.webp]]


# Tutorial 1
Leave management system requirement gathering video

# Module 16 How to identify objects and classes
![[OSSU OOAD-20241008225613612.webp]]
![[OSSU OOAD-20241008225712832.webp]]
![[OSSU OOAD-20241008225850342.webp]]
![[OSSU OOAD-20241008230130857.webp]]
![[OSSU OOAD-20241008230149547.webp]]
![[OSSU OOAD-20241008230237576.webp]]
![[OSSU OOAD-20241008230456238.webp]]
- once we identify the characteristic we are clustering based on, we can identify the key abstraction details 
![[OSSU OOAD-20241008230646656.webp]]
![[OSSU OOAD-20241009210633541.webp]]
- structural clustering is immediately visible, but conceptual clustering has some hidden property that is not visible at first look
![[OSSU OOAD-20241009211706075.webp]]
- example : games have no specific characteristic that identify it as a game so we can use the prototyping
	- for example we have 4 prototypes of games  : chess, soccer, wrestling, swimming, 
	- so when somebody asks if Chinese checkers is a game ? we check its similarities to our prototypes and then we classify it in the same cluster of that of chess (board games).
![[OSSU OOAD-20241009212552890.webp]]
- if we make each type a separate class, then our system is too complex
- we need to find and look for the "Key Abstractions"
- we can find them by "<span style="color:rgb(255, 192, 0)">Discovering</span>" the vocabulary of the domain specific system
- we need to "<span style="color:rgb(255, 192, 0)">Invent</span>" the domain specific abstractions but with the developer tools
![[OSSU OOAD-20241009213024814.webp]]
- classification by association is using '<span style="color:rgb(255, 192, 0)">prototyping</span>'
- <span style="color:rgb(210, 127, 127)">ONCE CLASSIFICATION IS FINISHED, WE CAN GET TO DEFINING THE KEY ABSTRACTIONS FOR DESIGNING THE CLASS</span> 
- Remember that software design is an refinement process using a lot of iteration, getting domain knowledge, talking again to the customer, reviewing the clustering and refinement of key abstraction and repeating the process many times.

- Remember : that between two competing designs, there maybe no clear winner, each has its own pros and cons. and this is a matter of refinement and of personal judgement.
# Module 17: Identification of objects, classes and relationships in LMS
![[OSSU OOAD-20241009214831445.webp]]
![[OSSU OOAD-20241009215001006.webp]]
![[OSSU OOAD-20241009215018950.webp]]
![[OSSU OOAD-20241009215036814.webp]]
![[OSSU OOAD-20241009220137782.webp]]
- at this stage
![[OSSU OOAD-20241009220156654.webp]]
 -lets first check all the vocabulary and identify the attributes (attributes are characteristics that only have a value but don't have a behavior)
![[OSSU OOAD-20241009220339086.webp]]
![[OSSU OOAD-20241009221305663.webp]]
![[OSSU OOAD-20241009221508802.webp]]
![[OSSU OOAD-20241009221735662.webp]]
- then we perform behavioral clustering
![[OSSU OOAD-20241009221817226.webp]]
- we need to look for what happens in the system.
![[OSSU OOAD-20241009222054864.webp]]
![[OSSU OOAD-20241009222803060.webp]]
# Module 18: Identification of object classes and relationships
![[OSSU OOAD-20241009223039003.webp]]
- here we would be looking for actions (verb)
![[OSSU OOAD-20241010212620614.webp]]
- we need to take into consideration if certain verbs are repeated by many agents, then this is a possible case of reusability 
- the verb in many case has a subject and an object in the linguistic sense, so we would be able to extract the expected object using the action

![[OSSU OOAD-20241010213018503.webp]]
- all verbs are colored, we need to extract the verbs from our business model
![[OSSU OOAD-20241010213101900.webp]]
ex: credited, joining, prorated, 
cannot be carried over-> primary verb: carry over and auxiliary verb is cannot be (negative)

![[OSSU OOAD-20241010213613964.webp]]
after cleaning
![[OSSU OOAD-20241010213728136.webp]]
 - now lets try to analyze the verb associated with its subject class
![[OSSU OOAD-20241010214403941.webp]]
 - some actions are core responsibilities of all employee
![[OSSU OOAD-20241010214647815.webp]]
![[OSSU OOAD-20241010214724368.webp]]
![[OSSU OOAD-20241010215351972.webp]]![[OSSU OOAD-20241010215730011.webp]]

# Module 19: Identification of objects, classes, relationships part 3 
![[OSSU OOAD-20241010221157530.webp]]
- we are trying to extract the collaboration between the classes and the modularization of the system
![[OSSU OOAD-20241010221431620.webp]]
![[OSSU OOAD-20241010221442038.webp]]
![[OSSU OOAD-20241010221554654.webp]]
![[OSSU OOAD-20241010221603343.webp]]
![[OSSU OOAD-20241010221620120.webp]]
![[OSSU OOAD-20241010223057705.webp]]
![[OSSU OOAD-20241010223259207.webp]]
- after doing so, lots of repetitions will appear, then we need to filter them
![[OSSU OOAD-20241010223434299.webp]]
- modularization is another exercise, where we try to group the software components into modules
- we are trying to maximize the intra-module interactions and minimize the inter-module interactions 
- if so is done, then modularization is successful.

if intra-module interaction is more than inter-module interactions, then the design failed and we should change the module structure and group the interactions together
![[OSSU OOAD-20241010225848168.webp]]
![[OSSU OOAD-20241010225934303.webp]]
after further investigation
![[OSSU OOAD-20241010230432859.webp]]
Final Look:
![[OSSU OOAD-20241010230654590.webp]]
![[OSSU OOAD-20241015203406930.webp]]

# Module 20: Identification of classes, objects and relationships
![[OSSU OOAD-20241015203612979.webp]]
![[OSSU OOAD-20241015203704202.webp]]
then after we refined these classes even more by saying there is a hierarchy of responsibilities which forms a chain
![[OSSU OOAD-20241015203747930.webp]]

now we need to take that further and apply that to the leave class
![[OSSU OOAD-20241015203857270.webp]]
we are trying to check all the common actions and try to make a hierarchy or the common factors and difference between leaves

![[OSSU OOAD-20241015204553283.webp]]
![[OSSU OOAD-20241015204640299.webp]]
- here we are trying to tabulate the data of the design so we can refine and optimize it further if possible
![[OSSU OOAD-20241015205529532.webp]]
 - here we notice that duty leave has no common properties with any other leave (all is N/A), so we try to extract a property which differs it from other leaves, which is exactly what we done by the two properties (Not on duty and On-Duty)
![[OSSU OOAD-20241015205856112.webp]]

- so all the red classes are real classes and blue classes are abstract classes
- we will never have an en-cashable leave on its own but we will have leaves with its properties
![[OSSU OOAD-20241015210307965.webp]]

- the hierarchy of the system classes is very critical, and if the hierarchy is not solid then all the system is not on solid grounds


- coming to the quality measure, we have made some good progress in terms of coupling, completeness and primitiveness

![[OSSU OOAD-20241015210558873.webp]]


# Module 21: Overview of  UML
- unified modelling language is a language where we can put our extraction of an OOP system of objects, classes and relationships
![[OSSU OOAD-20241015211320953.webp]]
![[OSSU OOAD-20241015211331422.webp]]
![[OSSU OOAD-20241015211738873.webp]]
![[OSSU OOAD-20241015212228253.webp]]
![[OSSU OOAD-20241015212311658.webp]]
![[OSSU OOAD-20241015212419448.webp]]
![[OSSU OOAD-20241015212546733.webp]]

professor said each diagram will be explained separately later, so now we only pass by them without explaining in details

![[OSSU OOAD-20241015212747700.webp]]
- empty arrow represents an IS_A relationship
![[OSSU OOAD-20241015221308916.webp]]
![[OSSU OOAD-20241015221458972.webp]]
![[OSSU OOAD-20241015221620287.webp]]
![[OSSU OOAD-20241015221740519.webp]]
![[OSSU OOAD-20241015221927626.webp]]
![[OSSU OOAD-20241015221954068.webp]]

# Module 22: SDLC Phases and UML Diagrams

- we call it a life cycle, because once we reach the last phase we need to start from the first phase again and so on
![[OSSU OOAD-20241015222531021.webp]]
![[OSSU OOAD-20241015222610922.webp]]
![[OSSU OOAD-20241015223253658.webp]]
- so all our UML diagrams will be output of analysis and design and will be the input for the implementation phase
![[OSSU OOAD-20241015223443311.webp]]
- designing the interface doesn't necessarily mean GUI, maybe sound interface or keyboard interface only or .......
![[OSSU OOAD-20241015223620867.webp]]
- the rhombus mean aggregation and here it means tat requirement model is union of  3 things

![[OSSU OOAD-20241015223807094.webp]]
![[OSSU OOAD-20241015224005020.webp]]
![[OSSU OOAD-20241015224158345.webp]]

![[OSSU OOAD-20241022220114314.webp]]
- high level design is specifying what methods are in the class
- but the low level design is refining on the high level design to specify the algorithm used for the method, what are the data members in the class.

![[OSSU OOAD-20241022220346821.webp]]
- component diagrams tell which components we have (leave component, executive component, ...)
- deployment diagram: how to layout these components in the system
- architectural description: before this meant the English description of network diagram: how the server and clients set up, front ends, cables ...., but now we are supposed to lay this information in form of diagrams to be more easily adopted in the system

![[OSSU OOAD-20241022220819866.webp]]


# Module 23: Use Case Diagrams
![[OSSU OOAD-20241022221146806.webp]]
![[OSSU OOAD-20241022221418907.webp]]
![[OSSU OOAD-20241022221525668.webp]]
![[OSSU OOAD-20241022221537304.webp]]
![[OSSU OOAD-20241022223049665.webp]]
![[OSSU OOAD-20241022223159265.webp]]
secondary is one who makes sure system is working correctly like an administrator
![[OSSU OOAD-20241022223331075.webp]]
![[OSSU OOAD-20241022223417027.webp]]
there are actors which initiate the action like those marked
![[OSSU OOAD-20241022223451940.webp]]
![[OSSU OOAD-20241022223655451.webp]]
- remember that the use case is used at the very beginning of the project at the requirement phase
- so at this point you have no other diagrams, so you may not be able to express everything in the first sit, but no problem
![[OSSU OOAD-20241022223854065.webp]]
![[OSSU OOAD-20241022223909385.webp]]
![[OSSU OOAD-20241022224107828.webp]]
optimistic flow is the designer saying "if everything goes right, this is what should happen"
![[OSSU OOAD-20241022224700882.webp]]

# Module 24: Use Case Diagrams Part 2
![[OSSU OOAD-20241022224809545.webp]]
![[OSSU OOAD-20241022224957815.webp]]
![[OSSU OOAD-20241022225008669.webp]]
![[OSSU OOAD-20241022225512324.webp]]

![[OSSU OOAD-20241022225927143.webp]]
![[OSSU OOAD-20241022230018690.webp]]
![[OSSU OOAD-20241022230049988.webp]]
![[OSSU OOAD-20241022230302430.webp]]
![[OSSU OOAD-20241022230351487.webp]]
extends is the additional of conditions of different use cases to a base use case
![[OSSU OOAD-20241022230650814.webp]]
![[OSSU OOAD-20241022230949637.webp]]
![[OSSU OOAD-20241022231156216.webp]]
act on leave - in itself is not an action but it is a generalization

![[OSSU OOAD-20241022231307503.webp]]
![[OSSU OOAD-20241022231507892.webp]]

# Module 24
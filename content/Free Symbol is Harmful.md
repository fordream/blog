Title:Free Symbol is Harmful
Date:2015-08-08
Category:编程语言

#What is Free Variable?

　　"Free" is relative to "Bound"。Function parameters are "bound" to a function; Local variables/functions/classes are "bound" to a function. A variable which is defined out of a function is "free" for this function.

 

#Why is Free variable harmful?

　　Free variables make a function depend on outside scopes. When a programer reads a function with some free variables, He/She has to go to the definition of a free variable to see what it means. Furthermore, He/She will worry about whether there are other operations on this variable at somewhere else.

　  Personally, in terms of programming, I would rather to know what a function does, explicitly from the parameters I give it. Read/Write operations of free variables inside a function are indeed implicit operations, which is like undercurrent water, you never know how it flows(unless dive in to read through all the codes).

 

#Functional programming cuts down Free variables

　　Most functional programming languages do limitations on variable assignment(Side Effects). Although I think it's a "Hypercorrection", It does cuts down free variables. In functional programming, functions are much like state transformations, which is quite direct and expressive.  Data flows are quite direct and expressive in this way.
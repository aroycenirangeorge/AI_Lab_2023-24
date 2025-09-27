# Ex.No: 10  Logic Programming –  Simple queries from facts and rules
### DATE: 27-09-2025                                                                           
### REGISTER NUMBER : 212223060231
### AIM: 
To write a prolog program to find the answer of query. 
###  Algorithm:
 Step 1: Start the program <br> 
 Step 2: Convert the sentence into First order Logic  <br> 
 Step 3:  Convert the sentence into Horn clause form  <br> 
 Step 4: Add rules and predicates in a program   <br> 
 Step 5:  Pass the query to program. <br> 
 Step 6: Prolog interpreter shows the output and return answer. <br> 
 Step 8:  Stop the program.
### Program:
### Task 1:
Construct the FOL representation for the following sentences <br> 
1.	John likes all kinds of food.  <br> 
2.	Apples are food.  <br> 
3.	Chicken is a food.  <br> 
4.	Sue eats everything Bill eats. <br> 
5.	 Bill eats peanuts  <br> 
   Convert into clause form and Prove that John like Apple by using Prolog. <br> 
### Program:
```pddl
likes(john,X):-
food(X).
eats(bill,X):-
eats(sue,X).
eats(Y,X):-
food(X).
eats(bill,peanuts).
food(apple).
food(chicken).
food(peanuts).
```


### Output:
<img width="1071" height="752" alt="image" src="https://github.com/user-attachments/assets/e98453bf-d7a3-48fc-8c57-e993e07b21a4" />


### Task 2:
Consider the following facts and represent them in predicate form: <br>              
1.	Steve likes easy courses. <br> 
2.	Science courses are hard. <br> 
3. All the courses in Have fun department are easy <br> 
4. BK301 is Have fun department course.<br> 
Convert the facts in predicate form to clauses and then prove by resolution: “Steve likes BK301 course”<br> 

### Program:
```pddl
likes(steve,X):-
easycourse(X).
hard(sciencecourse).
easycourse(X):-
course(X,dept(havefun)).
course(bk301,dept(havefun)).
```

### Output:
<img width="1073" height="382" alt="image" src="https://github.com/user-attachments/assets/d636106f-3152-402e-a19a-e04e68e11739" />



### Task 3:
Consider the statement <br> 
“This is a crime for an American to sell weapons to hostile nations. The Nano , enemy of America has some missiles and its missiles were sold it by Colonal West who is an American” <br> 
Convert to Clause form and prove west is criminal by using Prolog.<br> 
### Program:
```pddl
criminal(X):-
american(X),
weapon(Y),
hostile(Z),
sells(X,Y,Z).
weapon(Y):-
missile(Y).
hostile(Z):-
enemy(Z,X).
sells(west,Y,nano):-
missile(Y),
owns(nano,Y).
missile(m).
owns(nano,m).
enemy(nano,america).
american(west).
```


### Output:
<img width="1068" height="406" alt="image" src="https://github.com/user-attachments/assets/6255dcbb-2e50-457b-92e3-2049eb93514b" />

### Result:
Thus the prolog programs were executed successfully and the answer of query was found.

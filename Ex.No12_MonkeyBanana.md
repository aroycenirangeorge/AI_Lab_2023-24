# Ex.No: 12  Planning –  Monkey Banana Problem
### DATE:  27-09-2025                                                                          
### REGISTER NUMBER : 212223060231
### AIM: 
To find the sequence of plan for Monkey Banana problem using PDDL Editor.
###  Algorithm:
Step 1:  Start the program <br> 
Step 2 : Create a domain for Monkey Banana Problem. <br> 
Step 3:  Create a domain by specifying predicates. <br> 
Step 4: Specify the actions GOTO, CLIMB, PUSH-BOX, GET-KNIFE, GRAB-BANANAS in Monkey Banana problem.<br>  
Step 5:   Define a problem for Monkey Banana problem.<br> 
Step 6:  Obtain the plan for given problem.<br> 
Step 7: Stop the program.<br> 
### Program:

```
 (define (domain monkey)
 (:requirements :strips)
 (:constants monkey box knife bananas glass waterfountain)
 (:predicates (location ?x)
 (on-floor)
 (at ?m ?x)
 (hasknife)
 (onbox ?x)
 (hasbananas)
 (hasglass)
 (haswater))
 ;; movement and climbing
 (:action GO-TO
 :parameters (?x ?y)
 :precondition (and (location ?x) (location ?y) (on-floor) (at monkey ?y))
 :effect (and (at monkey ?x) (not (at monkey ?y))))
 (:action CLIMB
 :parameters (?x)
 :precondition (and (location ?x) (at box ?x) (at monkey ?x))
 :effect (and (onbox ?x) (not (on-floor))))
 (:action PUSH-BOX
 :parameters (?x ?y)
 :precondition (and (location ?x) (location ?y) (at box ?y) (at monkey ?y)
 (on-floor))
 :effect (and (at monkey ?x) (not (at monkey ?y))
 (at box ?x) (not (at box ?y))))
 ;; getting bananas
 (:action GET-KNIFE
 :parameters (?y)
 :precondition (and (location ?y) (at knife ?y) (at monkey ?y))
 :effect (and (hasknife) (not (at knife ?y))))
 (:action GRAB-BANANAS
 :parameters (?y)
 :precondition (and (location ?y) (hasknife)
 (at bananas ?y) (onbox ?y))
:effect (hasbananas))
 ;; getting water
 (:action PICKGLASS
 :parameters (?y)
 :precondition (and (location ?y) (at glass ?y) (at monkey ?y))
 :effect (and (hasglass) (not (at glass ?y))))
 (:action GETWATER
 :parameters (?y)
 :precondition (and (location ?y) (hasglass)
 (at waterfountain ?y)
 (at monkey ?y)
 (onbox ?y))
 :effect (haswater)))
```

### Input 

```
(define (problem pb1)
 (:domain monkey)
 (:objects p1 p2 p3 p4 bananas monkey box knife)
 (:init (location p1)
 (location p2)
 (location p3)
 (location p4)
 (at monkey p1)
 (on-floor)
 (at box p2)
 (at bananas p3)
 (at knife p4)
 )
 (:goal (and (hasbananas)))
 )
```

### Output/Plan:

<img width="609" height="580" alt="image" src="https://github.com/user-attachments/assets/d2863905-60ee-4fbd-95dc-58c7694936e5" />
<img width="585" height="499" alt="image" src="https://github.com/user-attachments/assets/f8a59cad-1d57-485e-9766-5758d6e94088" />
<img width="574" height="555" alt="image" src="https://github.com/user-attachments/assets/811ea945-e9d8-4aa3-b9ce-f39b3d905eb5" />
<img width="592" height="650" alt="image" src="https://github.com/user-attachments/assets/6ed7d49d-d6a5-4355-a23c-cc1fb39b5652" />
<img width="581" height="548" alt="image" src="https://github.com/user-attachments/assets/90406771-6920-4270-a05f-e0206cf930c0" />
<img width="580" height="462" alt="image" src="https://github.com/user-attachments/assets/3f3a78f8-a2f2-41b4-a58f-b2440c24b30e" />



### Result:
Thus the plan was found for the initial and goal state of given problem.

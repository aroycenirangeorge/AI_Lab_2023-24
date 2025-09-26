# Ex.No: 11  Planning –  Block World Problem 
### DATE:                                                                            
### REGISTER NUMBER : 
### AIM: 
To find the sequence of plan for Block word problem using PDDL  
###  Algorithm:
Step 1 :  Start the program <br>
Step 2 : Create a domain for Block world Problem <br>
Step 3 :  Create a domain by specifying predicates clear, on table, on, arm-empty, holding. <br>
Step 4 : Specify the actions pickup, putdown, stack and un-stack in Block world problem <br>
Step 5 :  In pickup action, Robot arm pick the block on table. Precondition is Block is on table and no other block on specified block and arm-hand empty.<br>
Step 6:  In putdown action, Robot arm place the block on table. Precondition is robot-arm holding the block.<br>
Step 7 : In un-stack action, Robot arm pick the block on some block. Precondition is Block is on another block and no other block on specified block and arm-hand empty.<br>
Step 8 : In stack action, Robot arm place the block on under block. Precondition is Block holded by robot arm and no other block on under block.<br>
Step 9 : Define a problem for block world problem.<br> 
Step 10 : Obtain the plan for given problem.<br> 
     
### Program:
```
(define (domain blocksworld)
 (:requirements :strips :equality)
 (:predicates (clear ?x)
 (on-table ?x)
 (arm-empty)
 (holding ?x)
 (on ?x ?y))
 (:action pickup
 :parameters (?ob)
 :precondition (and (clear ?ob) (on-table ?ob) (arm-empty))
 :effect (and (holding ?ob) (not (clear ?ob)) (not (on-table ?ob))
 (not (arm-empty))))
 (:action putdown
 :parameters (?ob)
 :precondition (and (holding ?ob))
 :effect (and (clear ?ob) (arm-empty) (on-table ?ob)
 (not (holding ?ob))))
 (:action stack
 :parameters (?ob ?underob)
 :precondition (and (clear ?underob) (holding ?ob))
 :effect (and (arm-empty) (clear ?ob) (on ?ob ?underob)
 (not (clear ?underob)) (not (holding ?ob))))
 (:action unstack
 :parameters (?ob ?underob)
:precondition (and (on ?ob ?underob) (clear ?ob) (arm-empty))
 :effect (and (holding ?ob) (clear ?underob)
 (not (on ?ob ?underob)) (not (clear ?ob)) (not (arm-empty)))))
```

### Input 
```
Problem-1
     (define (problem pb1)
     (:domain blocksworld)
     (:objects a b)
     (:init (on-table a) (on-table b) (clear a) (clear b) (arm-empty))
     (:goal (and (on a b))))
```

```
Problem-2
     (define(problem pb3)
     (:domain blocksworld)
     (:objects a b c)
     (:init (on-table a) (on-table b) (on-table c)
     (clear a) (clear b) (clear c) (arm-empty))
     (:goal (and (on a b) (on b c))))
```

### Output/Plan:

![WhatsApp Image 2025-09-26 at 09 29 37_174f795b](https://github.com/user-attachments/assets/498d8727-4016-4bf3-bc84-656c83dae76a)

![WhatsApp Image 2025-09-26 at 09 29 59_f64e147e](https://github.com/user-attachments/assets/93f9fb2f-9df1-40f5-aaa3-78dad77d41c0)

![WhatsApp Image 2025-09-26 at 09 31 44_2f2b750b](https://github.com/user-attachments/assets/493378eb-7a95-43a6-a6dd-6a7ae6a96630)

![WhatsApp Image 2025-09-26 at 09 31 57_757571be](https://github.com/user-attachments/assets/c1cea842-3f32-43c6-8b39-b4f22aa6ebd8)

![WhatsApp Image 2025-09-26 at 09 32 11_ea94e0c5](https://github.com/user-attachments/assets/31d59577-d931-463e-a784-70e583692f8c)

![WhatsApp Image 2025-09-26 at 09 33 15_e063fd0a](https://github.com/user-attachments/assets/d724d4d8-a5e0-4549-a9e4-3bdefa8976ac)



### Result:
Thus the plan was found for the initial and goal state of block world problem.

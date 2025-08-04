## [Table of Contents](https://github.com/ZapCon1/KnowledgeBase.git)

### Macro Call Arguments 

| Argument | Variable# |
|----------|-----------|
|A         | #1        |
|B         | #2        |
|C         | #3        |
|D         | #7        |
|E         | #8        |
|F         | #9        |
|G         | -         |
|H         | #11       |
|I         | #4          |
|J         | #5        |
|K         | #6        |
|L         | -         |
|M         | 13        |
|N         | -         |
|O         | -         |
|P         | -         |
|Q         | #17       |
|R         | #18       |
|S         | #19       |
|T         | #20       |
|U         | #21       |
|V         | #22       |
|W         | #23       |
|X         | #24       |
|Y         | #25       |
|Z         | #26       |

### WCS Parameters 


| WCS              |  Parameters   |
|------------------|---------------|
| G54              | #5221 - #5226 |
| G55              | #5241 - #5246 |
| G56              | #5261 - #5266 |
| G57              | #5281 - #5286 |
| G58              | #5301 - #5206 |
| G59              | #5321 - #5226 |

To compute the register value in a macro, use this equation (where W is the WCS number): 

```
parameter# = 5221 + (W-54)*20 
```

### Extended WCS Parameteres 

The extended WCS start at #7000 - #7006 and increment by 20 for each new WCS value. 

| WCS              |  Parameters   |
|------------------|---------------|
| G54.1P1          | #7001 - #7006 |
| G54.1P2          | #7021 - #7026 |
| ...              | ...           |
| G54.1P48         | #7941 - #7946 |

or D00 controls, 300 extended WCS are available.

| WCS              |  Parameters     |
|------------------|-----------------|
| G54.1P1          | #14001 - #14006 |
| G54.1P2          | #14021 - #14026 |
| ...              | ...             |
| G54.1P48         | #19981 - #19986 |

Note: Most Brother macros expect a negative value when passing in an extended WCS offset number. 
So `G54.1P1` is referenced by `W-1` in a macro call. 

To compute the register value in a macro, use this equation (where W is the WCS number): 

```
parameter# = 7001 + (-W-1 * 20)
```
For D00:
```
parameter# = 14001 + (-W-1 * 20)
```

### Sample WCS Register Calculation in MACRO

``` 
(W - WCS OFFSET #23)

(FIND THE CORRECT WCS REGISTERS)


IF[#23GT0] GOTO1 (NORMAL WORK OFFSETS)
IF[#23LT0] GOTO2 (EXTENDED WORK OFFSETS)
#3000 = 6(BAD WORK OFFSET VALUE)

(NORMAL WORK OFFSETS)
N1 #100 = #[5221+[#23-54]*20]
#101 = #[5222+[#23-54]*20]
#102 = #[5223+[#23-54]*20]
GOTO3

(EXTENDED WORK OFFSETS)
N2 #100 = #[5221+[#23-54]*20] 
#101 = #[5222+[#23-54]*20]
#102 = #[5223+[#23-54]*20]
GOTO3

N3
```


### Positional Variables
Machine Coordinate System (Tool Offseet Included):

| Variable #     |  WCS Coordinate |
|----------------|-----------------|
| #5021          | X               |
| #5022          | Y               |
| #5023          | Z               |
| #5024~#5028    | Additional Axes |

Workpiece Coordinate System (Tool Offseet Included):

| Variable #     |  WCS Coordinate |
|----------------|-----------------|
| #5041          | X               |
| #5042          | Y               |
| #5043          | Z               |
| #5044~#5048    | Additional Axes |

Skip Signals (Tool Offseet Included):

| Variable #     |  WCS Coordinate  |
|----------------|------------------|
| #5061          | X                |
| #5062          | Y                |
| #5063          | Z                |
| #5064~#5068    | Additional Axes  |

### Usefull System Variables 

| Variable #     |  Description     |
|----------------|------------------|
| #11001~#11099  | T01~T99          |
| #11201~#11299  | T201~T299        |
| #4120          | T Code           |
| #4111          | H Code           |
| #3801 ~ #3804  | Workpiece counter 1 Count, Current, Completion, Ending|
| #3811 ~ #3814  | Workpiece counter 2 Count, Current, Completion, Ending|
| #3821 ~ #3824  | Workpiece counter 3 Count, Current, Completion, Ending|
| #3831 ~ #3834  | Workpiece counter 4 Count, Current, Completion, Ending|


### Useful G/M Codes

| Code        |  Description                   | Modal/Oneshot |
|-------------|--------------------------------|---------------|
| M159        | Disable lookahead (one block)  | One-Shot      |
| M211 ~ M214 | Workpiece Counter 1 ~ 4 set    | Modal         |
| M221 ~ M224 | Workpiece Counter 1 ~ 4 cancel | Modal         |
| M252 ~ M254 | Tap accel constant Hi/Med/Low  | Modal         |
| M300, M301  | Z-axis Perimeter Mode (Z hop)  | Modal         |
| M442, M443  | Unclamp, Clamp A axis          | Modal         |
| M442, M443  | Unclamp, Clamp A axis          | Modal         |
| M442, M443  | Unclamp, Clamp A axis          | Modal         |

### High Accuracy Machine Modes (M298)

| Code        |  Description     |
|-------------|------------------|
| M298 L0     | Off              |
| M298 L1     | Standard         |
| M298 L2     | Rough            |
| M298 L3     | Medium Rough     |
| M298 L4     | Medium Rough S   |
| M298 L5     | Finishing        |
| M298 L6     | Finishing S      |
| M298 L7     | Adjustment A     |
| M298 L8     | Adjustment B     |
| M298 L9     | Adjustment C     |
| M298 L21    | Accuracy Spec. A |
| M298 L22    | Accuracy Spec. B |
| M298 L23    | Accuracy Spec. C |



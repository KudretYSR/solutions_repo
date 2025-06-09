# Problem 1
1. Setup and Measurement:
Suspend the weight from the string fixed at a point.

Measure length 
𝐿
L from suspension point to center of mass of bob.

Record the resolution of measuring instrument (e.g., 1 mm = 0.001 m), and calculate length uncertainty as

𝛿
𝐿
=
resolution
2
δL= 
2
resolution
​
 
2. Data Collection:
Displace pendulum slightly (<15°) to avoid nonlinear effects.

Measure time 
𝑇
10
T 
10
​
  for 10 oscillations.

Repeat 10 times to get 10 measurements of 
𝑇
10
T 
10
​
 :

𝑇
10
,
1
,
𝑇
10
,
2
,
…
,
𝑇
10
,
10
T 
10,1
​
 ,T 
10,2
​
 ,…,T 
10,10
​
 
Calculate mean:

𝑇
ˉ
10
=
1
10
∑
𝑖
=
1
10
𝑇
10
,
𝑖
T
ˉ
  
10
​
 = 
10
1
​
  
i=1
∑
10
​
 T 
10,i
​
 
Calculate standard deviation:

𝑠
=
1
9
∑
𝑖
=
1
10
(
𝑇
10
,
𝑖
−
𝑇
ˉ
10
)
2
s= 
9
1
​
  
i=1
∑
10
​
 (T 
10,i
​
 − 
T
ˉ
  
10
​
 ) 
2
 
​
 
Uncertainty in mean time:

𝛿
𝑇
10
=
𝑠
10
δT 
10
​
 = 
10
​
 
s
​
 
3. Calculations:
Calculate period 
𝑇
T:

𝑇
=
𝑇
ˉ
10
10
T= 
10
T
ˉ
  
10
​
 
​
 
Uncertainty in 
𝑇
T:

𝛿
𝑇
=
𝛿
𝑇
10
10
δT= 
10
δT 
10
​
 
​
 
Calculate acceleration due to gravity 
𝑔
g from:

𝑔
=
4
𝜋
2
𝐿
𝑇
2
g= 
T 
2
 
4π 
2
 L
​
 
4. Uncertainty Propagation:
For 
𝑔
=
4
𝜋
2
𝐿
𝑇
2
g= 
T 
2
 
4π 
2
 L
​
 , partial derivatives:

∂
𝑔
∂
𝐿
=
4
𝜋
2
𝑇
2
∂L
∂g
​
 = 
T 
2
 
4π 
2
 
​
 
∂
𝑔
∂
𝑇
=
−
8
𝜋
2
𝐿
𝑇
3
∂T
∂g
​
 =− 
T 
3
 
8π 
2
 L
​
 
Combined uncertainty:

𝛿
𝑔
=
(
∂
𝑔
∂
𝐿
𝛿
𝐿
)
2
+
(
∂
𝑔
∂
𝑇
𝛿
𝑇
)
2
δg= 
( 
∂L
∂g
​
 δL) 
2
 +( 
∂T
∂g
​
 δT) 
2
 
​
 
Plugging in:

𝛿
𝑔
=
(
4
𝜋
2
𝑇
2
𝛿
𝐿
)
2
+
(
8
𝜋
2
𝐿
𝑇
3
𝛿
𝑇
)
2
δg= 
( 
T 
2
 
4π 
2
 
​
 δL) 
2
 +( 
T 
3
 
8π 
2
 L
​
 δT) 
2
 
​
 
5. Example Tabulated Data (Markdown):
Trial 
𝑖
i	Time for 10 Oscillations 
𝑇
10
,
𝑖
T 
10,i
​
  (s)
1	20.15
2	20.22
3	20.20
4	20.18
5	20.25
6	20.16
7	20.23
8	20.19
9	20.21
10	20.24

Parameter	Value	Uncertainty
Length 
𝐿
L	1.00 m	0.0005 m
Mean 
𝑇
10
T 
10
​
 	20.20 s	0.02 s
Period 
𝑇
T	2.02 s	0.002 s
Calculated 
𝑔
g	
4
𝜋
2
×
1.00
2.02
2
=
9.68
 
𝑚
/
𝑠
2
2.02 
2
 
4π 
2
 ×1.00
​
 =9.68m/s 
2
 	Calculated below
Uncertainty 
𝛿
𝑔
δg	—	Calculated below

6. Calculation of 
𝛿
𝑔
δg:
Using the above example:

𝐿
=
1.00
±
0.0005
 
𝑚
L=1.00±0.0005m

𝑇
=
2.02
±
0.002
 
𝑠
T=2.02±0.002s

Calculate:

∂
𝑔
∂
𝐿
=
4
𝜋
2
𝑇
2
=
39.48
4.08
≈
9.68
 
𝑚
𝑠
2
⋅
𝑚
∂L
∂g
​
 = 
T 
2
 
4π 
2
 
​
 = 
4.08
39.48
​
 ≈9.68 
s 
2
 ⋅m
m
​
 
∂
𝑔
∂
𝑇
=
−
8
𝜋
2
𝐿
𝑇
3
=
−
78.96
×
1.00
(
2.02
)
3
=
−
78.96
8.24
≈
−
9.58
 
𝑚
𝑠
3
∂T
∂g
​
 =− 
T 
3
 
8π 
2
 L
​
 =− 
(2.02) 
3
 
78.96×1.00
​
 =− 
8.24
78.96
​
 ≈−9.58 
s 
3
 
m
​
 
Calculate contributions:

(
∂
𝑔
∂
𝐿
𝛿
𝐿
)
2
=
(
9.68
×
0.0005
)
2
=
(
0.00484
)
2
=
2.34
×
10
−
5
( 
∂L
∂g
​
 δL) 
2
 =(9.68×0.0005) 
2
 =(0.00484) 
2
 =2.34×10 
−5
 
(
∂
𝑔
∂
𝑇
𝛿
𝑇
)
2
=
(
9.58
×
0.002
)
2
=
(
0.01916
)
2
=
3.67
×
10
−
4
( 
∂T
∂g
​
 δT) 
2
 =(9.58×0.002) 
2
 =(0.01916) 
2
 =3.67×10 
−4
 
So,

𝛿
𝑔
=
2.34
×
10
−
5
+
3.67
×
10
−
4
=
3.90
×
10
−
4
≈
0.0197
 
𝑚
/
𝑠
2
δg= 
2.34×10 
−5
 +3.67×10 
−4
 
​
 = 
3.90×10 
−4
 
​
 ≈0.0197m/s 
2
 
Therefore,

𝑔
=
9.68
±
0.02
 
𝑚
/
𝑠
2
g=9.68±0.02m/s 
2
 
7. Analysis and Discussion:
Comparison: The standard 
𝑔
=
9.81
 
𝑚
/
𝑠
2
g=9.81m/s 
2
 . The measured value is close, but slightly lower, within uncertainty.

Resolution effect on 
𝐿
L: The uncertainty in length (
𝛿
𝐿
δL) is very small because of fine measurement tools (1 mm resolution). Length uncertainty contributes less to total uncertainty.

Variability in timing: Stopwatch human reaction time can introduce variability (often ±0.1 s per measurement). Averaging 10 oscillations and repeating 10 times reduces this uncertainty significantly.

Assumptions:

Small-angle approximation (<15°) ensures 
𝑇
T formula validity.

Air resistance and friction at pivot are negligible.

String is massless and inextensible.

Experimental limitations:

Reaction time delay in stopwatch start/stop.

Measuring exact center of mass of bob.

String length changes due to stretch.

Pendulum swings are not perfectly planar.

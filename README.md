Download Link: https://assignmentchef.com/product/solved-40-319-homework4-hidden-markov-model-hmm
<br>
Figure 1: Hidden Markov Model (HMM)

Consider the HMM described in Figure 1. let the states of <em>H<sub>i </sub></em>be {1<em>,</em>2<em>,</em>3}, and the states of <em>O<sub>i </sub></em>be {”<em>the</em>”<em>,</em>”<em>cat</em>”<em>,</em>”<em>jumps</em>”<em>,</em>”<em>up</em>”}.

<ul>

 <li>Let <em>T </em>= 3. Write out the factorized form of <em>P</em>(<em>O</em><sub>1 </sub>= ”<em>the</em>”<em>,O</em><sub>2 </sub>= ”<em>cat</em>”<em>,O</em><sub>3 </sub>= ”<em>jumps</em>”) in terms of the initial, transition and emission probabilities. Specify all summations and products clearly.</li>

 <li>Show that if any initial parameter <em>π<sub>i </sub></em>or transition parameter <em>p<sub>ij </sub></em>is initially set to 0, then it will remain 0 in all subsequent updates of the EM algorithm.</li>

</ul>

<h1>Problem 2</h1>

In this problem, we will study the multi-armed (k = 10) bandit problem. Begin by including the following code in your script:

<strong>import </strong>numpy as np <strong>import </strong>matplotlib . pyplot as plt

T = 1000

<ul>

 <li>Define the greedy and UCB policy functions</li>

</ul>

def         e greedy (Q, N, t ,         e ):

. . .

def UCB(Q, N, t ,         c ):

. . .

which both take in <em>Q</em>, an array representing the action-values, <em>N</em>, an array representing the number of times different actions have been taken, <em>t</em>, the total number of actions taken thus far, and finally a policy-specific parameter.

<ul>

 <li>Write a function that performs one run (1000 time steps), updates <em>Q </em>incrementally and records the reward received at each time step:</li>

</ul>

def testrun ( policy , param ): truemeans = np. random . normal (0 , 1 , 10) reward = np. zeros (T + 1)

Q = np. zeros (10)

. . .

r = np. random . normal( true means [ a ] ,         1)

. . .

return reward

At each time step, when action <em>a </em>is taken, the reward <em>r </em>is sampled from a normal distribution with mean <em>true means</em>[<em>a</em>] and standard deviation 1.

<ul>

 <li>Use the following function to average over 2000 runs and plot the results:</li>

</ul>

def main ():

aveg = np. zeros (T+1) aveeg = np. zeros (T+1) aveucb = np. zeros (T+1)

for    i       in range (2000):

g = test run ( e greedy , 0.0) eg = test run ( e greedy , # choose parameter ) ucb = test run (UCB, # choose parameter )

aveg += (g − ave g ) / ( i + 1) aveeg += (eg − ave eg ) / ( i + 1) aveucb += (ucb − ave ucb ) / ( i + 1)

t = np. arange (T + 1) plt . plot (t , ave g , ’b−’, t , ave eg , ’r −’, t , ave ucb , ’g−’) plt . show()

At approximately what value of <em> </em>does the -greedy method switch from being better than the greedy policy to being worse than it?

<h1>Problem 3: Robot vs Snakes</h1>

In this problem, we will simulate a robot navigating a room trying to find the exit. The robot is bleeding and loses 1 hitpoint for every step it takes before it finds the exit. To make matters worse, there are 2 snakes in the centre of the room. If the robot steps onto a square with a snake, the snake will bite it and cause it to lose 15 hitpoints! As the robot is terrified of being bitten, it is very nervous and does not strictly respond to commands; if told to move in a certain direction, it will only do so half the time. One quarter of the time it will instead move to the left of the commanded direction, and another quarter of the time it will move to the right of the commanded direction. Can you help train the robot to find its way out?

Begin by installing OpenAI’s gym module (pip install gym), and include the following code in your script.

<strong>import </strong>numpy as np <strong>import </strong>sys <strong>from </strong>gym. envs . toy text <strong>import </strong>discrete UP = 0

RIGHT = 1

DOWN = 2

LEFT = 3

<table width="265">

 <tbody>

  <tr>

   <td width="118">GOAL = 4</td>

   <td width="99"><em># upper</em><em>−</em><em>right</em></td>

   <td width="49"><em>corner</em></td>

  </tr>

  <tr>

   <td width="118">START = 20SNAKE1 = 7SNAKE2 = 17</td>

   <td width="99"><em># lower</em><em>−</em><em>l e f t</em></td>

   <td width="49"><em>corner</em></td>

  </tr>

 </tbody>

</table>

eps = 0.25

<strong>class </strong>Robot vs snakes world ( discrete . DiscreteEnv ):

<strong>def </strong>i n i t ( s e l f ): s e l f . shape = [5 , 5]

nS = np. prod( s e l f . shape )                  <em># total       number    of     states</em>

nA = 4                                       <em># total       number    of      actions      per     state</em>

MAXY = s e l f . shape [0]

MAXX = s e l f . shape [1]

P = {}

grid = np. arange (nS ). reshape ( s e l f . shape ) it = np. nditer ( grid , flags =[ ’ multi index ’ ])

<strong>while not </strong>it . finished : s = it . iterindex

y , x = it . multi index P[ s ] = {a : [ ] <strong>for </strong>a <strong>in range</strong>(nA)}

<table width="232">

 <tbody>

  <tr>

   <td width="139">is done = <strong>lambda </strong>s :<strong>if </strong>is done ( s ): reward = 0.0</td>

   <td width="93">s == GOAL</td>

  </tr>

  <tr>

   <td width="139"><strong>elif </strong>s == SNAKE1 <strong>or </strong>reward = −15.0</td>

   <td width="93">s == SNAKE2:</td>

  </tr>

 </tbody>

</table>

<strong>else </strong>:

reward = −1.0

<strong>if </strong>is done ( s ):

P[ s ] [UP] = [(1.0 ,         s ,       reward , True )]

P[ s ] [RIGHT] = [(1.0 ,         s ,       reward , True )]

P[ s ] [DOWN] = [(1.0 ,        s ,       reward , True )]

P[ s ] [LEFT] = [(1.0 , s , reward , True )] <strong>else </strong>:

nsup = s <strong>if </strong>y == 0 <strong>else </strong>s − MAXX nsright = s <strong>if </strong>x == (MAXX − 1) <strong>else </strong>s + 1

nsdown = s <strong>if </strong>y == (MAXY − 1) <strong>else </strong>s + MAXX

nsleft = s <strong>if </strong>x == 0 <strong>else </strong>s − 1

P[ s ] [UP] = [(1 − (2 ∗ eps ) , ns up ,                reward ,      is done ( ns up )) ,

(eps ,        nsright ,        reward ,          is done ( ns right )) ,

(eps ,        nsleft ,        reward ,          is done ( ns left ))]

P[ s ] [RIGHT] = [(1 − (2 ∗ eps ) ,                ns right ,        reward ,           is done ( ns right )) ,

(eps ,      nsup ,      reward ,        is done ( ns up )) ,

(eps , nsdown ,         reward ,         is done (ns down ))]

P[ s ] [DOWN] = [(1 − (2 ∗ eps ) , ns down ,               reward ,       is done (ns down )) ,

(eps ,        nsright ,        reward ,          is done ( ns right )) ,

(eps ,        nsleft ,        reward ,          is done ( ns left ))]

P[ s ] [LEFT] = [(1 − (2 ∗ eps ) ,                ns left ,        reward ,        is done ( ns left )) ,

(eps ,      nsup ,      reward ,        is done ( ns up )) ,

(eps , nsdown ,         reward ,         is done (ns down ))]

it . iternext ()

isd = np. zeros (nS) isd [START] = 1.0 s e l f .P = P <strong>super</strong>( Robot vs snakes world , s e l f ). i n i t (nS , nA, P, isd )

<strong>def      </strong>render ( s e l f ):

grid = np. arange ( s e l f .nS ). reshape ( s e l f . shape ) it = np. nditer ( grid , flags =[ ’ multi index ’ ])

<strong>while not </strong>it . finished : s = it . iterindex

y , x = it . multi index

<strong>if       </strong>s e l f . s == s :

output = ” R ”

<strong>elif </strong>s == GOAL:

output = ” G ”

<strong>elif </strong>s == SNAKE1 <strong>or </strong>s == SNAKE2:

output = ” S ” <strong>else </strong>:

output = ” o ”

<strong>if </strong>x == 0:

output = output . lstrip ()

<strong>if </strong>x == s e l f . shape [1] − 1:

output = output . rstrip () sys . stdout . write ( output )

<strong>if </strong>x == s e l f . shape [1] − 1: sys . stdout . write (”
”) it . iternext () sys . stdout . write (”
”)

You can write

env = Robot vs snakes world ()

to start the environment, which is a 5 x 5 grid. Locations on the grid are numbered starting from 0 on the upper-left, and increasing in a row-wise manner; i.e. the upper-right is numbered 4 (exit/goal state), the lower-left (starting location of robot) is numbered 20, the lower-right corner is numbered

24, and so on. You can access the robot’s location at any time using env . s ,

and issue a command to move using env . step (DIR) ,

where <em>DIR </em>is <em>UP</em>, <em>DOWN</em>, <em>LEFT </em>or <em>RIGHT</em>. Finally,

env .p[ state ] [ action ]

returns a list of tuples, each corresponding to a possible next state <em>j </em>and of the form (probability of transitioning to state <em>j</em>, <em>j</em>, reward, goal state?).

<ul>

 <li>Begin by writing a function which performs value-iteration (note that there is no discountingof the rewards, i.e. the discount factor is 1):</li>

</ul>

<strong>def </strong>value iteration (env ): policy = np. zeros ([ env .nS , env .nA])

V = np. zeros (env .nS)

. . .

. . .

<strong>return </strong>policy , V

This function is to return the value function, as well as the greedy policy function. Print out both the policy and the value function.

<ul>

 <li>Next, use the policy function obtained above to navigate the robot through the room. At eachtime step, use env . render ()</li>

</ul>

to print out the layout of the room with the robot’s current location. Terminate the program when the robot reaches the exit.

<ul>

 <li>Does the robot try to avoid the snakes? If so, refer to the policy function obtained in (a) toexplain in what way it does so.</li>

</ul>
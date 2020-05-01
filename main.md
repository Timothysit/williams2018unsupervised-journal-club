---
title: Williams et al 2018. Unsupervised discovery of demixed, low-dimensional neural dynamics across multiple timescale through tensor component analysis.
separator: <!--h-->
verticalSeparator: <!--v-->
theme: white
revealOptions:
    transition: 'fade'
---




<style>
.reveal section img { background:none; border:none; box-shadow:none; }
.reveal h1 { font-size: 2em; }
.reveal h2 { font-size: 1em; }
</style>



<font size=4>

# Williams et al 2018: Unsupervised discovery of demixed, low-dimensional neural dynamics across multiple timescale through tensor component analysis.

</font>

![Tensor Component Analysis](./figures/williams2018unsupervised/tca_only.jpg)


<font size=3>

### Tim Sit

</font>

</font>

<font size=3>

### 2020 May 1

</font>

<!--v-->

## The paper

<iframe src="./pdfs/williams2018unsupervised.pdf"
width="100%" height=800>
</iframe>


<!--h-->



## Outline 

 1. History and background: Matrix and tensor factorisation methods
 2. Tensor component analysis for neural data
 3. Examples 
 4. Extensions and further reading


<!--h-->

## 1 | Matrix and tensor factorisation

<!--h-->


### We usually represent neural data as matrices 

Example 

$$
\mathbf{X} \in \mathbb{R}^{N \times T}
$$

where: 

 - $N$ is the number of neurons
 - $T$ is the number of time bins

<!--h-->



<font size=6>

### In matrix factorisation, we want to reconstruct the data from smaller matrices

</font> 

<font size=5>

$$
\mathbf{X} \approx \hat{\mathbf{X}} =  \mathbf{UV}^\intercal
$$



Another way to think about this is that we want to minimise the difference between the data and our approximation of it

</font>

$$
\min_{\mathbf{U}, \mathbf{V}} = \vert\vert \mathbf{X} - \mathbf{UV}^\intercal \vert\vert^2_{F}
$$

<font size=5>

Applied to neural data, we can think of our data matrix $\mathbf{X} \in \mathbb{R}^{N \times T}$, such that: <!-- .element: class="fragment current-visible" data-fragment-index="2" -->

 - $\mathbf{U} \in \mathbb{R}^{N \times R}$ will be our neuron factors, where $R$ is the number of factors (components) we want to reconstruct our data with <!-- .element: class="fragment current-visible" data-fragment-index="2" -->
 - $\mathbf{V} \in \mathbb{R}^{T \times R}$ will be our temporal factors <!-- .element: class="fragment current-visible" data-fragment-index="2" -->
 
 
 </font>

<font size=5>

Many dimensionality methods can be framed as solving the above problem (usually with additional regularisation or constraints) <!-- .element: class="fragment current-visible" data-fragment-index="3" -->

</font>


<font size=3>

A comment I found from Alex William's notes <!-- .element: class="fragment current-visible" data-fragment-index="3" -->

![Alex williams tSNE comment](./figures/alex-williams-tsne-comment.png) <!-- .element: class="fragment current-visible" data-fragment-index="3" -->

</font>


<!--v-->

### How this reconstruction happens

<font size=5>

One way to think about multiplying two matrices is that it is just the sum of the outer product of the columns of the first matrix and the rows of the second matrix:

$$
\begin{equation}
\begin{bmatrix}
\mathbf{u}_1 & \mathbf{u}_2 & ... & \mathbf{u}_n
\end{bmatrix}
\begin{bmatrix}
\mathbf{v}_1 \\\ \mathbf{v}_2 \\\ ... \\\  \mathbf{v}_n
\end{bmatrix} = \sum_i^N \mathbf{u}_i \otimes \mathbf{v}_i 
\end{equation}
$$

</font>

![trial-averaged matrix decomposition](./figures/williams2018unsupervised/figure-1a.png) <!-- .element  width="45%"--> 


<!--v-->


### Example

![USV example](./figures/tca-concepts/USV-example.svg)<!-- .element  width="100%"--> 


<!--v-->


### Principal Component Analysis (PCA) as minimising reconstruction error 

<font size=5>

The objective function of PCA can be written as 

</font>

$$
\min_{\mathbf{V}} \vert\vert \mathbf{X} - \mathbf{X}\mathbf{V}\mathbf{V}^\intercal \vert\vert^2_\mathrm{F}
$$

<font size=5>

subject to $\mathbf{V}$ being an orthogonal matrix, meaning that $\mathbf{C}$ is a square matrix with orthogonal columns and rows with unit length. More formally defined by the property that: $\mathbf{C}\mathbf{C}^\intercal = \mathbf{V}^\intercal \mathbf{V} = \mathbf{I}$

We can write our equation back to the familiar form of thinking about our reconstruction as just multiplyling two matrices if we set $\mathbf{U} = \mathbf{XV}$

</font>





<!--v-->

### Non-negative matrix factorisation (NMF) as minimising reconstruction error


<div id='left'>

![PCA face](./figures/PCA_Face.png)

</div>

<div id='right'>

![NMF face](./figures/NMF_Face.png)

</div>


<font size=3>

[Lee and Song 1999: Learning the parts of objecs by non-negative matrix factorizataion](https://www.nature.com/articles/44565)

</font>


<font size=5>

With the simple additional constraint that our matrices have to be zero or positive $\mathbf{U} \geq 0, \mathbf{V} \geq 0$. This has the advantage of giving factors that are (1) sparse and (2) positivitely combined

This will become relevant to the tensor component analysis method introduced in this paper because there is also a non-negative variant of Tensor Component Analysis.

</font>





<!--h-->

### Tensor and tensor decomposition 

<div id='left'>

![Tensor representation of data](./figures/tensor_data.png)

</div>

<div id='right'>



We can extend the idea of representing data as a "2D" (second order) matrix to a "3D" (third order) tensor:

$$
\boldsymbol{\mathcal{X}}  \in \mathbb{R}^{N \times T \times K}
$$

<font size=5>


where:

 - $N$ is the number of neurons
 - $T$ is the number of time points 
 - $K$ is the number of trials 


</font>
 
</div>

<!--v-->



#### History of tensor methods

<div id='left'>

![Tensor analysis history](./figures/linear-and-multilinear-methods-history.png) <!-- .element  width="120%"--> 

</div>

<div id='right'>

<font size=5>

 - Idea first introduced by Hitchcock 1927
 - Originally applied to chemometrics and psychometrics
 - Recently gain popularity through application in analysing videos and image of human faces
 
 
 </font>
 
 </div>


<!--v-->

#### Two main tensor decomposition methods 

<div id='left'>

CP (canonical polyadic) tensor decomposition 

![CP decomposition](./figures/CP-decomposition.png) <!-- .element  width="100%"--> 



<font size=5>

This is the method used by tensor component analysis.
Main effect: One neuron factor per temporal factor per trial factor. 

$\boldsymbol{\mathcal{X}} \approx \sum_{r=1}^{R} \mathbf{a}_r \circ \mathbf{b}_r \circ \mathbf{c}_r$


</font>

</div>
 
 <div id='right'>
 
Tucker tensor decomposition


![Tucker decomposition](./figures/tucker-decomposition.png) <!-- .element  width="100%"--> 


<font size=5>

Main effect: One neuron factor can be associated with multiple temporal / trial factors. But this makes interpretation difficult.

$\boldsymbol{\mathcal{X}} \approx \boldsymbol{\mathcal{G}} \times_1 \mathbf{A} \times_2 \mathbf{B} \times_3 \mathbf{C}$


</font>
 
 </div>
 
 

<!--v-->

### TCA vs. PCA: uniqueness of solution

PCA can reconstruct your data well (unique solution) if you assume: 

 1. Your factors are orthogonal 
 2. Your factors have large eigengaps (the magnitude of your factors are very different)

TCA can reconstruct you data well allowing for: 

 1. Your factors only have to be linearly independent 
 2. You have small eigengap 


<font size=4>

[Kruskal 1977: Linear independence is sufficient for tensor decomposition identifiability (for rank-3 tensors)](https://www.sciencedirect.com/science/article/pii/0024379577900696)
 
 Also see [Rhodes 2010: A concise proof of Kruskal's theorem on tensor decomposition](https://www.sciencedirect.com/science/article/pii/S0024379509006132)


</font>

<!--h-->

## 2 | Tensor Component Analysis 

<!--h-->

### The main selling point of TCA is you get a *trial factor*


![TCA and other methods](./figures/williams2018unsupervised/TCA-paper-figure-1.png) <!-- .element  width="90%"--> 


<!--h-->

<font size=6>

### TCA is equivalent to a feedforward neural network with gain modulation


</font>



<font size=5>

<div id='left'>

Feedfoward network 

- You have some latent factors as input (eg. movement, decision, stimulus etc.
- The activity of your neurons is some weighted combination of these latent factors 

 
Gain modulation <!-- .element: class="fragment" data-fragment-index="2" -->
 
- You assume that the shape of the time couse of each neuron remain the same across trials <!-- .element: class="fragment" data-fragment-index="2" -->
- But the amplitude of this time course is scaled depending on the trial <!-- .element: class="fragment" data-fragment-index="2" -->

</div> 

<div id='right'>

<center>

![TCA as neural network](./figures/williams2018unsupervised/TCA-as-neural-network.png) <!-- .element  width="30%"--> 

![Linear combination of inputs](./figures/tca-concepts/activity_as_linear_combination_of_inputs.png)  <!-- .element  width="70%"--> <!-- .element: class="fragment current-visible" data-fragment-index="1" -->

![Gain modulation](./figures/williams2018unsupervised/gain-modulation.png)  <!-- .element  width="70%"--> <!-- .element: class="fragment current-visible" data-fragment-index="2" -->



</center>

</div>

</font>

<!--v-->


### Demo of best-case scenario for TCA

![Base case scenario TCA](./figures/williams2018unsupervised/figure-2cde.png) <!-- .element  width="100%"-->



<!--v-->


### Does that mean TCA is not suitable for modelling recurrent networks?

Not necessarily.

![TCA to model simple RNN](./figures/williams2018unsupervised/figure-3-abcde.png) <!-- .element  width="100%"-->



<!--h-->



<font size=5>

### TCA + Time Warping 

</font>

<div id='left'>

<font size=5>

If you remember from a few months ago in Kevin's journal club:

[Williams et al 2019: Discovering Precise Temporal Patterns in Large-Scale Neural Recordings through Robust and Interpretable Time Warping]()


![Time warp paper abstract](./figures/time-warp-paper-abstract.png)  <!-- .element  width="80%"--> 



</font>

</div>

</div>

<div id='right'>

<font size=5>

Now you can do both time warping and TCA <p>&#128512;</p>

[Williams 2020: Combining tensor decomposition and time warping models for multi-neuronal spike train analysis](https://scholar.google.com/scholar?hl=en&as_sdt=0%2C5&q=williams+2020+combining+tensor&btnG=)

</font>

![TCA and time warp](./figures/TCA+TW-figure-1.png)





</div>





<!--v-->

<iframe src="./pdfs/williams2020combining.pdf"
width="100%" height=800>
</iframe>


<!--v--> 

<iframe border=0 frameborder=0 height=500 width=550
src="https://twitframe.com/show?url=https%3A%2F%2Ftwitter.com%2FSuryaGanguli%2Fstatus%2F1202637594606981120"
</iframe>

<!--h-->


## 3 | Examples 



<!--h-->

### Spatial navigation task 

<div id='left'>

![Spatial navigation task 1](./figures/williams2018unsupervised/figure-4a.png)

![Spatial navigation task labels](./figures/williams2018unsupervised/figure-4b.png)

</div>

<div id='right'>

<font size=5>

Recording using a miniature micro-endoscope in the medial prefrontal cortex whilst:

1. Mouse is placed either on the east or west of the maze 
2. Mouse then decide either to go north or go south 
3. Mouse gets water as reward or gets nothing (rule changes on different sessions)
4. Dataset: 282 neurons, 111 time points, 600 trials, $\boldsymbol{\mathcal{X}} \in \mathbb{R}^{282 \times 111 \times 600}$

</font>


</div>

<!--h-->


<font size=6>

#### TCA can reconstruct your data well with few parameters 


PSTH of individual neurons can be reconstructed well with 15 components

</font>





<div id='left'>

![Reconstruct position-selective neurons](./figures/williams2018unsupervised/figure-4c.png) <!-- .element  width="100%"-->

![Reconstruct choice-selective neurons](./figures/williams2018unsupervised/figure-4d.png) <!-- .element  width="100%"-->

</div>

<div id='right'>

![Number of components and reconstruction error](./figures/williams2018unsupervised/figure-4f.png) <!-- .element  width="100%"-->

</div>


<!--v-->

#### TCA can reconstruct your data well with few parameters 

<div id='left'>

![Model fit versus number of parameters](./figures/williams2018unsupervised/figure-4k.png) <!-- .element  width="100%"-->

</div>

<div id='right'>

<font size=5>

Parameters

  - Trial-average PCA: You take the average across trials, so only neural factor and temporal factor 
  - TCA / NTCA: Neural factor, temporal factor, trial factors
  - Concatenated PCA: Neural factor, and individual sets of temporal factor for each trial

</font>

</div>


<!--v-->

#### "How do I know TCA is not overfitting?" 

Method 1: cross-validate the reconstruction error


![TCA cross validation](./figures/williams2018unsupervised/figure-5-ab.png) <!-- .element  width="70%"--> <!-- .element: class="fragment current-visible" data-fragment-index="1" -->


![TCA cross validation part 2](./figures/williams2018unsupervised/figure-5c.png) <!-- .element  width="70%"--> <!-- .element: class="fragment current-visible" data-fragment-index="2" -->


Even with 10% of the data, they have 90 data points per free parameter. <!-- .element: class="fragment current-visible" data-fragment-index="2" -->


<!--v--> 


#### "How do I know TCA is not overfitting?" 

Method 2: check that the factors you obtain are similar across optimisations.

![TCA model similarity](./figures/williams2018unsupervised/figure-4-h.png) <!-- .element  width="45%"-->


<!--v--> 


#### "How do I know TCA is not overfitting?" 

Method 3: Look at how well you are fitting each neuron depending on how reliable they fire 

<div id='left'>

![TCA neuron variance](./figures/williams2018unsupervised/figure-4j.png) <!-- .element  width="100%"-->

</div>


<div id='right'>

 - 'dimensionality': low dimensionality means firing reliably across trials 
 - variance: dynamic range of neural activity


</div>



<!--h-->




<font size=6>

#### Factors extracted by (nonnegative) TCA are interpretable

</font>


<font size=4>

Reminder: TCA is unsupervised, and the trial metadata are added post-hoc. (TCA performed here with 15 components, 7 not shown but are similar)

</font>

<div id='left'>

![TCA results on spatial navigation task](./figures/williams2018unsupervised/figure-6.png) <!-- .element  width="100%"-->

 <font size=1>
 
 $T=0$ Mouse at initial positoin. $0 \leq T \leq 5$ Mouse stay at initial position $5 \leq T \leq 7$ Mouse move to new location. $7 \leq T \leq 12$ Mouse at final position

 </font>

</div>

<div id='right'>

<font size=5>


 Component 1 and 2: neurons selective to initial position <!-- .element: class="fragment fade-in-then-semi-out" data-fragment-index="1" -->
 
 Component 5 and 6: neurons selective to the final position <!-- .element: class="fragment fade-in-then-semi-out" data-fragment-index="2" -->
 
 Component 7 and 8: neurons selective to reward (blue line: position rewarded changed) <!-- .element: class="fragment fade-in-then-semi-out" data-fragment-index="3" --> 
 
Thought: "These components are not difficult to pick up using other analysis technique." <!-- .element: class="fragment fade-in-then-semi-out" data-fragment-index="4" -->

Component 3: some neurons fire just before final-location-selective neurons fire  <!-- .element: class="fragment fade-in-then-semi-out" data-fragment-index="5" -->

Component 4: All neurons decrease activity within each day (arousal related?) <!-- .element: class="fragment fade-in-then-semi-out" data-fragment-index="6" -->
 

 
 
 </font>

</div>

<!--v-->

#### "I have to see the other 7 components"


![The rest of the 7 components](./figures/williams2018unsupervised/figure-s4a.png) <!-- .element  width="80%"-->



<!--v--> 



<font size=5>

#### "What if I just do PCA on the data instead?"

</font>


<font size=5>

For comparison purposes, Alex and others perform trials unfolding PCA, ie. you do PCA on $\mathbf{X} \in \mathbb{R}^{K \times NT}$

</font>


![Trial unfolding](./figures/williams2018unsupervised/figure-s1.png) <!-- .element  width="80%"--> <!-- .element: class="fragment current-visible" data-fragment-index="1" -->

<div id='left'> 

![PCA on the spatial navigation task](./figures/williams2018unsupervised/figure-s6.png) <!-- .element  width="80%"--> <!-- .element: class="fragment current-visible" data-fragment-index="2" -->

</div>

<div id='right'> 

<font size=5>



 - each row represent one component <!-- .element  width="50%"--> <!-- .element: class="fragment current-visible" data-fragment-index="2" -->
 - components sorted from most to least variance explained <!-- .element  width="50%"--> <!-- .element: class="fragment current-visible" data-fragment-index="2" -->


Thought: Since we are using nonnegative TCA, will be more fair to compare with nonnegative matrix factorisation. <!-- .element: class="fragment current-visible" data-fragment-index="2" -->

</font>

</div>


<!--h-->


### Audiovisual decision making task 



![Pip audiovisual task](./figures/pip-multispaceworld-task-outline.png)  <!-- .element width="40%"-->


<font size=5>

Data: neuropixel recording of MOs neurons, aligned to movement, trials involve either left/right choices.


</font>

<!--h-->

### The code is easy to use (but documentation can be better)

[Tensotools: fitting tensor decompositions in Python](https://github.com/ahwillia/tensortools)

<pre><code class="python">
import tensortools as tt

# Neuron * Time Points * Trials 
X = my_dataset['firing_rate'].values 

num_components = 8

# CP tensor decomposition solved with ALS
result = tt.cp_als(X, rank=num_components) 

# Prebuilt function to plot all factors
fig, _, _ = tt.plot_factors(result.factors)


</code></pre>

<!--h-->

### Audiovisuals task: TCA component 1

![TCA first component](./figures/tca-examples/subject_3_exp_21_movement_aligned_min_100ms_best_5_components_component_1_trial_response_w_kde.png) <!-- .element  width="80%"-->


<!--v-->


![TCA component 2](./figures/tca-examples/subject_3_exp_21_movement_aligned_min_100ms_best_5_components_component_2_trial_response_w_kde.png) <!-- .element  width="80%"-->


<!--v-->



![TCA component 3](./figures/tca-examples/subject_3_exp_21_movement_aligned_min_100ms_best_5_components_component_3_trial_response_w_kde.png) <!-- .element  width="80%"-->



<!--v-->


![TCA component 4](./figures/tca-examples/subject_3_exp_21_movement_aligned_min_100ms_best_5_components_component_4_trial_response_w_kde.png) <!-- .element  width="80%"-->



<!--v-->


![TCA component 5](./figures/tca-examples/subject_3_exp_21_movement_aligned_min_100ms_best_5_components_component_5_trial_response_w_kde.png) <!-- .element  width="80%"-->






<!--h-->


## Summary 


<font size=5>


 1. TCA exploit the fact neural data can be organised by trials to give more interpretable components that relate to (a) within trial neural activity and (b) changes in amplitude of these activity across trials <!-- .element: class="fragment fade-in-then-semi-out" data-fragment-index="1" -->
 
 2. Most task-related components that are retrieved probably can also be found using other methods, but since TCA is unsupservised, you may find components that were not obvious to you initially <!-- .element: class="fragment fade-in-then-semi-out" data-fragment-index="2" -->
 
 
 - Pros: interpretable factors, trial factors, IMO simpler than other extensions/alternatives of PCA (eg. demixed PCA, Gaussian Process Factor Analysis). <!-- .element: class="fragment fade-in-then-semi-out" data-fragment-index="3" -->
 
 - Cons: not an established technique, components may be different depending on the selected number of components (though it is possible to re-align them), and no closed form solution so you need to run iterations to get solution (ie. it may be slower) <!-- .element: class="fragment fade-in-then-semi-out" data-fragment-index="4" -->
 
 
 
 </font>

 <!--h-->
 

## Further reading

 - If you couldn't understand me, then the [author also did a talk about it](https://www.youtube.com/watch?v=hmmnRF66hOA&t=2s)
 - A good introduction to tensor decomposition: [Kolda and Bader 2009](https://epubs.siam.org/doi/abs/10.1137/07070111x)
 - Someone asked on Quora: [What is all the current fuss about data tensor decomposition? ](https://www.quora.com/What-is-all-the-current-fuss-about-data-tensor-decomposition-and-analysis-Data-analysis-and-historical-perspective)



 <!--h-->
 
 



<style>

#left {
	margin: 10px 0 15px 20px;
	text-align: left;
	float: left;
	z-index:-10;
	width:48%;
	font-size: 0.85em;
	line-height: 1.5; 
}

#right {
	margin: 10px 0 15px 0;
	float: right;
	text-align: left;
	z-index:-10;
	width:48%;
	font-size: 0.85em;
	line-height: 1.5; 
}

p { text-align: left; }

#myfigure{
	text-align: center;
}


.fragment.current-visible.visible:not(.current-fragment) {
    display: none;
    height:0px;
    line-height: 0px;
    font-size: 0px;
}

</style>



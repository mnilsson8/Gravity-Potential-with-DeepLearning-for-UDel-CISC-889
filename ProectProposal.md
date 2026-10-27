Proposal Link: 
https://docs.google.com/document/d/1j2TZJyZJMFm-9dnA9_faDacOpKsoXMpMjNPrXYIlgto/edit?usp=sharing


Paper Link: 
https://ar5iv.labs.arxiv.org/html/2011.04673
Pytorch: https://github.com/tingyuansen/deep-potential/blob/master/notebooks/plummer_sphere_example.ipynb 
https://github.com/gregreen/deep-potential/blob/master/notebooks/gauss_law.ipynb 

The final project asks students to apply Scientific Machine Learning methods to a substantive problem in science or engineering. Projects should connect a clearly defined scientific question with appropriate data, governing equations, physical constraints, or domain knowledge. Students are expected to justify their modeling choices, evaluate their results critically, and communicate the limitations of their approach. The size of the group and the duration of the presentation will be determined after registration for the course is finalized.
Research scope and expected outcomes
You are expected to complete a small but well-defined research project on either solving differential equations using deep learning or applying machine learning to scientific data. Keep the scope focused enough to implement, evaluate, and analyze within the semester.
The project should go beyond simply reproducing existing work. You should:
Identify a specific research question or potential improvement, and explain how it builds on existing work.
Implement appropriate methods and compare them with at least one relevant baseline using clearly defined evaluation metrics.
Conduct experiments that directly address your question, such as testing the effects of data availability, noise, model choices, or physical constraints.
Analyze the results, explain what they support, and discuss limitations and possible reasons for success or failure.
A focused comparison or a modest, carefully evaluated improvement is sufficient; a new state-of-the-art method is not required. For example, you might investigate whether a sampling strategy improves a neural differential-equation solver, or whether adding a physical constraint improves prediction from limited scientific data. A well-supported finding that an approach does not improve performance is also a valid outcome.
Example papers for project inspiration are available in Robotics and Time series (please access using UDEL account). Projects are not limited to these papers or topics; other projects within the scope described above are welcome.
The final results should be communicated through a total of five figures and tables combined (for example, three figures and two tables). These should support the research question, method comparisons, and experimental analysis, with clear labels, captions, and an explanation of the main findings. Include them in the final presentation slides and make them available in the code repository.


Project proposal — 10%
The proposal should clearly describe:
Team member names
The scientific or engineering problem and its significance
The research question or modeling objective
The proposed dataset, simulation, governing equations, or other sources of domain knowledge
The planned machine learning or Scientific Machine Learning approach
At least one baseline or comparison method
The proposed evaluation metrics and criteria for success
A feasible implementation timeline and expected final deliverables
The proposal will be evaluated on problem formulation, technical feasibility, connection to course concepts, appropriateness of the proposed evaluation, and clarity of presentation.

Our Proposal

Team member names: Athanasios Avgeris, Weston Broussea, Will Branam, Youssef El Gharably, Mathilda Nilsson

Problem and significance:
We want to understand with a few sample points the gravitational potential of the Milky Way, which can tell us about the distribution of dark matter within our own galaxy as well as reveal information about past mergers with other galaxies. The European Space Agency’s Gaia survey has recorded the positions of velocities of billions of stars within our galaxy, creating a map of our Milky Way. We want to be able to recover the gravitational potential profile of the Milky Way using position and velocity data. The paper “Deep Potential: Recovering the gravitational potential from a snapshot of phase space” (Green et al. 2023) describes a method to do so using normalizing flows to convert the data into a continuous distribution and a feed-forward neural network to solve for the gravitational potential, tested on a Plummer sphere model. We hope to improve on the original model by introducing further boundary conditions, as well as use the model on a selection of Gaia survey data. 

Research question:
How can we recover the gravitational potential from a snapshot of star positions and velocities? Can we improve upon the neural-network from Green et al. 2026? As a further question, could we recover a reasonable gravitational potential for the Milky Way from Gaia survey data?

Dataset/simulation/equations:
Equations: 
The collisionless Boltzmann equation: dfdt=ft+ i3(vifxi-xifvi)=0
𝚽 is the gravitational potential, and f is a function that describes the density of stars in the position vs velocity space. 

Proposed boundary conditions:
Gauge Invariance Pin: 
Where phi_0 is the neural network potential as a scalar function of a position in 3D space. R is the radius of the boundary condition sphere, which will be a number we choose that is large enough to contain nearly all the stars and still inside the region where the flow is accessible. n is a unit vector to tell us where the sphere is pointing. Phi_ref is the value we require Phi_0 to take at that point, which gives us the loss value for this. 
Gauss’s law flux: 


	Where M_enc is the total mass inside the sphere of radius R. G is newton’s constant, dA is the small patch of the sphere we are integrating on, the gradient of phi is the radial component of phi at that point (how fast the potential rises outwards) and E_n is the average/expectation value distributed on the sphere. I am thinking this will likely be a Monte Carlo mean over many random directions.


Exterior positive reward: i am thinking we can add this if the phi value decides to go negative outside the sphere, but also part of me thinks we should just add this regardless. 
 
The laplacian should be proportional to the matter’s density, the max keeps only the positive part and awards the more positive value, sinh seems like a good way to me for damping the outliers in case something explodes, and the 1[.] is a piecewise equation to ensure the points are outside the sphere


Total loss: 

Simulated Data: 
Plummer sphere model of gravitating body

Real Data: 
	Selection of Gaia Data Release 3 data from Gaia ESA archive:
	https://telbib.eso.org/detail.php?bibcode=2023A%26A...674A...1G

Planned approach:
Simulate the gravitational potential 
Attempt to improve: change boundary conditions
Original paper used bare minimum boundary conditions, we introduce gauge invariance, Gauss’s law, and and exterior positive reward to further constrain the model. 
Use normalizing flow to retrieve smooth function f from discrete distribution of stars in phase space.
Use feed-forward neural network to find gravitational potential.
If we have time: Test against ESA Gaia Archive
Retrieve position and velocity information for stars from various locations in Milky Way.
Compare our gravitational model to traditional models (https://arxiv.org/pdf/2601.08378) 


Comparison/baseline:
Green et al. 2023 Plummer sphere results vs our Plummer sphere results.
For our stretch goal: Bobylev et al 2026 models vs our gravitational potential from Gaia data.

Metrics/criteria for success:
The baseline metric for success is to recover a potential that makes physical sense using real data. 
We plan to start evaluating using MAE loss, potentially migrating to a hybrid method such as Huber Loss if initial results perform poorly. Our model will be tested against Plummer Sphere models and the results compared with other simulated models, aiming to improve performance by a significant margin. 

Timeline and deliverables:
Once the proposal is approved, we will then simulate the same Plummer sphere as in Green et al. 2023 and compare our performance to the original performance. This will happen by the end of November.
If we have time once we have tested our model on the simulated Plummer sphere, we will test our model on data from the Gaia survey of the Milky Way and compare our results to the results in (paper 2).
By December 1st, we will have our results and can start working on our presentation. We will present on December 8th.

Our deliverables:
Repository of code
https://github.com/westb1999/Gravity-Potential-with-DeepLearning-for-UDel-CISC-889
Loss plots 
Plot of potential of Plummer sphere real potential vs recovered potential
Velocity vs radius plot (referred to as a “rotation curve” in astronomy)
Bonus: Plot of potential of Milky Way from this model vs other traditional potential model (insert paper here)
Analysis of the difference in the traditional models to the current methods.


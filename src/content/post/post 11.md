## ANTIDOTE: Understanding and Defending against Poisoning of Anomaly Detectors
> Rubinstein, Benjamin IP, et al. "Antidote: understanding and defending against poisoning of anomaly detectors." Proceedings of the 9th ACM SIGCOMM conference on Internet measurement. ACM, 2009.[[PDF]] (https://people.eecs.berkeley.edu/~tygar/papers/SML/IMC.2009.pdf)
To uncover anomalies, many network anomography detection techniques mine the network-wide traffic matrix, which describes the traffic volume between all pairs of Points-of Presence(PoP) in a backbone network and contains the collected traffic volume time series for each origin-destination(OD) flow.

There is a network with N links and F OD flows and measure traffic on this network over T time intervals.
The relationship between link traffic and OD flow traffic is concisely captured in the routing matrix A. This matrix is an N ×F matrix such that Aij = 1 if OD flow j passes over link i, and is zero otherwise. If X is the T ×F traffic matrix(TM) containing the time-series of all OD flows, and if Y is the T × N link TM containing the time-series of all links, then Y = XA. We denote the t the row of Y as y(t) = Yt, which is the vector of N link traffic measurements at time t), and the original traffic along a source link, S by yS(t). 

Besides, the PCA defense method is inferring this normal traffic subspace using PCA, which finds the principal traffic components, makes it easier to identify volume anomalies in the remaining abnormal
subspace.

This paper's topic is to poisoning Principal Component Analysis anomaly detectors by poisoning the training data the detector uses (observed normal network activity), like adding additional traffic and noise to regular network traffic, to achieve a higher false negative rate

Threat Model
The adversary’s goal is to launch a Denial of Service (DoS) attack on some victim and to have the attack traffic successfully cross an ISP’s network without being detected. Before launching a DoS attack, the attacker poisons the detector for a period of time, by injecting additional traffic, chaff, along the OD flow that he eventually intends to attack.  For a poisoning strategy, the attacker needs to decide how much
chaff to add, and when to do so. These choices are guided by the amount of information available to the attacker. The weakest attacker is one that knows nothing about the traffic at the ingress PoP, and adds chaff randomly. An intermediate case is when the attacker is partially informed. Here the attacker knows the current volume of traffic on the ingress link(s) that he intends to inject chaff on, which is locally-informed attack. Attack can be the third type, globally-informed because the attacker's global view over the network enables him to know the traffic levels on all network links. Moreover, we assume this attacker has knowledge of future traffic link levels. 

Uninformed Chaff Selection
At each time t, the adversary decides whether or not to
inject chaff according to a Bernoulli random variable. If he
decides to inject chaff, the amount of chaff added is of size
θ, i.e., ct = θ. 
 Locally-Informed Chaff Selection
the attacker knows the volume of traffic in the
ingress link he controls, yS(t). Hence this scheme elects to
only add chaff when the existing traffic is already reasonably
large. In particular, we add chaff when the traffic volume on
the link exceeds a parameter α (we typically use the mean).
The amount of chaff added is ct = (max {0, yS(t) − α}})
θ

Globally-informed

Omnipotent adversary with knowledge of past, present, and future network traffic
Selects a link to poison and amount of chaff to add by solving an optimization problem
The optimization problem is as follow:
/image
/meaning of denote




ANTIDOTE: A ROBUST DEFENSE
This paper propose an approach searches for directions that maximize a robust scale estimate of the data projection to make PCA robust. Together with a new robust Laplace threshold, they form a new network-wide traffic anomaly detection method, Antidote. To mitigate the effect of poisoning attacks, this paper needs a learning algorithm that is stable in spite of data contamination. So the robust PCA can be that learning algorithm since robust is the formal term used to qualify this notion of stability.

The aim of a robust PCA is to construct a low dimensional subspace that captures most of the data’s dispersion and are stable under data contamination. The robust PCA algorithms we considered search for a
unit direction v whose projections maximize some univariate dispersion measure S (·); that is, v ∈ arg 公式4！！！max
a2=1 S (Ya) . The standard deviation is the dispersion measure used by PCA;

Unlike the eigenvector solutions that arise in PCA, there is generally no efficiently computable solution
for robust dispersion measures and so these must be approximated. So this paper proposed PCA-GRID, which is a successful method for approximating robust PCA subspaces.

To better understand the efficacy of a robust PCA algorithm, this paper demonstrate the effect our poisoning techniques have on the PCA algorithm and contrast them with the effect on the PCA-GRID algorithm

PCA-GRID
用图

Robust Laplace Threshold


instead of the normal distribution assumed by the Q-statistic, we use the quantiles of a Laplace distribution specified by a location parameter c and a scale parameter b. Critically, though, instead of using the mean and standard deviation, we robustly fit the distribution’s parameters. We
estimate c and b from the residuals ya(t)2 using robust consistent estimates of location (median) and scale (MAD) where P −1(q) is the qth quantile of the standard Laplace
distribution. The Laplace quantile function has the form
P −1 c,b (q) = c+b·k(q) for some k(q)


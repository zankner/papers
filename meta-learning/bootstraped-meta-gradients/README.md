This paper addresses two problems with the way that meta-learning is currently done:

* Myopia - Traditional approaches can only roll out the learner-network for K steps. This leads to the bias that learning dynamics in the first K steps are the same as though later in training.
* Ill-conditioning - The meta-weight gradients are calculated with the same loss that the student-learning is trained on. This means that if the loss landscape for the student-learner is ill-conditioned, the meta network will have the same problems.

Two changes are introduced to fix these problems:
* Target bootstrapping - The learner continues its update for L further steps, leading to learner weights K + L steps in the future. This means that a longer horizon of the learning dynamics are embedded in the learner weights.
* Matching function - Instead of taking the gradient with respect to the learner loss function, the similarity between the learner weights after K steps and the bootstraped learner weights is computed. This means that the learned policies can be more directly compared and that the meta optimization problem is no longer constrained to the same curvature as the learner task.

An interesting property of this formulation is that values which are not easily optimized under standard meta-gradients can be directly optimized. Since it is the policies which have their similarities computed, quantities such as epsilon in epsilon-greedy methods can be directly optimized by finding an epsilon which makes the policy after K steps similar to the policy learned L steps in the future.
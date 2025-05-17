Here I will be extending a few derivations found in the paper: "Understanding Diffusion Models: A Unified Perspective", by Calvin Luo.

I was initially confused as to how one could reach equation 45 from equation 43. I wanted to provide the my full derivation in case someone finds it helpful.

Equation 43: $$\ =\mathbb{E}_{q(x_{1:T}|x_0)} [\log p_\theta(x_0|x_1)] \ + \mathbb{E}_{q(x_{1:T}|x_0)} [\log \dfrac{p(x_T)}{q(x_T|x_{t-1})}]\ +\sum_{t=1}^{T-1}\mathbb{E}_{q(x_{1:T}|x_0)}\dfrac{p_\theta(x_T|x_{t+1})}{q(x_T|x_{t-1})}$$

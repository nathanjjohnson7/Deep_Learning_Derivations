Here I will be extending a few derivations found in the paper: "Understanding Diffusion Models: A Unified Perspective", by Calvin Luo.

I was initially slightly confused as to how one could reach equation 45 from equation 43. I wanted to provide my full derivation in case someone finds it helpful.

Equation 43 (from paper):

$$\ =E_{q(x_{1:T}|x_0)} \left[\log p_\theta(x_0|x_1)\right] \ + E_{q(x_{1:T}|x_0)} \left[\log \dfrac{p(x_T)}{q(x_T|x_{T-1})}\right]\ +\sum_{t=1}^{T-1}E_{q(x_{1:T}|x_0)}\left[\log \dfrac{p_\theta(x_t|x_{t+1})}{q(x_t|x_{t-1})}\right]$$

We marginalize out irrelevant variables.
For example, if we consider just the first term:

$$\ =E_{q(x_{1:T}|x_0)} \left[\log p_\theta(x_0|x_1)\right]$$
$$\ =\int q(x_{1:T}|x_0) \left[\log p_\theta(x_0|x_1)\right] dx_{1:T}$$
$$\ =\int \left[\log p_\theta(x_0|x_1)\right] \left[\int q(x_{1:T}|x_0) dx_{2:T} \right] dx_1$$
$$\ =\int \left[\log p_\theta(x_0|x_1)\right] q(x_1|x_0) dx_1$$
$$\ =E_{q(x_1|x_0)} \left[\log p_\theta(x_0|x_1)\right] $$

We apply the above approach to all three terms.

Equation 44 (from paper):

$$\ =E_{q(x_1|x_0)} \left[\log p_\theta(x_0|x_1)\right] \ + E_{q(x_{T-1},x_T|x_0)} \left[\log \dfrac{p(x_T)}{q(x_T|x_{T-1})}\right]\ +\sum_{t=1}^{T-1}E_{q(x_{t-1},x_t,x_{t+1}|x_0)}\left[\log \dfrac{p_\theta(x_t|x_{t+1})}{q(x_t|x_{t-1})}\right]$$

Let's now simplify the second term of equation 44:

$$\ =E_{q(x_{T-1},x_T|x_0)} \left[\log \dfrac{p(x_T)}{q(x_T|x_{T-1})}\right]$$
$$\ =\int q(x_{T-1},x_T|x_0) \left[\log \dfrac{p(x_T)}{q(x_T|x_{T-1})}\right] dx_{T-1}dx_T$$
$$q(x_{T-1},x_T|x_0) = q(x_T|x_{T-1},x_0)q(x_{T-1}|x_0)$$

Markov Property: every state is only dependant on the previous state

$$q(x_{T-1},x_T|x_0) = q(x_T|x_{T-1})q(x_{T-1}|x_0)$$
$$\ =\int q(x_T|x_{T-1})q(x_{T-1}|x_0) \left[\log \dfrac{p(x_T)}{q(x_T|x_{T-1})}\right] dx_{T-1}dx_T$$
$$\ =\int q(x_{T-1}|x_0) \left[ \int q(x_T|x_{T-1}) \left[\log \dfrac{p(x_T)}{q(x_T|x_{T-1})}\right] dx_T \right] dx_{T-1}$$
$$\ =\int q(x_{T-1}|x_0) (-D_{KL}(q(x_T|x_{T-1}) || p(x_T))) dx_{T-1}$$
$$\ = - E_{q(x_{T-1}|x_0)} [D_{KL}(q(x_T|x_{T-1}) || p(x_T))]$$

Similarly, we simplify the third term of equation 44: 

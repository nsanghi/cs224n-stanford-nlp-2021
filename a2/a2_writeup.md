# Written part of the Assignment 1

## 1(a)

The relation 
$$ - \sum_{w \in Vocab} y_wlog(\hat{y}_w) = - log(\hat{y}_o)$$
is true as $y_w$ is a one-hot vector with only one element set to 1 for $w=o$.

## 1(b)

$$ \frac{\partial J_{naive_softmax}(v_c, o, U)}{\partial v_c} = U(\hat{y}-y)$$

and this has shape of $(d,1) where $d$ is the depth of each vector$

## 1(c)

when $w \neq o$,
$$ \frac{\partial J_{naive_softmax}(v_c, o, U)}{\partial u_w} = \hat{y}_w v_c$$

when $w = o$,

$$ \frac{\partial J_{naive_softmax}(v_c, o, U)}{\partial u_w} = (\hat{y}_w-1) v_c$$

## 1(d)

$$ \frac{\partial J_{naive_softmax}(v_c, o, U)}{\partial U} = v_c (\hat{y}-y)^T$$
which has a shape of $(d,|Vocab|)$

## 1(e)

$$f(x) = max(0,x)$$
$$\frac{\partial f(x)}{\partial x} = 1 \text{ if } x > 0$$

## 1(f)

$$ \sigma(x) = \frac{1}{1+e^{-x}}$$
$$\frac{\partial \sigma(x)}{\partial x} = \sigma(x) (1-\sigma(x))$$

## 1(g)(i)

$$ J_{neg\_sample}(v_c, o, U) = -log(\sigma(u_o^T v_c)) - \sum_{s=1}^{s=K}log(\sigma(-u_{w_s}^T v_c))$$


$$ \frac{\partial J_{neg\_sample}(v_c, o, U)}{\partial v_c} = -[1-\sigma(u_o^T v_c)]u_o + \sum_{s=1}^{s=K} [1-\sigma(-u_{w_s}^T v_c)]u_{w_s}$$

$$ \frac{\partial J_{neg\_sample}(v_c, o, U)}{\partial u_o} = -[1-\sigma(u_o^T v_c)]v_c $$

$$ \frac{\partial J_{neg\_sample}(v_c, o, U)}{\partial u_{w_s}} = [1-\sigma(-u_{w_s}^T v_c)]v_c $$

## 1(g)(ii)
We can precompute the $\sigma(u_o^T v_c)$ and $\sigma(-u_{w_s}^T v_c)$ for all $w_s \in Vocab$

in matrix form that would mean pre-computing:
$$\mathbf{1}_{K+1} - \sigma(U^Tv_c)$$

## 1(g)(iii)

Naive-softmax requires calcualtion of $\hat{y}$ which is expensive.

## 1(h)

$$ \frac{\partial J_{neg\_sample}(v_c, o, U)}{\partial u_{w_s}} =  - \sum_{s=1 \atop w_s = w_s'}^{K} [\sigma(-u_{w_s'}^T v_c)-1]v_c $$

## 1(i)

$$J_{skip-gram}(v_c, w_{t-m},...,w_{t+m},U) = \sum_{-m \leq j\leq m \atop j\neq 0} J(v_c,w_{t+j},U)$$

$$\frac{\partial J_{skip-gram}(v_c, w_{t-m},...,w_{t+m},U)}{\partial U} = \sum_{-m \leq j\leq m \atop j\neq 0} \frac{J(v_c,w_{t+j},U)}{\partial U}$$

$$\frac{\partial J_{skip-gram}(v_c, w_{t-m},...,w_{t+m},U)}{\partial v_c} = \sum_{-m \leq j\leq m \atop j\neq 0} \frac{J(v_c,w_{t+j},U)}{\partial v_c}$$

$$\frac{\partial J_{skip-gram}(v_c, w_{t-m},...,w_{t+m},U)}{\partial v_w} = \sum_{-m \leq j\leq m \atop j\neq 0} \frac{J(v_c,w_{t+j},U)}{\partial v_w}$$

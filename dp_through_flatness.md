### 2024/Nov/19
## Differential Privacy through Flatness. 

I came across this paper called [*Privacy-preserving Fine-tuning of Large Language Models through Flatness*](https://openreview.net/forum?id=LtdcfCw92l&referrer=%5Bthe%20profile%20of%20Tianlong%20Chen%5D(%2Fprofile%3Fid%3D~Tianlong_Chen1)). This paper is accepted to SeT LLM @ ICLR 2024; seems to be a franchise of a larger brand, much like Volkswagen is to the Volkswagen Group (which also includes Porsche and Audi). While Volkswagen doesn’t represent the highest standard of the brand, it’s still part of the lineup, so I decided to give it a try.

The authors write that ```our paper reveals that the flatness of DP-trained models' loss landscape plays an essential role in the trade-off between their privacy and generalization.``` 

In Figure 1 of their paper, they show that when you perturb the model parameters $w$ with some random noise $d$ sampled from a standard Gaussian distribution times some magnitude $\eta$. Then the loss computed on 

$$w+\eta d$$

is less stable as we increase $\eta$, if $w$ is a DP model, compared with a non-DP model. This makes sense to me--DP models are less flat--at least from the provided Figure 1. So maybe we can do something about the sharpness to make DP models perform better.

The authors then ```conduct pioneering efforts to investigate that the critical role of weight flatness in DP-trained LLMs.``` I do not know the definition of pioneering efforts, but this idea to seems interesting to me. So I continued reading.

#### How does this pizza taste?
In the rest of this paper, the authors then propose ```a holistic framework to enforce appropriate weight flatness, which substantially improves model generalization with competitive privacy preservation```. Their algorithm can be summarized as follows. In each iteration with model weight $w$,

1. find $v$ such that the loss is *maximized* at $w+v$;
2. compute the model's gradient at $w+v$, and then perform the gradient descent from $w$.

How to make this algorithm differentially private? The authors wrote ```We tailor AWP to DP training with two critical changes...the required noises in DP training are only added to the final gradient...instead of the process of computing $v$```. I gave up reading after seeing this. The authors say that only the gradients in the second step are perturbed with DP noises, and the first step is not differentially private. This is not differentially private, since the information of training data is encoded in $v. It could be that the gradients computed from $w+v$ are all based on some particular record, and adding noises in the second step does not help hide this information at all. 

This concludes my first review. Maybe the authors have made some pioneering efforts. Sadly I do not understand those efforts. This is similar to seeing cold chocolates on top of hot pizzas with melting cheese. It is a quite bold combination but I could not appreciate the idea; perhaps, if the chef really care about pizza, at least, please, make the chocolates hot. 

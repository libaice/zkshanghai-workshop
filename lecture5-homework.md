# 第5课 课后作业



1. **The Setup phase of the KZG polynomial commitment scheme involves computing commitments to powers of a secret evaluation point τ . This is called the “trusted setup" and is often generated in a multi-party computation known as the “Powers of Tau" ceremony. One day, you find the value of τ on a slip of paper. How can you use it to make a fake KZG opening proof?**

   **如果有一天，在纸条上发现了 τ的值，如何使用这个值来做一个假的 KZG 证明？**



> 如果有个τ的值，那么你可以使用它来制作一个假的KZG开放证明。
>
> KZG承诺多项式p(X)的承诺是C = Commit(p(X)) = [p(τ)]1。
>
> 
>
> 对于声明“C = Commit(p(X)), p(x) = y”的开放证明是一个群元素π∈G1。
>
> 因此，如果知道τ的值，你可以伪造一个多项式p'(X)，使得[p'(τ)]1=C，然后构造一个开放证明π'=[q'(τ)]1，其中q'(X)=p'(X)-y/(X-x)，这样就可以欺骗验证者了。





2. **Construct a vector commitment scheme from the KZG polynomial commitment scheme.** 
   **(Hint: For a vector m = (m1, . . . , mq), is there an “interpolation polynomial" I(X) such that I(i) = m[i]?)** 

   【Fun fact: The Verkle tree is a Merkle tree that uses a vector commitment instead of a hash function. Using the KZG vector commitment scheme, can you see why a Verkle tree is more efficient?】

​	**从 KZG 多项式承诺方案构造一个向量承诺方案。**



> 可以将向量m = (m1,...,mq)视为在点1，...，m处的多项式的评估。
>
> 我们可以构造一个拉格朗日插值多项式I(X)，使得I(i)=m[i]。
>
> 这里，拉格朗日基函数L_i(X)是一个多项式，当X=i时为1，否则为0。使用KZG承诺方案对I(X)进行承诺，并在向量位置x∈[m]处查询该承诺以获得向量承诺。


**使用 KZG 向量承诺方案，您能看出为什么 Verkle 树更高效吗**

> Verkle Tree相对于Merkle Tree更高效，因为它使用向量承诺而不是哈希函数。
>
> 在深度为n的k叉树中，Merkle Tree构造将给出大小为klogn的认证路径（每个级别有k个子节点）。相比之下，Verkle Tree的认证路径仅由log n个KZG开放证明组成：在每个父节点处，我们承诺一个子节点向量，并提供一个常数大小的开放证明。通过巧妙地将父子关系捕捉到单个多项式中，我们可以进一步将证明大小减小到单个KZG证明。
>
> 详细内容请参见“[Verkle Trees (Vitalik Buterin, 2018)](https://vitalik.ca/general/2021/06/18/verkle.html)”。





3.  **The KZG polynomial commitment scheme makes an opening proof π for the relation p(x) = y. Can you extend the scheme to produce a multiproof π, that convinces us of p(xi) = yi for a list of points and evaluations (xi , yi)? (Hint: assume that you have an interpolation polynomial I(X) such that I(xi) = yi .**



​	**拓展这个KZG多项式承诺，从而产生一个多重证明，来使得p(xi) = yi 有一系列的点和评估(xi,yi)**



> 可以将KZG承诺方案扩展到多个点和评估{ (xi,yi) }，从而产生一个多重证明π，使得p(xi) = yi。假设我们有一个插值多项式I(X)，使得I(xi) = yi。KZG开放证明为π = [q(τ)]1，其中商多项式q(X)定义为q(X) = p(X) - y / (X - xi)，这是一个良构造的多项式，当且仅当x是p(X)-y的根时（也就是说，当p(x)-y=0时）。要将此证明扩展到多个点和评估{ (xi,yi) }，我们设置q_multiproof(X) = p(X) - I(X) / Q(X - xi)，其中Q是所有点的乘积。


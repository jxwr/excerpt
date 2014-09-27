### proofgeneral(emacs) keybind

- c-x c-n 证明一行
- c-x c-u 取消一行
- c-x c-ret 证明到指定行

### coq

* Coq中描述项、类型、证明、程序的语言称为Gallina，命令语言称为Vernacular。Coq采用了具有很强表达能力的类型lambda演算的变体归纳构造演算。
* 论文集：《From Frege to Godel》
* 程序与类型之间的关系和证明与命题之间的关系相同，因此可以用类型验证算法来验证一个证明。
* 假设和局部变量相同，公理和全局变量相同。
* 假设用Hypotheses或Variables声明，公理用Axiom或Parameter声明。
* 定理用Theorem声明，引理Lemma和Theorem类似，但是一般用于辅助结果。
* tactics为证明策略。
* 默认情况下，Definition和Let声明都是透明的，而Theorem和Lemma都是不透明的，透明值其值是否后续可见。
* 原子命题可以分解为客体和谓词两部分
* 刻划一个客体性质的词称之为一元谓词,刻划n个客体之间关系的词称之为n元谓词
* the keywords Example and Theorem (and a few others, including Lemma, Fact, and Remark) mean exactly the same thing to Coq.
* rewrite后面的箭头表示从哪向哪rewrite

* Curry-Howard同构，lambda演算与proof演算可互相表示
* 最小命题逻辑：仅有命题变量和蕴含关系，如(P->Q)->(Q->R)->P->R
* 命题变量作为类型，若可以可以构造出一个函数定义，其返回值的类型为需要求得的Goal命题变量，则证明了该命题
* Modus Ponens (implication elimimination)
* 很多时候，逻辑书本上给出一个定义，为某个阶段的结果起一个名字，但却没有给出这个定义之所以抽取出来作为定义的重要意义
* 依赖类型：函数作用于适当的表达式的结果
* 依赖积： forall v:A, B  这是个类型， 其中v相当于一个类型变量，该类型在使用时需要首先指定第一个参数





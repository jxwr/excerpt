
- A dependently-typed programming language relies on several components, a type checker for the core type theory, a uniﬁcation algorithm, an evaluator.
- (Idris ) a tactic-based method for translating programs in a high-level dependently-typed programming language to a small core type theory, TT, based on UTT.
- IDRIS (desugaring) −−−−−−−→ IDRIS (elaboration) −−−−−−−→ TT (compilation) −−−−−−−→ Executable
- Idris's core TT, which is a λ-calculus with dependent types, augmented with algebraic data types and pattern matching.
- Idris compiled via the Epic supercombinator library.
- 基本类型: Int, Integer, Float, Char, String, Ptr, Bool
- Idris所有toplevel函数必须写类型签名，因为依赖类型的类型推断不总是确定性的
- 隐式参数用于给类型变量指定类型或占位（将会类型推断）
  ```
  index : {a:Type} -> {n:Nat} -> Fin n -> Vect n a -> a
  ```
- TT, http://eb.host.cs.st-andrews.ac.uk/writings/ivor.pdf
- 将Idris代码转换成TT
  1. 要将隐式参数变为显式的，并将模式匹配函数前面加上占位参数
  2. 求解这些隐式参数，使用uniﬁcation algorithm算法
- Idris到TT的转化过程，其实是一系列tactics不断求解证明的过程

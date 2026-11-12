# Pattern Recognition slides — derivations to expand (WS 2026/27)

Instructions for an editing agent. Seven places where a slide states a result without the intermediate steps. For each: **where** (chapter file + frame title), **what is missing**, and **ready-to-paste LaTeX** (beamer frames using the course macros `\vec`, `\mat`, `\argmax`, `\real` from `commands.tex`).

## General rules
- **Insert new frames directly after the named frame.** Do not delete or rewrite the existing slide (exception: item 3, where three image slides are replaced).
- Keep the course notation: $y$ true label, $\hat y$ prediction, hats on estimates, $p(\cdot)$ for both pmf and pdf, parameters after `;`.
- Use `\pause` between derivation steps, as the surrounding slides do. Keep each frame within the slide; if it gets long, use `{\small ...}` or split into two frames titled `... \cont`.
- Compile the chapter after each insertion (pdfLaTeX) and check that no text runs into the footer.
- Priority: 1, 2, 4, 5 first (short, often examined); then 6, 7; item 3 is the largest.

---

## 1. Chapter 20 — Bias–variance decomposition (regression)

**File:** `20_model_assessment.tex` — insert after frame *Bias and Variance for Regression* (the one stating $E_{\mathcal D}\{(g-F)^2\} = \text{bias}^2 + \text{variance}$).

**Missing:** the add-and-subtract step and why the cross term vanishes.

```latex
\begin{frame}
  \frametitle{Bias and Variance for Regression \cont}

  \structure{Derivation} (fixed $\vec x$; abbreviate $g = g(\vec x;\mathcal D)$, $\bar g = E_{\mathcal D}\{g\}$, $F = F(\vec x)$):
  {\small
  \begin{eqnarray*}
    E_{\mathcal D}\left\{ (g - F)^2 \right\}
      &=& E_{\mathcal D}\left\{ \big( (g - \bar g) + (\bar g - F) \big)^2 \right\} \\[.2cm] \pause
      &=& E_{\mathcal D}\left\{ (g - \bar g)^2 \right\}
          + 2\,(\bar g - F)\, E_{\mathcal D}\left\{ g - \bar g \right\}
          + (\bar g - F)^2 \\[.2cm] \pause
      &=& \underbrace{E_{\mathcal D}\left\{ (g - \bar g)^2 \right\}}_{\text{variance}}
          + \underbrace{(\bar g - F)^2}_{\text{bias}^2}
  \end{eqnarray*}
  }
  \pause
  The cross term vanishes because $\bar g - F$ does not depend on $\mathcal D$ and
  $E_{\mathcal D}\{ g - \bar g \} = \bar g - \bar g = 0$.
\end{frame}
```

---

## 2. Chapter 17 — GMM M-step (where the update formulas come from)

**File:** `17_em.tex` — insert after frame *GMM -- Maximization* (which lists $\hat{\vec\mu}_k$, $\hat{\mat\Sigma}_k$, $\hat p_k$ without derivation).

**Missing:** derivative of the log-likelihood w.r.t. $\vec\mu_k$ (how the responsibilities $p_{ik}$ appear), the $\mat\Sigma_k$ result, and the constrained maximization for $p_k$.

Notation (as in ch. 17): $L(\vec\theta) = \sum_{i=1}^m \log \sum_{k=1}^K p_k\, \mathcal N(\vec x_i;\vec\mu_k,\mat\Sigma_k)$, responsibilities $p_{ik} = p(z_i=k|\vec x_i;\vec\theta)$, Lagrangian written $\Lambda$ (not $L$).

```latex
\begin{frame}
  \frametitle{GMM -- Maximization \cont}

  \structure{Derivative w.\,r.\,t.\ the mean $\vec\mu_k$} \\[.1cm]
  {\small
  Using $\frac{\partial}{\partial \vec\mu_k}\mathcal N(\vec x_i;\vec\mu_k,\mat\Sigma_k)
        = \mathcal N(\vec x_i;\vec\mu_k,\mat\Sigma_k)\,\mat\Sigma_k^{-1}(\vec x_i-\vec\mu_k)$:
  \begin{eqnarray*}
    \frac{\partial L}{\partial \vec\mu_k}
      &=& \sum_{i=1}^m
          \underbrace{\frac{p_k\,\mathcal N(\vec x_i;\vec\mu_k,\mat\Sigma_k)}
                           {\sum_{l} p_l\,\mathcal N(\vec x_i;\vec\mu_l,\mat\Sigma_l)}}_{=\,p_{ik}}
          \mat\Sigma_k^{-1}(\vec x_i-\vec\mu_k)
      ~\stackrel{!}{=}~ \vec 0 \\[.2cm] \pause
    &\Rightarrow& \hat{\vec\mu}_k = \frac{\sum_i p_{ik}\,\vec x_i}{\sum_i p_{ik}}
  \end{eqnarray*}
  }
  \pause
  \structure{Covariance $\mat\Sigma_k$:} the same steps as for the single Gaussian (ML example), \\
  with every sample weighted by $p_{ik}$:
  {\small
  \begin{displaymath}
    \hat{\mat\Sigma}_k = \frac{\sum_i p_{ik}\,(\vec x_i-\hat{\vec\mu}_k)(\vec x_i-\hat{\vec\mu}_k)^T}{\sum_i p_{ik}}
  \end{displaymath}
  }
  The responsibilities act as \structure{soft class assignments}: with hard assignments ($p_{ik}\in\{0,1\}$) these are the ordinary class means and covariances.
\end{frame}


\begin{frame}
  \frametitle{GMM -- Maximization \cont}

  \structure{Mixture weights $p_k$} must satisfy $\sum_k p_k = 1$ $\Rightarrow$ Lagrangian with multiplier $\nu$:
  {\small
  \begin{eqnarray*}
    \Lambda(p_1,\dots,p_K,\nu) &=& L(\vec\theta) + \nu\Big(\sum_{k=1}^K p_k - 1\Big) \\[.2cm] \pause
    \frac{\partial \Lambda}{\partial p_k}
      &=& \sum_{i=1}^m \frac{\mathcal N(\vec x_i;\vec\mu_k,\mat\Sigma_k)}{\sum_l p_l\,\mathcal N(\vec x_i;\vec\mu_l,\mat\Sigma_l)} + \nu
      ~=~ \frac{1}{p_k}\sum_{i=1}^m p_{ik} + \nu ~\stackrel{!}{=}~ 0 \\[.2cm] \pause
    &\Rightarrow& p_k = -\frac{1}{\nu}\sum_i p_{ik}
  \end{eqnarray*}
  }
  \pause
  Summing over $k$ and using $\sum_k p_{ik}=1$: $\;1 = -\frac{1}{\nu}\sum_i\sum_k p_{ik} = -\frac{m}{\nu}$, i.\,e.\ $\nu=-m$:
  {\small
  \begin{displaymath}
    \hat p_k = \frac{1}{m}\sum_{i=1}^m p_{ik}
  \end{displaymath}
  }
  (The same argument is used in the prior-estimation example later in this chapter.)
\end{frame}
```

---

## 3. Chapter 10 — Replace the three gradient images with LaTeX

**File:** `10_mlp.tex` — the three frames titled *Linear Network in Matrix notation* that only contain `\includegraphics{png/gradient_derviation1.png}` / `...2.png` / `...3.png` (plus a caption mapping $\hat{\vec f}$, $L(\vec\theta)$). **Replace these three frames** with the two frames below. Keep the preceding frame *Linear Network in Matrix Notation* (definition of $\hat{\vec y}=\mat W_3\mat W_2\mat W_1\vec x$ and $\mathcal L(\vec\theta)$) unchanged.

**Content of the images (for reference):** forward pass $\vec x \to \vec f_1 \to \vec f_2 \to \vec f_3$ through $\mat W_1,\mat W_2,\mat W_3$; backward pass with $\partial\mathcal L/\partial\vec f_3 = \mat W_3\mat W_2\mat W_1\vec x-\vec y$, $\partial\vec f_3/\partial\vec f_2 = \mat W_3^T$, $\partial\vec f_2/\partial\vec f_1=\mat W_2^T$, and results
$\partial\mathcal L/\partial\mat W_3 = (\mat W_3\mat W_2\mat W_1\vec x-\vec y)(\mat W_2\mat W_1\vec x)^T$,
$\partial\mathcal L/\partial\mat W_2 = \mat W_3^T(\mat W_3\mat W_2\mat W_1\vec x-\vec y)(\mat W_1\vec x)^T$,
$\partial\mathcal L/\partial\mat W_1 = \mat W_2^T\mat W_3^T(\mat W_3\mat W_2\mat W_1\vec x-\vec y)\,\vec x^T$.

```latex
\begin{frame}
  \frametitle{Linear Network in Matrix Notation \cont}

  \structure{Forward pass} (store the layer outputs):
  {\small
  \begin{displaymath}
    \vec f_1 = \mat W_1\vec x, \qquad
    \vec f_2 = \mat W_2\vec f_1, \qquad
    \vec f_3 = \mat W_3\vec f_2 = \hat{\vec y}, \qquad
    \mathcal L(\vec\theta) = \tfrac12\|\vec f_3 - \vec y\|_2^2
  \end{displaymath}
  }
  \pause
  \structure{Two rules} for a linear layer $\vec f_\text{out} = \mat W\vec f_\text{in}$ (chain rule):
  {\small
  \begin{displaymath}
    \frac{\partial \mathcal L}{\partial \mat W} = \frac{\partial \mathcal L}{\partial \vec f_\text{out}}\;\vec f_\text{in}^{\,T},
    \qquad
    \frac{\partial \mathcal L}{\partial \vec f_\text{in}} = \mat W^T\,\frac{\partial \mathcal L}{\partial \vec f_\text{out}}
  \end{displaymath}
  }
  \pause
  \structure{Backward pass}, starting from the error $\vec e = \partial\mathcal L/\partial\vec f_3 = \hat{\vec y}-\vec y$:
  {\small
  \begin{displaymath}
    \frac{\partial \mathcal L}{\partial \vec f_3} = \vec e, \qquad
    \frac{\partial \mathcal L}{\partial \vec f_2} = \mat W_3^T\vec e, \qquad
    \frac{\partial \mathcal L}{\partial \vec f_1} = \mat W_2^T\mat W_3^T\vec e
  \end{displaymath}
  }
\end{frame}


\begin{frame}
  \frametitle{Linear Network in Matrix Notation \cont}

  \structure{Gradients w.\,r.\,t.\ the weights} (first rule, with the stored forward outputs):
  {\small
  \begin{eqnarray*}
    \frac{\partial \mathcal L}{\partial \mat W_3} &=& \vec e\;\vec f_2^{\,T}
      = (\mat W_3\mat W_2\mat W_1\vec x - \vec y)\,(\mat W_2\mat W_1\vec x)^T \\[.2cm] \pause
    \frac{\partial \mathcal L}{\partial \mat W_2} &=& (\mat W_3^T\vec e)\;\vec f_1^{\,T}
      = \mat W_3^T(\mat W_3\mat W_2\mat W_1\vec x - \vec y)\,(\mat W_1\vec x)^T \\[.2cm] \pause
    \frac{\partial \mathcal L}{\partial \mat W_1} &=& (\mat W_2^T\mat W_3^T\vec e)\;\vec x^T
      = \mat W_2^T\mat W_3^T(\mat W_3\mat W_2\mat W_1\vec x - \vec y)\,\vec x^T
  \end{eqnarray*}
  }
  \pause
  \structure{Note:} the backward vectors are $\partial\mathcal L/\partial\vec f_l = -\vec\delta^{(l)}$, i.\,e.\ the sensitivities of the backpropagation algorithm with opposite sign, for a linear activation $f(\text{net})=\text{net}$; each weight gradient is ``backward signal $\times$ forward input$^T$''.
\end{frame}
```

After the replacement the three PNG files `png/gradient_derviation{1,2,3}.png` are no longer used (leave them in the project or delete them).

---

## 4. Chapter 14 — Soft-margin dual and the box constraint

**File:** `14_svm_2.tex` — insert after frame *Lagrange Dual* (which derives the **hard-margin** dual $L_D(\vec\lambda)$) and before *The Lagrange Dual Problem*.

**Missing:** that the soft-margin Lagrangian gives the same dual objective, plus the box constraint $0\le\lambda_i\le\mu$ and its interpretation.

Notation (as in ch. 14): slack weight $\mu$ (also $C$), multipliers $\lambda_i$ (margin constraints) and $\eta_i$ (for $\xi_i\ge 0$); stationarity conditions $\vec\alpha=\sum_i\lambda_iy_i\vec x_i$, $\sum_i\lambda_iy_i=0$, $\mu-\eta_i-\lambda_i=0$.

```latex
\begin{frame}
  \frametitle{Lagrange Dual: Soft Margin}

  Insert the three stationarity conditions into the soft-margin Lagrangian:
  {\small
  \begin{eqnarray*}
    L &=& \frac12\vec\alpha^T\vec\alpha - \sum_i\lambda_i\big(y_i(\vec\alpha^T\vec x_i+\alpha_0)-1\big)
          + \sum_i \underbrace{(\mu - \eta_i - \lambda_i)}_{=\,0}\,\xi_i \\[.2cm] \pause
      &=& -\frac12\sum_i\sum_j \lambda_i\lambda_j y_iy_j\,\vec x_i^T\vec x_j + \sum_i\lambda_i
      ~=~ L_\text{D}(\vec\lambda)
  \end{eqnarray*}
  }
  \pause
  The slack variables drop out: the dual objective is the \structure{same as for the hard margin}. \\[.2cm] \pause
  Only the constraints change: $\eta_i = \mu - \lambda_i \geq 0$ and $\lambda_i\ge 0$ give the \structure{box constraint}
  {\small
  \begin{displaymath}
    0 \le \lambda_i \le \mu, \qquad \sum_i \lambda_i y_i = 0
  \end{displaymath}
  }
  $\mu$ bounds the influence a single sample can have on $\vec\alpha=\sum_i\lambda_iy_i\vec x_i$.
\end{frame}


\begin{frame}
  \frametitle{Lagrange Dual: Soft Margin \cont}

  \structure{Complementary slackness} $\lambda_i\big(y_if(\vec x_i)-1+\xi_i\big)=0$ and $\eta_i\xi_i = (\mu-\lambda_i)\,\xi_i = 0$:
  \begin{itemize}
    \item $\lambda_i = 0$: $\;y_if(\vec x_i)\ge 1$ -- correctly classified, outside the margin (no influence). \pause
    \item $0<\lambda_i<\mu$: $\;\xi_i=0$ and $y_if(\vec x_i)=1$ -- support vector \structure{on} the margin hyperplanes. \pause
    \item $\lambda_i=\mu$: $\;\xi_i\ge 0$ -- support vector \structure{inside} the margin ($0<\xi_i\le 1$) \\ or misclassified ($\xi_i>1$). \pause
  \end{itemize}
  \structure{Offset:} for any sample with $0<\lambda_i<\mu$: $\;\alpha_0 = y_i - \vec\alpha^T\vec x_i$ (in practice: average over all such samples).
\end{frame}
```

Also fix the existing implications slide (*Lagrange Dual Problem (cont.)*, "All $\vec x_i$ with $\lambda_i>0$ lie on the margin hyperplanes"): add "(hard margin; for the soft margin see above)".

---

## 5. Chapter 07 — Fisher's criterion → generalized eigenvalue problem

**File:** `07_discriminant_analysis_2.tex` — insert after the frame *Fisher Transform (cont.)* that ends with "This is known as the Generalized Rayleigh Quotient", before the frame that starts "Maximizing the Generalized Rayleigh Quotient is equivalent to solving … $\mat S_\mathsf B\vec r^* = \lambda\mat S_\mathsf W\vec r^*$".

**Missing:** why maximizing $J(\vec r)$ gives the generalized eigenproblem, and which eigenvalue to take.

```latex
\begin{frame}
  \frametitle{Fisher Transform \cont}

  \structure{Maximizing the Rayleigh quotient}
  \begin{itemize}
    \item $J(\vec r) = \dfrac{\vec r^T\mat S_\mathsf B\vec r}{\vec r^T\mat S_\mathsf W\vec r}$ does not change if $\vec r$ is scaled. \\
          We may therefore fix the denominator and solve the constrained problem
          {\small
          \begin{displaymath}
            \max_{\vec r}\; \vec r^T\mat S_\mathsf B\vec r \quad\text{subject to}\quad \vec r^T\mat S_\mathsf W\vec r = 1
          \end{displaymath}
          }
          \pause
    \item Lagrangian with multiplier $\lambda$:
          {\small
          \begin{eqnarray*}
            \Lambda(\vec r,\lambda) &=& \vec r^T\mat S_\mathsf B\vec r - \lambda\,(\vec r^T\mat S_\mathsf W\vec r - 1) \\[.1cm] \pause
            \frac{\partial\Lambda}{\partial\vec r} &=& 2\mat S_\mathsf B\vec r - 2\lambda\,\mat S_\mathsf W\vec r ~\stackrel{!}{=}~ \vec 0
            \quad\Rightarrow\quad \mat S_\mathsf B\vec r = \lambda\,\mat S_\mathsf W\vec r
          \end{eqnarray*}
          }
          \pause
    \item Multiplying by $\vec r^T$ from the left: $\;J(\vec r) = \lambda$. \\
          Hence $\vec r^*$ is the generalized eigenvector with the \structure{largest} eigenvalue $\lambda$. \\[.1cm]
          (The norm $\|\vec r\|_2=1$ from the projection step is obtained by rescaling afterwards.)
  \end{itemize}
\end{frame}
```

(Uses the symbols $\mat S_\mathsf B$, $\mat S_\mathsf W$ exactly as defined on the previous slides. The quotient-rule route is an equivalent alternative.)

---

## 6. Chapter 12 — Signed distance to the hyperplane

**File:** `12_svm.tex` — frame *Remarks on Linear Algebra (cont.)*, first bullet: "The signed distance $d$ of a point $\vec x$ to the hyperplane is: $d = \frac{\|\vec\alpha\|_2}{\vec\alpha^T\vec\alpha} f(\vec x) = \dots$".

**Missing:** where the formula comes from. Insert a short derivation (e.g. as a new frame directly before this one, or replace the first equality by the steps below).

```latex
\begin{frame}
  \frametitle{Remarks on Linear Algebra \cont}

  \structure{Signed distance to the hyperplane} $\{\vec x: f(\vec x) = \vec\alpha^T\vec x+\alpha_0 = 0\}$:
  \begin{itemize}
    \item Decompose $\vec x$ into its orthogonal projection $\vec x_\perp$ onto the hyperplane
          and a step of length $d$ along the unit normal $\vec n = \vec\alpha/\|\vec\alpha\|_2$:
          {\small
          \begin{displaymath}
            \vec x = \vec x_\perp + d\,\frac{\vec\alpha}{\|\vec\alpha\|_2}, \qquad f(\vec x_\perp) = 0
          \end{displaymath}
          }
          \pause
    \item Apply $f$ to both sides:
          {\small
          \begin{displaymath}
            f(\vec x) = \underbrace{\vec\alpha^T\vec x_\perp + \alpha_0}_{=\,f(\vec x_\perp)\,=\,0}
                        + d\,\frac{\vec\alpha^T\vec\alpha}{\|\vec\alpha\|_2}
                      = d\,\|\vec\alpha\|_2
            \quad\Rightarrow\quad
            d = \frac{f(\vec x)}{\|\vec\alpha\|_2}
          \end{displaymath}
          }
          \pause
    \item $d>0$ on the side the normal $\vec\alpha$ points to, $d<0$ on the other side.
  \end{itemize}
\end{frame}
```

---

## 7. Chapter 18 — From the gradient to $\hat{\vec\beta} = \mat H\,\overline{\vec R}$

**File:** `18_em_applications.tex` — frames *Gradient Computation* … *Gradient Computation (cont.)*. Three small gaps:

**7a.** In the second *Gradient Computation (cont.)* frame, the step from $\sum_k p_k\,\frac{\partial}{\partial\beta_i}\mathcal N(\dots)$ to $\sum_k p_k\,\mathcal N(\dots)\,\psi_k^{-1}(Y_i-\mu_k-\beta_i)$ uses the derivative of the Gaussian. Add one line under the first equation:

```latex
  {\footnotesize using $\frac{\partial}{\partial\beta_i}\mathcal N(Y_i;\mu_k+\beta_i,\psi_k)
     = \mathcal N(Y_i;\mu_k+\beta_i,\psi_k)\,\psi_k^{-1}(Y_i-\mu_k-\beta_i)$}
```

**7b.** In the last *Gradient Computation (cont.)* frame, the step $\frac{\nabla_{\vec\beta}p(\vec\beta)}{p(\vec\beta)} = -\mat\Psi_{\vec\beta}^{-1}\vec\beta$ needs the prior. Add after the first equation line:

```latex
  {\footnotesize with the zero-mean Gaussian prior $p(\vec\beta)=\mathcal N(\vec\beta;\vec 0,\mat\Psi_{\vec\beta})$:
   $\;\frac{\nabla_{\vec\beta}\,p(\vec\beta)}{p(\vec\beta)} = \nabla_{\vec\beta}\log p(\vec\beta) = -\mat\Psi_{\vec\beta}^{-1}\vec\beta$}
```

**7c.** Between "$\stackrel{!}{=}\vec 0$" and "It follows that $\hat{\vec\beta}=\mat H\overline{\vec R}$", add the rearrangement and why it is solved iteratively:

```latex
  {\small
  \begin{displaymath}
    \overline{\vec R} - \big(\mat D + \mat\Psi_{\vec\beta}^{-1}\big)\,\vec\beta = \vec 0
    \quad\Rightarrow\quad
    \vec\beta = \big(\mat D + \mat\Psi_{\vec\beta}^{-1}\big)^{-1}\,\overline{\vec R}
  \end{displaymath}
  }
  This is linear in $\vec\beta$ only if the weights $W_{ik}$ (and hence $\overline{\vec R}$, $\mat D$) are held fixed:
  compute $W_{ik}$ with the current estimate $\hat{\vec\beta}^{(j)}$ (E-step), then solve for $\hat{\vec\beta}^{(j+1)}$ (M-step).
```

If the frame becomes too long, move the last paragraph ("$\mat H$ is a linear operator …") to a new frame `Gradient Computation \cont`.

---

## Checklist
- [ ] 1 — Ch 20 bias–variance derivation frame added
- [ ] 2 — Ch 17 two GMM M-step frames added
- [ ] 3 — Ch 10 three image frames replaced by two LaTeX frames
- [ ] 4 — Ch 14 two soft-margin dual frames added + note on hard-margin implications slide
- [ ] 5 — Ch 07 Rayleigh-quotient frame added
- [ ] 6 — Ch 12 signed-distance frame added
- [ ] 7 — Ch 18 three additions (7a, 7b, 7c)
- [ ] Every changed chapter compiles without errors; changed slides checked for overflow

# Pattern Recognition slides — change log for WS 2026/27

Reference version: `sheethalb/PR_Lecture_Slides`, folder `refactored` (commit "refactored v1" = the unchanged lab slides).
Companion file: `notation_pass_WS2627.patch` — a unified diff of **every** change below against the original lab sources (LaTeX `.tex` chapters + `texfig_c/*.pstex_t` figure labels). If your Overleaf project has the original lab sources, the patch can be applied directly (`git apply notation_pass_WS2627.patch`); otherwise use this checklist and look up the exact LaTeX in the patch.

**Instructions for an editing agent:** work chapter by chapter. For each item, find the frame by its title (given in *italics*), make the change, and tick it. Keep beamer overlays (`\pause`, `\alt`, `\only`) intact. Compile after each chapter. Do **not** change `p(·)` to `P(·)` anywhere (decision pending).

## 0. Course-wide conventions (apply everywhere)

| Concept | Notation |
|---|---|
| True class label (ground truth) | $y$, training labels $y_i$ |
| **Predicted** label (output of a classifier) | $\hat y$ |
| **Optimal** prediction (Bayes decision, argmin of expected loss) | $\hat y^*$ |
| Estimates of parameters | hat: $\hat\theta$, $\hat{\vec\mu}$, $\hat{\mat\Sigma}$ |
| Hidden / latent variables | $z$ (never $y$) |
| Training set | $S=\{(\vec x_i,y_i)\}_{i=1}^m$; $m$ samples, $d$ dimension, $\vec x_i$ = $i$-th sample, $x_{i,j}$ = $j$-th component |
| Label coding | stated at first use in every chapter; one-line reminder wherever it switches ($\{0,1\}$, $\{1,2\}$, $\{-1,+1\}$) |
| Probabilities / densities | single letter $p(\cdot)$ (pmf for discrete, pdf for continuous); random variable and value not distinguished (convention stated in Ch. 02) |
| Parameters vs. conditioning | parameters after `;` e.g. $p(\vec x;\vec\theta)$, conditioning after `|` e.g. $p(\vec x|y)$; Gaussians $\mathcal N(\vec x;\vec\mu,\mat\Sigma)$ |
| Star | optimum only ($\vec x^*$, $p^*$, $\hat y^*$); never ground truth |

Chapters that follow a textbook's notation got a frame **"Notation in this Chapter"** (08, 11, 13, 18, 19, 20, 21) instead of mass renaming.

---

## 00 Cover / pr.tex (done by Sheethal)

## Build fixes (only needed if starting from the lab repo)
  `\AtEndDocument{\immediate\write\csname @mainaux\endcsname{\string\newlabel{LastPage}{{}{\number\numexpr\value{page}-1\relax}{}{}{}}}}`


## Open decisions (not yet changed)
- [ ] $p(\cdot)$ vs. $P(\cdot)$ for probabilities (ask professor); if switched, also revisit random-variable notation ($P(Y=y)$).
- [ ] Sigmoid kernel uses $\alpha,\beta$ (clash with SVM $\vec\alpha$) — Ch. 14/15.
- [ ] Ch. 16: $L$ = Laplacian and Lagrangian.
- [ ] Ch. 18: $Y_i$ (observed) uses the label letter (flagged in notation box only).
- [ ] Ch. 07: claim "PCA features approx. Gaussian (CLT)" is questionable content.
- [ ] Ch. 14: soft-margin box constraint $0\le\lambda_i\le\mu$ never derived.
- [ ] Figure labels were edited in `texfig_c/*.pstex_t`; regenerating figures from `texfig/*.fig` on the lab server would restore the old labels.

---

## DONE in this Overleaf notes project (moved from above)

- [x] Rank-reduced LDA: $L\le K-1$; constraints $i=1..L$; define $\lambda_i$, $\bar\mu'$, $\Sigma_{\text{inter}}$; **error fix** eigen-equation $\mat\Sigma_{\text{inter}}\mat\Phi^T=\mat\Phi^T\mat\Lambda'$ with $\mat\Lambda=\mathrm{diag}(\lambda_i)$, $\mat\Lambda'=-\mat\Lambda$ (also in the PCA note); "Principle" → "Principal".
- [x] $\mathcal M$ = set of **indices**, misclassification $\le 0$ (also in the convergence proof).
- [x] Fisher kernels: $\mat I(\vec x)\to\mat I(\vec\theta)$.
- [x] EM slide: $W_{ik}^{(j)}$ with $\hat\beta_i^{(j)}$, $\hat{\vec\beta}^{(j+1)}\leftarrow\mat H^{(j)}\bar{\vec R}^{(j)}$, init $\hat{\vec\beta}^{(0)}=\vec0$; $\mathcal N(\cdot;\cdot,\cdot)$.
- [x] *Postulates for Pattern Recognition*: footnote — in Niemann's notation $\vec x$ is a position (e.g. in the image), not a feature vector; $N$ = number of patterns in $\omega$.
- [x] *Performance Evaluation* (confusion matrix): caption defines $n_{\kappa\lambda}$ and states reference = true class $y$ (rows), hypothesis = predicted class $\hat y$ (columns).
- [x] *Performance Evaluation (cont.)* (ROC): threshold $\theta$ → $t$; "threshold decision on the posterior of the positive class (in general at 0.5), equivalently a threshold $t$ on the eye pressure"; "eye-pressure thresholds $t\in[0,40]$".
## 05 Naive Bayes
- [x] "class dependent pdf" → "class-conditional pdf $p(\vec x|y)$" (also in Comprehensive Questions).
- [x] Independence: "**conditionally** independent given the class $y$".
- [x] Decision: $\hat y^*=\argmax p(y|\vec x)$ (optimal) vs. naive-Bayes decision $\hat y=\argmax_y p(y)\prod_i p(x_i|y)$ + one sentence on the difference.
- [x] Gaussian example: class subscripts $\mat\Sigma_y$, $\mathcal N(x_i;\mu_{y,i},\sigma^2_{y,i})$; $i\in\{1,\dots,100\}$.
- [x] Logit: "two classes $y\in\{0,1\}$"; $\alpha_{0,i}(x_i)\to\alpha_i(x_i)$ with $\alpha_0=\log\frac{p(y=0)}{p(y=1)}$, $\alpha_i(x_i)=\log\frac{p(x_i|y=0)}{p(x_i|y=1)}$; "this is $F(\vec x)$ of Chapter 03".
- [x] First-order dependency: last "=" marked as assumption $p(x_i|y,x_1..x_{i-1})=p(x_i|y,x_{i-1})$.
- [x] **Error fix** (two *Naive Bayes (cont.)* example frames): first-order dependency → the **inverse** covariance (precision) $\mat\Sigma^{-1}$ is tridiagonal ($\mat\Sigma$ itself in general dense); matrix entries $\sigma_{i,j}\to q_{i,j}$, tied diagonal $q_{i,i}=q$.
## 04 Logistic Regression II
- [x] *Parameterization*: lifted coefficients named $\vec a$ ("Rewrite $F(\vec x)=\vec a^T\vec x'$"); definition: "$\vec\theta$ is a lifted parameter vector ($\vec\theta=-\vec a$ under the convention below) and $\vec x$ now denotes the lifted feature vector $\vec x'$".
- [x] *Log-Likelihood Function*: label coding $y\in\{0,1\}$; posteriors $p(y=\cdot|\vec x;\vec\theta)$; **note**: "Chapter 03 wrote $p(y=0|\vec x)=g(F(\vec x))$. Here the sigmoid models class $y=1$, i.e. $\vec\theta^T\vec x=-F(\vec x)$."
- [x] Bernoulli form $p(y|\vec x;\vec\theta)$ + "requires $y\in\{0,1\}$"; likelihood $\prod p(y_i|\vec x_i;\vec\theta)$.
- [x] Maximization: ML estimate $\hat{\vec\theta}=\argmax\mathcal L(\vec\theta)$; iterates $\vec\theta^{(k)}$ ($k$ iteration counter) → $\hat{\vec\theta}$.
- [x] Newton–Raphson: Taylor order $k\to n$ (k only counts iterations); "(here $x$ is a scalar variable)".
- [x] Gradient slides: define $\theta_j$ = $j$-th component.
- [x] **New frame** *Decision Rule*: $\hat y=1\Leftrightarrow g(\hat{\vec\theta}^T\vec x)>0.5\Leftrightarrow\hat{\vec\theta}^T\vec x>0$, else 0; boundary $\hat{\vec\theta}^T\vec x=0$; $\hat y$ vs. true labels $y_i$.

- [x] Quadratic polynomial slide: $a_{11}x_1^2+(a_{12}+a_{21})x_1x_2+a_{22}x_2^2+\alpha_1x_1+\alpha_2x_2+\alpha_0$ (instead of $a\dots f$).
- [x] Distributions unified: $p(x;\lambda)$ (exponential), $p(k;n,\pi)$ binomial (caption "…success probability $\pi$"), $p(k;\lambda)$ Poisson, $p(k;N,M,n)$ hypergeometric; figure labels in `exponential1–4`, `binomial1–3` (legend $p=\to\pi=$), `poisson1–3`, `hypergeometric1–3`.
## 06 Discriminant Analysis
- [x] *Discriminant Analysis*: "discriminative" → **generative** modeling (posterior via $p(y)p(\vec x|y)$); summation index $y'$.
- [x] LDA algorithm: $\hat{\vec\mu}_y=\frac1{m_y}\sum_{i:y_i=y}\vec x_i$ ($m_y$ defined); $\hat{\mat\Sigma}$ uses $\hat{\vec\mu}_{y_i}$; $\phi(\vec x)=\mat D^{-1/2}\mat U^T\vec x$; decisions $\hat y$ using $\phi(\hat{\vec\mu}_y)$, note plug-in $\hat y$ approximates $\hat y^*$; 2-class slide "$y\in\{0,1\}$, equal priors".
    
- [x] p. 8 after the UAR formula: “$\kappa$ is the total number of classes” (wrong) → “$K$ is the number of classes, $\kappa$ the class index”.
- [x] p. 18 posterior derivation, 3rd line: spurious trailing factor “$\cdot p(y=0\mid\vec x)$” → delete.
- [x] p. 20 proof of Lemma 1: remove the “$=0$” tautology; prove $p(y=0\mid\vec x)=\tfrac12 \Leftrightarrow F(\vec x)=0$ cleanly.
- [x] p. 23 §3.3.4 Gaussian bullet: don’t call the Gaussian pdf “decision boundary”; phrase as “class-conditional density is …”.
- [x] p. 23 §3.3.4 intro: exponential-family condition must match Lemma 2 (“same family with equal dispersion $\phi$”).
- [x] p. 25 definition under Fig. 13: “$F(\vec x)=\vec\theta^T\vec x$ … ($\vec\theta=-\vec a$)” → “$-F(\vec x)=\vec\theta^T\vec x$ with $\vec\theta=-\vec a$”.
- [x] p. 29 Hessian bullet: replace “double derivative w.r.t. $x$ and $y$” by “second derivatives w.r.t. the components of $\vec\theta$”.
- [x] p. 36 conclusion: linear boundary claim must be restricted to the shared-transform/shared-covariance case; say hyperplane (not line) for $d>2$.
- [x] p. 39 $\vec\mu'_y\in\mathbb R^{K-1}$, $\mat\Phi\in\mathbb R^{L\times(K-1)}$: dimensionality mismatch (since $\phi:\mathbb R^d\to\mathbb R^d$ earlier) → either project to $(K-1)$ first and say so, or take $\mat\Phi\in\mathbb R^{L\times d}$.
- [x] p. 41 “In original PCA: $\Sigma\Phi^T = \lambda'\Phi^T$”: eigenvalue matrix must multiply from the right → $\Sigma\Phi^T=\Phi^T\Lambda'$.
- [x] p. 42 sums for $\vec\mu_k,\mat S_k,\tilde\mu_k,\tilde s_k^2$: fix index from $\sum_{i=1,\,y_i=k}^{m_k}$ to $\sum_{i:\,y_i=k}$.
- [x] p. 43 $\vec r^* = \argmax\{\vec r^T\Sigma_{\text{inter}}\vec r - \lambda\,\vec r^T\Sigma_{\text{intra}}\vec r\}$: constraint constant missing; Lagrangian form should be $\mathcal L(\vec r,\lambda)=\vec r^T\Sigma_{\text{inter}}\vec r-\lambda(\vec r^T\Sigma_{\text{intra}}\vec r-1)$ and solve $\nabla_{\vec r}\mathcal L=\vec 0$.
- [x] p. 57/58 perceptron: misclassification uses $\le 0$ vs proof’s $<0$; allow equality at init; fix superscript indexing $(k)$ vs $(k-1)$.
- [x] p. 64 “$f(\vec x^{(k+1)})<f(\vec x^{(k)})$, i.e. $\nabla f^T\Delta\vec x<0$”: rephrased as a descent-direction requirement.
- [x] p. 70 hard-margin note: constraints keep samples at least margin away; objective maximises margin (rephrased).
- [x] p. 82 kernel PCA: restrict the “linear combination” statement to $\lambda_i\ne 0$.
- [x] p. 83 kernel PCA projection: add normalisation ($\|\vec e_i\|_2=1$) and note null-space ambiguity; avoid incorrect eigenvector claims.
- [x] p. 85 Fisher score definition: correct sign (no minus) and avoid misleading capitalization for vector-valued score.
- [x] p. 89 SVM dual: include the explicit dual optimisation statement.
- [x] p. 89 Laplacian SVM: clarify identity-matrix sizes ($\mat I_l$, $\mat I_m$) and state the invertibility assumption for canceling $\mat K$.
- [x] p. 93 EM: “will increase $L$” → “will not decrease $L$”.
- [x] p. 102 EM eq. (1)/(2): ensure both updates have correct left-hand sides (separate $W_{ik}^{(j)}$ update from $\hat{\vec\beta}^{(j+1)}$ update).
- [x] p. 111 Gaussian moments note: fix double factorial definition for even $n$.
- [x] p. 112 kurtosis argmax: include constraint $\|\vec w\|=1$.
- [x] p. 122 §19.3 first bullet: include defining basis expansion $f(\vec x)=\sum_{m=1}^M \beta_m b(\vec x;\vec\gamma_m)$.
- [x] p. 125 Viola–Jones weak classifier: keep $G_j(\vec x)\in\{-1,+1\}$ (or explicitly flag variants).
- [x] p. 124 Viola–Jones feature count statement is not present in this manuscript (nothing to fix).

---

## Completed review items

- [x] $L$: Lagrangian vs graph Laplacian (same equation); also subspace dimension, number of layers, log-likelihood. Reviewer request: use $\mathcal L$ for Lagrangian; reserve $L$ (or $\Delta_G$) for Laplacian.
- [x] $p$: density vs mixture weight $p_k$ vs responsibility $p_{ik}$ → use $\pi_k$ and $\gamma_{ik}$.
- [x] $\lambda$: eigenvalue vs Lagrange multiplier vs ridge weight vs learning rate, etc.
- [x] $D$: DTW distance vs degree matrix vs dimension.
- [x] $F(\vect x)$: log-odds vs true label vs posterior symbol.
- [x] Fix listed typos: double “+” line break; broken legend “$p(x\mid y=0\mid$”; define $r$ in Fig. 13 caption (“plane $z=r^2$”);
      change exact “=” stopping tests to tolerances; spacing consistency for conditionals $p(y\mid\vect x)$; etc. (see reviewer note).
- [x] Undefined symbols list: ensure each is defined where first used (e.g. $\Omega$, $\omega$ vs $w$, $x^*$ in Fig. 5, etc.).
- [x] $c$: constant offset vs polynomial coefficient vs $c(\vect x,\phi)$ in exponential family.
      *Done:* offset symbol removed (p. 21, the constant is written out and noted as part of $\alpha_0$); polynomial coefficients already $a_{ij},\alpha_i$; $c(\vect x,\phi)$ kept as standard exponential-family notation.

- [x] $\alpha_0,\alpha_i$: inconsistent meanings across logistic / naive Bayes parts.
      *Done:* Naive Bayes additive model (p. 31-32) now uses $f_0$, $f_i(x_i)$, with a note on why it differs from $\alpha_0,\alpha_i$ in Chapter 03. $\alpha_0,\vect\alpha$ keep their Chapter 03 meaning everywhere else.

- [x] $S$: training set vs scatter matrices vs sparsity level.
      *Done:* sparsity level renamed $S\to s$ ("$s$-sparse", Compressed Sensing). Scatter matrices stay $\mat S_k,\mat S_\mathsf W,\mat S_\mathsf B$: they are bold matrices, so they no longer clash with the (non-bold) training set $S$ under the bold-matrix convention.

- [x] $d$: signed distance vs dimension.
      *Done:* signed distance renamed $d\to\delta(\vect x)$ in the SVM I derivation (p. 69); $d$ is the dimension everywhere else. $d^*$ (dual optimum, Optimization II) kept as standard Boyd notation.

- [x] $I$: Fisher information vs identity vs indicator vs image intensity.
      *Done:* Fisher information already $\mathcal I(\vec\theta)$, identity already bold $\mat I$ (sizes $\mat I_l,\mat I_m$ in Laplacian SVM). AdaBoost: indicator function $I(\cdot)\to\mathbb I(\cdot)$ (9 occurrences + notation list, p. 121-123); $I(x,y)$ kept for image intensity and now defined under the integral image (p. 125).

- [x] $M$: misclassified set vs max norm vs neurons per layer.
      *Done:* perceptron convergence bound $M=\max_i\|\vect x_i\|_2\to R$ (Novikoff notation, p. 58, 5 occurrences). Misclassified set is already calligraphic $\mathcal M$; $M^{(l)}$ stays neurons per layer (MLP).

- [x] $\vect e_i$: basis vector vs PCA eigenvector.
      *Done:* Kernel PCA eigenvectors renamed $\vec e_i\to\vec v_i$ (10 occurrences, p. 82-83); $\vect e_i$ stays the unit basis vector (Optimization I, p. 66).

- [x] $J$: Fisher score vs functional derivative vs negentropy.
      *Done:* Fisher score already $\vec u_{\vec\theta}(\vec x)$ (p. 85). Max-entropy derivation (ICA, p. 109): $\delta J/\delta p\to\delta\mathcal L/\delta p$, matching the functional $\mathcal L(p)$ defined just above. $J$ now only denotes negentropy; bold $\mat J_{\mathcal L}$ (Laplacian SVM selection matrix) is a matrix and unaffected.

- [x] $\vect\mu'_y$: transformed true mean vs pooled transform of estimate.
      *Done:* class-specific transform (p. 36): intermediate names $\vect\mu'_y,\mat\Sigma'_y$ removed, the density is written directly as $\mathcal N(\vect x';\mat D_y^{-1/2}\mat U_y^T\vect\mu_y,\mat I)$. $\vect\mu'_y=\phi(\hat{\vect\mu}_y)$ (LDA, pooled transform of the estimate) is now the only meaning.

- [x] $\vect r$: Fisher direction vs residual vs LP bound variable.
      *Done:* Norms chapter: LP bound variables renamed $r\to t$ (Chebyshev) and $\vect r\to\vect t$ ($L_1$), as in Boyd (p. 52); $\vect r$ stays the residual in that chapter. Fisher direction $\vect r$ (Ch. 5, pp. 41-43) kept: different chapter, single meaning there.

- [x] Tilde notation overloaded (projected scalar / augmented vector / centred matrix).
      *Done:* verified, no edit needed: projected Fisher scalars already use $\mu_k^{\mathrm{proj}},(s_k^{\mathrm{proj}})^2$ and the centred matrix in Ch. 5 is gone, so in Ch. 5 tilde only marks the augmented vector $\tilde{\vect x}_i$. Other tildes are chapter-local with one meaning each (feasible point, Optimization II; centred $\tilde\phi,\tilde{\mat K}$, kernel PCA; bias-free intensity $\tilde X_i$, MR; whitened $\tilde{\vect x}$, ICA).

- [x] Index $i$ overloaded (component vs sample vs iteration index); reviewer request: use $j,k$ for components; keep iteration index stable (uses $j$ in EM).
      *Done:* Naive Bayes chapter (pp. 30-32): feature components now indexed by $j$ ($x_j$, $\prod_j$, $\mu_{y,j}$, $f_j(x_j)$), $i$ stays the sample index; consistent with $x_{i,j}$ in logistic regression. EM iteration index was already $(j)$ throughout (GMM, general EM, MR bias field), no edit needed.

- [x] $y$: neuron outputs vs targets.
      *Done:* kept as is (decision by Sheethal, 12 Nov): neuron outputs carry the layer superscript $y_j^{(l)}$, targets have none ($y_k$), prediction $\hat y_k=y_k^{(L)}$; stated in the MLP Notation list and consistent with the slides.

- [x] Matrix/vector typeface consistency: pick one convention and apply consistently (reviewer lists mixed bolding and a stray “$\|\vec X\|_F$”).
      *Done:* convention: bold, as stated in main.tex. (1) \vect now uses \bm{\mathrm{.}}: Latin vectors unchanged, Greek vectors ($\vect\mu,\vect\alpha,\vect\theta,\dots$) are now bold too (\mathbf left them plain). (2) Ch. 13-16 file (chapter_15_18.tex): all 478 arrow \vec -> bold \vect; Niemann postulate in Ch. 1 likewise. (3) Text under the Gaussian (p. 21): $\mat\Sigma$, $\vect\mu$; ridge "Matrix $\mat X$"; GMM $\partial L/\partial\mat\Sigma=\mat 0$ (zero matrix). Frobenius norm already $\|\mat X\|_F$. Not changed: vector-valued $\phi(\vect x)$ stays non-bold (function symbol).

---

## Completed chapter items (notes project)

- [x] "Winter term 2025/26" → "2026/27" on both cover frames (`00_cover.tex`) and in `\date` (`pr.tex`).
      *Notes:* N/A for notes (slide cover). Notes title page: authors Sheethal Bhat, Andreas Maier.
- [x] Author acknowledgement: "…Rodriguez, Das, Bhat, and Maier" on **both** cover frames (presentation and handout). Footer `\author[...]` unchanged.
      *Notes:* N/A for notes (slide cover frames).
- [x] `pr.tex` starts with `\documentclass[aspectratio=43,t,10pt]{beamer}` + `\def\shadow{true}` instead of `\input{header}` (symlink). Handouts: `\input{header.A5}` / `\input{header.A6}`.
      *Notes:* N/A for notes (beamer build only).
- [x] Copy `latex-templates/theme` into `theme/` (submodule/symlink not available on Overleaf).
      *Notes:* N/A for notes (beamer theme).
- [x] `header.A5`, `header.A6`: replace `\usepackage{lastpage}` with
      *Notes:* N/A for notes (beamer handouts).
- [x] *Classification of Simple Patterns*: pipeline arrow labels $\vec c$ → $\vec x$ (features) and $y$ → $\hat y$ (output); add key below: $\vec f$ pattern, $\vec g$ preprocessed pattern, $\vec x$ feature vector, $\hat y$ class predicted by the classifier.
      *Notes:* N/A for notes: the notes have no pipeline figure.
- [x] *(cont.)* supervised learning: "each consisting of a feature vector and its **true** class label"; $y_i\in Z$ → $y_i\in\mathcal Y$, "true class label (ground truth)".
      *Notes:* already in notes (Ch. 2 intro: true class label, $y_i\in\mathcal Y$).
- [x] *Bayesian Classifier* notation slide rewritten: $\vec x\in\mathbb R^d$ (observed); $y\in\mathcal Y$ true label, $\mathcal Y=\{1,\dots,K\}$ (two classes $\{0,1\}$ or $\{-1,+1\}$, always stated); $\hat y$ predicted; $\hat y^*$ optimal (Bayes) prediction; $p(y)$ prior; $p(\vec x)$ evidence (density); $p(\vec x,y)$ **joint distribution** (not "joint pdf"); $p(\vec x|y)$ class-conditional density; $p(y|\vec x)$ posterior.
      *Notes:* already in notes (Sec. Notation).
- [x] **New frame** *Bayesian Classifier (cont.)* "Probabilities vs. densities": pmf vs pdf, mixed joint, convention "same letter $p$; $p(y)$ short for $P(Y=y)$", and "true vs. predicted class: correct on $\vec x_i$ if $\hat y=y_i$".
      *Notes:* already in notes (paragraph after the notation list).
- [x] Bayes-rule underbraces as upright text: `\text{joint}`, `\text{prior}`, `\text{class-conditional pdf}`, `\text{evidence}`, `\text{posterior}`.
      *Notes:* already in notes.
- [x] Decision rule: "The optimal prediction $\hat y^*$ is the class with the highest posterior: $\hat y^*=\argmax_y p(y|\vec x)$…".
      *Notes:* already in notes.
- [x] *Optimality*: loss $l(y',y)$ = loss of assigning true class $y$ to class $y'$; 0/1 loss with `\text{if}`/`\text{otherwise}`; expected loss $\mathsf{AL}(\vec x,y')=\sum_y l(y',y)\,p(y|\vec x)$ + sentence "the true class is unknown, so we average over its posterior"; $\hat y^*=\argmin_{y'}\mathsf{AL}=\argmin_{y'}(1-p(y'|\vec x))=\argmax_{y'}p(y'|\vec x)$ (step $1-p$ now shown).
      *Notes:* already in notes. Also: figure caption now defines $x^*$ (crossing point = decision boundary).
- [x] "The $(0,1)$-loss function is \textbf{not} convex."
      *Notes:* notes said "The loss function is NOT convex" -> "The $(0,1)$-loss function is NOT convex".
- [x] *Posteriors and the Logistic Function (cont.)*: define $F(\vec x):=\log\frac{p(y=0|\vec x)}{p(y=1|\vec x)}$ next to $p(y=0|\vec x)=1/(1+e^{-F})$; "$F$ is the log-odds of class 0 vs. class 1".
      *Notes:* already in notes.
- [x] Logistic function uses scalar $z$: $g(z)=1/(1+e^{-z})$, $z\in\mathbb R$ "(a scalar, not a feature vector)"; derivative slide $x\to z$; caption $g(az)$; figure labels `sigmoid1–4.pstex_t`: $x\to z$, $g(ax)\to g(az)$.
      *Notes:* already in notes (text and figure caption); pstex figures N/A.
- [x] *Decision Boundary*: remove undefined $\delta(\vec x)$; "separates the regions where the classifier decides for class 0 and class 1".
      *Notes:* already in notes.
- [x] **New frame** *Decision Rule*: $\hat y^*=0$ if $F(\vec x)>0$ ($p(y=0|\vec x)>\frac12$), $1$ if $F<0$; $F=0$ is the boundary; note that $\hat y^*$ is the predicted class and the true class can differ.
      *Notes:* already in notes (Sec. Decision Rule, Ch. 3).
- [x] Gaussian example: $p(\vec x|y)=\mathcal N(\vec x;\vec\mu_y,\mat\Sigma_y)=\dots$; typo `\mat{\mu}_0` → `\vec{\mu}_0`.
      *Notes:* already in notes; text below now says $\mat\Sigma_y$, $\vect\mu_y$ of class $y$.
- [x] **Error fix** — *Example cont.* (quadratic case): $\vec\alpha^T=\vec\mu_0^T\mat\Sigma_0^{-1}-\vec\mu_1^T\mat\Sigma_1^{-1}$ (sign was flipped).
      *Notes:* checked: notes have $\vect\alpha^T=\vect\mu_0^T\mat\Sigma_0^{-1}-\vect\mu_1^T\mat\Sigma_1^{-1}$; full derivation of $\mat A,\vect\alpha,\alpha_0$ re-derived and correct.
- [x] *Equal Dispersion*: "the argument $F(\vec x)$ is **affine** in $\vec x$"; **error fix** $\alpha_0=\log\frac{p(y=0)}{p(y=1)}+\frac12(\vec\mu_1+\vec\mu_0)^T\mat\Sigma^{-1}(\vec\mu_1-\vec\mu_0)$ (was $\vec\mu_1-\vec\mu_0$ in the first factor).
      *Notes:* checked: notes say affine and have the corrected $\alpha_0$ (verified: $\vect\mu_1^T\mat\Sigma^{-1}\vect\mu_1-\vect\mu_0^T\mat\Sigma^{-1}\vect\mu_0=(\vect\mu_1+\vect\mu_0)^T\mat\Sigma^{-1}(\vect\mu_1-\vect\mu_0)$).
- [x] Exponential family: $\vec\theta\to\vec\eta$ "natural (canonical) parameter vector"; add line on `;` vs `|`.
      *Notes:* already in notes.
- [x] Gaussian pdf: `\det(2\pi\mat\Sigma_y)` → `\det(2\pi\mat\Sigma)` (2×).
      *Notes:* already in notes.
- [x] Figure `perceptron.pstex_t`: $\alpha_i\to\theta_i$, $\sum\theta_i x_i=\vec\theta^T\vec x$, $1/(1+e^{-\vec\theta^T\vec x})$.
      *Notes:* N/A for notes: no perceptron figure in Ch. 4.
- [x] Gaussian classifier: "joint covariance" → "shared (pooled) covariance"; decisions with true parameters = $\hat y^*$; components $x_j$; "Nearest Neighbor" → "nearest class mean" (also conclusions, caption, lessons; figure `lda_nearest_neighbor.pstex_t`: $\hat\mu$).
      *Notes:* already in notes. Also: Mahalanobis distance now defined as the square root (the $\frac12$ quadratic form is half its square, same argmin); identity-covariance bullet now says "in addition" (equal priors needed).
- [x] *Feature Transform*: "positive **definite**"; $d_{i,i}\to\lambda_i$, $\mat D=\mathrm{diag}(\lambda_i)$.
      *Notes:* already in notes.
- [x] Fisher: "$y\in\{1,2\}$"; sums $\sum_{i:y_i=k}$, $m_k=|\{i:y_i=k\}|$; "$\vec\mu_k,\mat S_k$ are sample estimates"; $\Sigma_{\text{inter}}$/$\Sigma_{\text{intra}}$ related to $\mat S_B$/$\mat S_W$.
      *Notes:* added: $y\in\{1,2\}$, $m_k$, "sample estimates"; $\Sigma_{\text{inter}}=\frac14\mat S_\mathsf B$, $\Sigma_{\text{intra}}=\frac1m\mat S_\mathsf W$ for two classes (now defined). Normalisation made consistent ($R(\vect r)$ is scale-invariant, $\vect r^*\propto\mat S_\mathsf W^{-1}(\vect\mu_1-\vect\mu_2)$); axis $\vect a^*\to\vect r^*$.
- [x] PCA components "uncorrelated" (not independent); columns of $\mat X$ "linearly independent".
      *Notes:* already in notes; wording of the Gaussian remark cleaned up.
- [x] adidas / Notes on Regression: $\hat y=\mathrm{sgn}(\dots)$ + reminder $y\in\{-1,+1\}$.
      *Notes:* already in notes (Linear Regression: $\hat y=\mathrm{sgn}(\cdot)$, $y\in\{-1,+1\}$); adidas section has no formula. "Notes on Regression" intro rewritten (regression = continuous target).
- [x] Linear regression: augmented $\tilde{\vec x}_i=(\vec x_i^T,1)^T$, $\vec\theta^T\tilde{\vec x}_i$.
      *Notes:* already in notes.
- [x] Ridge: $\vec\theta\sim\mathcal N(\vec 0,\tau^2\mat I)$, intercept not in the prior; likelihood "$y_i\sim\mathcal N(\dots)$, i.e. $p(y_i|\vec x_i,\vec\alpha)=\dots$", prior "i.e. $p(\alpha_j)=\dots$".
      *Notes:* prior now on $\vect\alpha$ only (no prior on the intercept), consistent with $p(\alpha_j)$, $j=1..d$; ridge objective notes that $\alpha_0$ would be penalized as written and $\lambda>0$ is stated; lasso likewise.
- [x] **Error fix** MAP derivation: $\argmax_{\vec\alpha}p(\vec\alpha|S)=\argmax\{p(\vec\alpha)\prod_i p(y_i|\vec x_i,\vec\alpha)\}=\dots$ (prior once, $\vec x_i$ in the residual); summary slide likewise with $(\mat X\vec\theta-\vec y)$, $\vec\theta=(\vec\alpha^T,\alpha_0)^T$, "intercept not penalized".
      *Notes:* checked: notes have prior once and $\vect x_i$ in the residual; summary step relabelled "the same in matrix notation".
- [x] **New frame** *Notation in this Chapter*: $\mat A\leftrightarrow\mat X$, $\vec x\leftrightarrow\vec\theta$, $\vec b\leftrightarrow\vec y$; $\hat{\vec x}$ estimate, $\vec x_0$ true value; $\vec r$ residual; $\phi$ penalty.
      *Notes:* already in notes.
- [x] $L_2$ norm = square root of the sum of squares; "$L_{\mat 1}$" → "$L_{\mat I}$"; $\vec x^*$ (true value) → $\vec x_0$; "linearly independent" columns.
      *Notes:* already in notes.
- [x] $\preceq$ = componentwise; $\mat 1$ = all-ones vector.
      *Notes:* already in notes.
- [x] Ridge/Lasso objectives: $\|\mat A\vec x-\vec b\|_2^2+\lambda\|\vec x\|_2^2$ (and $\lambda\|\vec x\|_1$) — `\mat` placement fixed, squared residual.
      *Notes:* already in notes.
- [x] Compressed sensing: "can be rewritten as a **linear** program"; penalty slides state $a>0$.
      *Notes:* already in notes; added the missing "with parameter $a>0$" for the large-error penalty.
- [x] $y\in\{-1,+1\}$; $y_i$ true label; $\hat y=\mathrm{sgn}(\vec\alpha^T\vec x+\alpha_0)$ prediction.
      *Notes:* already in notes.
- [x] $\lambda$ = learning rate ("written $\eta$ in the MLP chapter"); remark on stacking $(\alpha_0;\vec\alpha)$ vs. $(\vec\alpha;\alpha_0)$ in Ch. 07.
      *Notes:* notes use $\eta$ for the learning rate in both perceptron and MLP (removes the $\lambda$ overload); stacking remark $(\alpha_0;\vect\alpha)$ vs. $(\vect\alpha;\alpha_0)$ added.
- [x] "Schwartz" → "Schwarz" (2×).
      *Notes:* already correct in notes.
- [x] **New frame** *Notation*: layers $l=0..L$ ($L$: number of non-input layers), $M^{(l)}$, $y^{(0)}=\vec x$, $w_{ij}^{(l)}$, $w_{0j}$, $\vec w$, net, $f$, output $\hat y_k=y_k^{(L)}$, target $y_k$.
      *Notes:* already in notes. Backpropagation derivation re-checked (output and hidden sensitivities, update rule): correct.
- [x] Target $t_k\to y_k$, output $y_k^{(L)}\to\hat y_k$ in error and δ derivations; figures `mlp`, `backpropagation{,2,3}.pstex_t` outputs $\hat y_k$; `activation.pstex_t` $F(\sigma)\to f(\text{net})$.
      *Notes:* already in notes; figures N/A.
- [x] Error: "squared error of one training pattern" (averaging over the set gives the MSE); $\varepsilon_{MSE}\to\varepsilon$; $\eta$ defined; bias sign explained (constant input $-1$); title $w_{ij}$; "Sensitivity".
      *Notes:* already in notes.
- [x] Linear network: extra `)` removed, no hats on $f$, $f_l(\vec z)=\mat W_l\vec z$, $(\mat W_l)_{ji}=w_{ij}^{(l)}$, loss $\mathcal L(\vec\theta)$ with $\vec\theta$ defined; captions of the 3 gradient PNGs map $\hat f$, $L(\theta)$, $y$ to the text symbols.
      *Notes:* already in notes; PNG captions N/A (no gradient figures in notes).
- [x] **New frame** *Notation in this Chapter*: $\vec x$ optimization variable (not features), $\vec y$ second point (not a label), $f,\nabla f,\nabla^2 f$, $\vec x^*$, $(k)$, $t^{(k)}$, $\Delta\vec x^{(k)}$, $\vec u$, $\alpha,\beta$ line-search parameters.
      *Notes:* already in notes.
- [x] Armijo: $\alpha\in(0,0.5)$, $\beta\in(0,1)$ (open).
      *Notes:* already in notes; the "halve the step" remark is now explained as $\beta=\frac12$.
- [x] Steepest descent: generic $\|\vec u\|$ "for a chosen norm ($L_1,L_2,L_\infty$ or $\|\cdot\|_{\mat P}$)".
      *Notes:* already in notes; added the $L_\infty$ steepest descent direction $-\mathrm{sgn}(\nabla f)$.
- [x] $L_2$: argmin $=-\nabla f/\|\nabla f\|_2$ (direction); unnormalized $-\nabla f$ used in practice.
      *Notes:* already in notes.
- [x] Quadratic norm renamed $\|\cdot\|_{\mat P}$ ($\mat P$ symmetric positive definite); change of variables $\vec x'=\mat P^{1/2}\vec x$, $f'(\vec x')=f(\mat P^{-1/2}\vec x')$; argmin over $\vec u'$; "$\propto$" where normalization dropped; result $-\mat P^{-1}\nabla f$; Newton: Hessian positive definite.
      *Notes:* already in notes; derivation re-checked ($\nabla f'(\vect x')=\mat P^{-1/2}\nabla f(\vect x)$, result $-\mat P^{-1}\nabla f$): correct. Newton step bracketed $(\nabla^2 f)^{-1}$.
- [x] $f$ = affine **decision function**; decision boundary $\{\vec x:f(\vec x)=0\}$; "margin $2/\|\vec\alpha\|_2$".
      *Notes:* already in notes.
- [x] $S=\{(\vec x_i,y_i)\}_{i=1}^m$, $y_i\in\{-1,+1\}$ (instead of $\{0,1\}$); $\hat y=\mathrm{sign}(f(\vec x))$.
      *Notes:* already in notes.
- [x] Soft margin: $\xi_i$ and $\mu>0$ defined where introduced.
      *Notes:* already in notes.
- [x] **New frame** *Notation in this Chapter*: $\vec x\in\mathbb R^n$, $f_0$, $f_i$ ($m$ = number of constraints, not samples), $h_i$ ($p$ equality constraints), $\lambda,\nu$, $p^*,d^*$, $\succeq$.
      *Notes:* already in notes.
- [x] Dual function: "pointwise infimum of a family of affine functions (hence concave)".
      *Notes:* already in notes; stray slide line "Neither $f_0$ nor $f_1$ is convex" rewritten as a remark, proof labelled.
- [x] `g(\vec{\lambda,\nu})` → $g(\vec\lambda,\vec\nu)$ (6×).
      *Notes:* already in notes.
- [x] **Error fix**: weak duality $d^*\le p^*$ always holds; $p^*>d^*$ = positive duality gap.
      *Notes:* already in notes.
- [x] Soft margin: define $\xi_i$, $\mu>0$, $m$ samples, $y_i\in\{-1,+1\}$.
      *Notes:* already in notes.
- [x] Multipliers for $\xi_i\ge0$ renamed $\eta_i$ (vector $\vec\eta$); "$\mu$ is also called $C$ in the literature"; **one frame deleted** (duplicate that renamed $\mu\to c$); derivative III: $\mu-\eta_i-\lambda_i=0$; duplicate `\subsection{Lagrangian}` removed.
      *Notes:* already in notes.
- [x] Dual: first line $L(\vec\alpha,\alpha_0,\vec\lambda)$, result $L_D(\vec\lambda)$, "$\vec\alpha,\alpha_0$ eliminated"; $\vec\lambda\succeq0$ explained.
      *Notes:* already in notes; dual derivation and box constraint $0\le\lambda_i\le\mu$ re-checked: correct.
- [x] Complementary slackness in SVM terms: $\lambda_i(y_i(\vec\alpha^T\vec x_i+\alpha_0)-1+\xi_i)=0$, $\eta_i\xi_i=0$.
      *Notes:* added soft-margin complementary slackness ($\lambda_i(\dots-1+\xi_i)=0$, $\eta_i\xi_i=0$) with the three cases for $\lambda_i$.
- [x] "slab" → margin hyperplanes $f(\vec x)=\pm1$; "norm vector" → "normal vector".
      *Notes:* done in notes.
- [x] Dual representation / feature transforms: $\hat y=\mathrm{sign}(f(\vec x))$, boundary $\{f=0\}$.
      *Notes:* added under the kernelized decision function; dual problem notes the soft-margin bound $\lambda_i\le\mu$.
- [x] Polynomial kernel exponent $k\to q\in\mathbb N$.
      *Notes:* done in notes ($q\in\mathbb N$).
- [x] Dual representation: $\hat y=\mathrm{sign}(f(\vec x))$, $y_i\in\{-1,+1\}$, $\lambda_i\ge0$; perceptron: meaning of $\mathcal E$, $\hat y=\mathrm{sign}(F(\vec x))$.
      *Notes:* already in notes; perceptron decision function $F\to f$ (log-odds clash), zero init/$\eta=1$ stated.
- [x] Kernel definition: input space $\mathcal X$ defined at first use; "for **some** feature mapping $\phi$".
      *Notes:* already in notes.
- [x] PSD proof with $\vec c\in\mathbb R^m$: $\vec c^T\mat K\vec c=\sum c_ic_jK_{ij}$.
      *Notes:* already in notes; proof checked.
- [x] Polynomial kernel exponent $q$; **error fix** RBF caption $e^{-0.1\|\vec x-\vec x'\|^2}$.
      *Notes:* already in notes. Also: Laplacian RBF now divides by $\sigma$ (not $\sigma^2$); Gaussian RBF notes $\gamma=1/\sigma^2$ as in SVM II; empty RBF heading completed.
- [x] Mercer: $\lambda_i$ are eigenvalues (not SVM multipliers); soft margin: "$C$: slack weight, denoted $\mu$ in Ch. 12/14".
      *Notes:* added both remarks (Mercer $\lambda_i$ = eigenvalues of the integral operator; $C$ = slack weight $\mu$).
- [x] Kernel PCA: coefficients $\alpha_{i,k}\to a_{i,n}$, $\vec\alpha_i\to\vec a_i$, index $k\to n$.
      *Notes:* already in notes ($a_{i,n}$, $\vect a_i$); eigenvectors are $\vect v_i$; normalization $\vect a_i^T\mat K\vect a_i=m\lambda_i\|\vect a_i\|^2=1$ made explicit. Derivation $\mat K^2\vect a_i=m\lambda_i\mat K\vect a_i$ checked.
- [x] DTW: sequences $X,X'$, index $t$, $k(X,X')=e^{-D(X,X')}$ "(not positive semidefinite in general)".
      *Notes:* already in notes; sequence brackets $\langle\cdot\rangle\to(\cdot)$ (clash with inner product).
- [x] $\mathcal L$: $l$ samples with true labels $y_i\in\{-1,+1\}$; $\mathcal U$: $u$ unlabeled; $m=l+u$.
      *Notes:* already in notes.
- [x] Edge weights $w_{ij}\ge0$ defined (e.g. heat kernel $e^{-\|\vec x_i-\vec x_j\|^2/(4t)}$).
      *Notes:* already in notes.
- [x] "Decision function $f(\vec x)$, predicted label $\hat y=\mathrm{sign}(f(\vec x))$".
      *Notes:* already in notes.
- [x] $\mathcal H_k$ = RKHS of kernel $k$; $\mathcal M$ = data manifold.
      *Notes:* already in notes.
- [x] Bold $\vec\beta_j\to\beta_j$; $\lambda_i,\nu_i$ defined on the Lagrange slide.
      *Notes:* added the primal problem (from representer theorem + hinge loss) and defined $\lambda_i,\nu_i\ge0$ at the Lagrangian.
- [x] **Error fixes**: $\sum_j\beta_j k(\vec x_i,\vec x_j)$ (was $\beta_i$, 2×); $\partial L/\partial\vec\beta$; $(2\gamma_A\mat I+2\gamma_I\mat L\mat K)^{-1}$ (was $\mat K\mat L$, 2×).
      *Notes:* remaining $\beta_i\to\beta_j$ in the simplified Lagrangian fixed; $\partial L/\partial\vect\beta$ and $(2\gamma_A\mat I+2\gamma_I\mat L\mat K)^{-1}$ already correct. Dual $\mat Q$ re-derived: $\mat K\mat M^{-1}=\mat M^{-T}\mat K$, so $\mat Q$ is correct; box $0\le\lambda_i\le1$ matches the objective $\sum_i\xi_i$.
- [x] Hidden variable **$y\to z$** throughout the general EM part ($p(x,z;\theta)$, $p(z|x;\theta)$, $\int dz$, Q, H); iteration index $(i)\to(j)$ with a note ("$i$ indexes samples").
      *Notes:* already in notes.
- [x] Parameter estimation: "$x$ a realization (observed value) of $X$"; MAP denominator $\int p(\theta')p(x|\theta')d\theta'$.
      *Notes:* already in notes.
- [x] ML example: `\vec{x_i}`→`\vec x_i`; zero matrix `\mat 0`.
      *Notes:* already in notes.
- [x] GMM: $\theta=\{p_k,\vec\mu_k,\mat\Sigma_k\}$, hidden $z_i\in\{1..K\}$; $p_{ik}=p(z_i=k|\vec x_i;\hat\theta)$ "responsibility"; $p(\vec x;\theta)$ is a density; $L(\theta)=\sum_i\log p(\vec x_i;\theta)$; $\mathcal N(\cdot;\cdot,\cdot)$; M-step = fixed-point equations solved iteratively; figures `gmm1/2.pstex_t` legend $\sum_k p_k\mathcal N(x;\mu_k,\sigma_k^2)$.
      *Notes:* already in notes (with $\pi_k$, $\gamma_{ik}$ per the review); hats added in the responsibility numerator; "classification by unsupervised learning" → unsupervised learning (clustering, density estimation). M-step derivations checked.
- [x] **Error fix** GMM struktogramm: E-step uses $(j)$, M-step computes $\vec\mu_k^{(j+1)},\mat\Sigma_k^{(j+1)},p_k^{(j+1)}$.
      *Notes:* already in notes.
- [x] Q: "expected complete-data log-likelihood (historically Kullback–Leibler statistics)"; $H$ is a cross-entropy; $E_{z\sim p(z|x;\theta)}[\log p(x,z;\theta')]$; KL proof uses $\log u\le u-1$, "$p,q$ arbitrary densities"; footnote "for discrete $z$ the integral becomes a sum".
      *Notes:* done: $Q$ named expected complete-data log-likelihood (historically KL statistics), $H$ cross-entropy; wrong student note ("measures pdf similarity") replaced; KL proof with $\log u\le u-1$ for arbitrary densities. Added the two-line proof that EM never decreases the log-likelihood.
- [x] **New frame** *EM for Gaussian Mixture Models*: observed $\vec x_1..\vec x_m$, hidden $z_i$, parameters, complete-data likelihood, E-step $Q$, M-step.
      *Notes:* covered by the GMM section of the notes.
- [x] Constrained optimization: Lagrangian $\Lambda(p_1..p_K,\nu)$; "stationarity condition".
      *Notes:* notes use $\mathcal L$ (reviewer: $\mathcal L$ for Lagrangians), also in the GMM weight derivation; "The Lagrange multiplier is $a_k=\dots$" → $\nu$ is the multiplier.
- [x] **Rewritten** prior-estimation example: samples $x_n$, $n=1..m$, hidden $z_n$, known $p(x|k)$, $a_{nk}=p(z_n=k|x_n;\hat\theta^{(j)})$, update $\hat p_k^{(j+1)}=\frac1m\sum_n a_{nk}$; undefined bias field $\beta$ removed.
      *Notes:* already in notes; initialization note generalized.
- [x] **New frame** *Notation in this Chapter*: voxels $0..n-1$, $\tilde X_i$/$X_i$/$Y_i$ (log intensity, not a label), $\vec\beta$ random with prior, hidden $z_i$, known $\mu_k,\psi_k,p_k$, $W_{ik}$, MAP-EM.
      *Notes:* already in notes.
- [x] Hidden class $\Gamma\to z_i$ / $k$ everywhere; $W_{i\Gamma}\to W_{ik}$; $p_k=p(z_i=k)$.
      *Notes:* remaining $\Gamma$ in the gradient fixed ($\sum_k\pi_k\dots$).
- [x] "conditionally independent given $\vec\beta$"; "density (likelihood) of the observations"; pixel → voxel.
      *Notes:* already in notes; remaining "pixel" → voxel (2×).
- [x] Gradient: typo $\psi_j^{-1}$ fixed; summation index $l$ in denominator; voxel sum index $i'$; $\bar{\vec R}=(\bar R_0..\bar R_{n-1})^T$, $\mat D=\mathrm{diag}(\bar\psi_i^{-1})$, $\mat H=[\mat D+\mat\Psi_\beta^{-1}]^{-1}$.
      *Notes:* already in notes; bias-field gradient and update $\hat{\vect\beta}=\mat H\bar{\vect R}$ re-derived: correct. Empty "Result using an extended model:" completed.
- [x] **New frame** *Notation in this Chapter*: $\vec x$ random vector of $n$ sensors ($x_i$ = component, not sample), $\vec s=(s_1..s_m)^T$ sources ($m$ sources, later $m=n$), $\mat A,\mat W$, realizations $\vec x(1..T)$, $E\{\cdot\}$ ≈ sample average, $\tilde{\vec x}$, $\hat{\vec s}$, $y=\vec w^T\vec x$ projection (not a label).
      *Notes:* already in notes.
- [x] "from now on $m=n$ (square $\mat A$)"; "observed realizations $\vec x(1),\dots,\vec x(T)$".
      *Notes:* added "from now on $m=n$" at the square-$\mat A$ assumption; realizations already in the notation list.
- [x] Decorrelation: $E\{\vec x\}=\vec 0$; $\hat{\vec s}=\tilde{\vec x}$; rotated $\hat{\vec x}\to\vec x'$; whitening note "unit-variance sources $E\{\vec s\vec s^T\}=\mat I$ assumed".
      *Notes:* already in notes; duplicated whitening formula removed; reference to the (non-existent) "Discriminant Analysis I" fixed. Whitening and $\mat R$-rotation derivations checked.
- [x] "is **typically** more Gaussian"; entropy $H(x)=-\int p\log p$; Lagrangian functional $J\to\mathcal L(p)$ (J = negentropy); moments $k$-th.
      *Notes:* already in notes; moment written $n$-th (formula uses $n$). Max-entropy proof checked ($\lambda_0,\lambda_1,\lambda_2$ give the Gaussian).
- [x] Algorithm: $\vec w_i^T\tilde{\vec x}$; $\mat W=(\vec w_1,\dots,\vec w_n)^T$; output $\hat{\vec s}=\mat W\tilde{\vec x}$ "(up to scale, sign and order)"; kurtosis of $\vec w^T\tilde{\vec x}$; MI $\vec y=(y_1..y_n)^T$.
      *Notes:* already in notes; added "(up to scale, sign and order)"; kurtosis maximization now on whitened $\tilde{\vect x}$; sub-/supergaussian examples now carry their kurtosis sign.
- [x] **New frame** *Notation in this Chapter*: $\mathcal D$ training set of size $n$ (elsewhere $S,m$), $y=F(\vec x)$ true label, $h$ hypothesis, $\hat y=h(\vec x)$, $g(\vec x;\mathcal D)$, $E_{\mathcal D}$, $\theta,\phi_n$, $m$ = NFL iterations / CV folds.
      *Notes:* notes use $y=f^*(\vect x)$ for the target (not $F$, which is the log-odds in Ch. 3); body text now uses $f^*$ consistently (11 places), classification target $f^*(\vect x)=p(y=+1\mid\vect x)$.
- [x] Off-training-set error: $y_i\in\{-1,+1\}$, define $e$, $h$, $\hat y=h(\vec x)$, $p_k(\cdot|\mathcal D)$, Kronecker $\delta$.
      *Notes:* already in notes ($F\to f^*$).
- [x] "precision **or** specificity".
      *Notes:* already in notes.
- [x] Regression bias: $(E_{\mathcal D}\{g(\vec x;\mathcal D)\}-F(\vec x))^2$; $\vec x$ fixed, expectation over training sets.
      *Notes:* already in notes; add-and-subtract derivation checked.
- [x] Classification: $p(y=+1)=p(y=-1)=\frac12$; $y_B\to\hat y^*(\vec x)$; trained decision $\hat y(\vec x;\mathcal D)=+1$ if $g\ge\frac12$ else $-1$; $p(\hat y(\vec x;\mathcal D)\ne\hat y^*(\vec x))$ (3×); "density of $g$ over random training sets (fixed $\vec x$)"; $\mathrm{Var}_{\mathcal D}[g]$; $\Phi(t)$ = upper tail of the standard normal.
      *Notes:* already in notes; Gaussian boundary-error formula checked for both cases.
- [x] **Error fix** case split: second case "if $F(\vec x)\ge0.5$".
      *Notes:* already in notes.
- [x] Jackknife: "sample estimates" (not ML/CLT); **error fix** new bullet "jackknife estimate $\mu_{PS}$ approx. normal with variance $\sigma^2_{PS}/n$"; bias label $\mathrm{bias}_{\text{jack},i}$, $\mathrm{bias}_{\text{jack}}=\frac1n\sum_i$.
      *Notes:* already in notes; both jackknife examples (mean, variance) checked.
- [x] Bootstrap: $\hat\theta^{(b)}=\phi_n(X^{(b)})$, $b=1..B$; tends to "the ideal bootstrap estimate ($B\to\infty$)".
      *Notes:* done: $\hat\theta^{(b)}=\phi_n(X^{(b)})$, sums over $b$; "does not change the prior" rewritten.
- [x] Cross-validation: "$m$ = number of folds"; note validation vs. test set ("if the held-out fold is used to stop training or select parameters, it acts as a validation set; final error on separate test data").
      *Notes:* already in notes; dangling colon fixed.
- [x] **New frame** *Notation in this Chapter*: $\mathcal D$ with $N$ samples (elsewhere $S,m$), $i$ sample index, $m=1..M$ boosting iteration, $y_i\in\{-1,+1\}$, $G_m\in\{-1,+1\}$, $f_M=\sum\beta_mG_m$, $\hat y=G(\vec x)=\mathrm{sign}(f_M(\vec x))$, $w_i^{(m)}$, $I(\cdot)$.
      *Notes:* already in notes; added $f_0\equiv0$ and $\alpha_m=2\beta_m$.
- [x] Boosting: generic classifier $G(\vec x)\in\{-1,+1\}$; final $\hat y=G(\vec x)=\mathrm{sign}(\sum\alpha_mG_m)$.
      *Notes:* already in notes.
- [x] **Error fixes** algorithm box: `w_i =\gets 1/N` → `w_i \gets 1/N`; loop `\until{m = M}` → `\until{m > M}` (all $M$ rounds); "using weights $w_1..w_N$"; $G_m(\vec x_i)$ bold; output $\hat y$.
      *Notes:* already in notes.
- [x] Exponential loss: $\{\beta_m,\vec\gamma_m\}_{m=1}^M$; argmin over the weak-classifier family; $f_0\equiv0$ ($w_i^{(1)}=1$); weight scaling irrelevant; $\alpha_m=2\beta_m$ so $\hat y=\mathrm{sign}(f_M)$; $\{-1,+1\}$.
      *Notes:* already in notes; added the missing step solving for $\beta_m=\frac12\log\frac{1-\mathsf{err}_m}{\mathsf{err}_m}$ and $w_i^{(1)}=1$. Weight update identity checked.
- [x] Face detection: integral image $ii(u,v)=\sum_{u'\le u,v'\le v}i(u',v')$ (figure `integral_image.pstex_t` $(x,y)\to(u,v)$); feature $\phi_j(\vec x)$, $j$ feature index; note Viola–Jones uses $G_j\in\{0,1\}$ (face iff $\sum\alpha_mG_m\ge\frac12\sum\alpha_m$); TPR and FPR defined.
      *Notes:* done: $II(u,v)=\sum I(u',v')$ (pixel coordinates no longer clash with the window $\vect x$), feature $\phi_j(\vect x)$, note on the Viola–Jones $\{0,1\}$ variant, TPR/FPR named; "3 basis operations" → four look-ups.

## Additional fixes found during the notes pass (not in the list above)

- [x] Ch. 1 postulates: heading says 6 postulates but only 5 were listed (constituents and structure were merged); split into two bullets as in Niemann.
- [x] Ch. 3 intro: logistic regression was described as a regression method; now: a classification method that models $p(y\mid\vect x)$ by a sigmoid, fitted by maximum likelihood.
- [x] Ch. 3 Newton–Raphson note: "finding the max values that satisfy a function" → applied to the gradient it finds a stationary point, which is the maximum because the log-likelihood is concave. Taylor step $f'(x_0+h)=\dots$ → $\approx$.
- [x] Ch. 3 gradient: duplicated sentence "where $x_{i,j}$ is …" removed.
- [x] Ch. 3 lifting figures: caption coefficients $w_i\to\alpha_i$; 2-D caption "the plane $z=r^2$" with $z=x_1^2+x_2^2$ and $r$ defined.
- [x] Build: undefined `\Nu` (rank-reduced LDA) → $\mat N$; math in section titles wrapped in `\texorpdfstring`; `\choose`-stacked vectors → `pmatrix`; empty `\textbf{}`. Build has 0 errors and 0 warnings (with biber).
- [x] Ch. 5 title "Discriminative Analysis" → "Discriminant Analysis"; odd Gaussian example ("availability of apples") replaced; rank-reduced LDA intro "N dim" → $d$-dimensional; "computationally prohibited" → "prohibitive"; prototypes sentence fixed.
- [x] Ch. 6 Norms: "sparcity" typo; unit-ball note rewritten (shape of the ball explains why $L_1$ favours sparse solutions); "residual zero" holds for the optimal solution.
- [x] Ch. 7 Perceptron convergence proof: misclassification condition now uses $(\alpha_0^{(k-1)},\vect\alpha^{(k-1)})$ (the parameters before the $k$-th update), zero initialization stated (needed for both inductions), $\|(y_i,y_i\vect x_i^T)\|^2\le1+R^2$ made explicit, theorem states "at most $k$ updates" for separable data with margin $\rho$, $\|\vect\alpha^*\|_2$. Decision function $F\to f$ (log-odds clash). Student note: the theorem gives an upper bound, not the exact number.
- [x] Ch. 11 KKT: conditions stated at the optimal points $(\vect x^*,\vect\lambda^*,\vect\nu^*)$ with $\nabla_{\vect x}\mathcal L$ (stars and gradient variable were undefined); typos "minumum", "vetor", "intialize", "and and", "Langrange".
- [x] Ch. 13–16: missing-space typesetting ("Anyscalar", "thesign", "haveunit", "apermutation", "thestatistical", "theentire", "thereduction", "thealignment", "thebias-variance", "byminimizing", "themargin", "byViola", …): space before `\textbf` restored (28 places); "colums" → "columns".
- [x] Ch. 17 No-Free-Lunch: statement rewritten ($f$ cost function, $A$ search algorithm, $c_m$ cost values of the first $m$ visited points).
- [x] Ch. 4 Naive Bayes: tied diagonal $q_{j,j}=q$ (component index $j$); "$x1 and x2$" → $x_1$ and $x_2$; "mutual independency" → conditional independence given the class.
- [x] Layout: long footnote URLs break (`xurl`); ridge likelihood split over two lines; quadratic log-ratio block set in `\small` (no visible overflow left).

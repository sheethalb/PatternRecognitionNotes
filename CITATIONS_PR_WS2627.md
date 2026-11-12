# Pattern Recognition slides — citations to add (WS 2026/27)

For an editing agent. Three parts:
1. **Bibliography** — every textbook and paper cited anywhere in the slides (deduplicated), with BibTeX keys.
2. **Where to cite** — per chapter: which slides/derivations follow which source. Section numbers marked *(verify)* should be checked against the book before printing.
3. **Problems in the existing references** — typos and inconsistencies to fix while adding citations.

Suggested style: a short source line at the bottom of the slide, e.g. `{\tiny Source: Hastie et al. [ESL], Sec. 4.4}` — or `\cite{...}` with a bibliography at the end of each chapter, replacing the "Further Readings" frame.

---

## 1. Bibliography

### Textbooks

| Key | Reference | Used in chapters |
|---|---|---|
| `duda2001` | R. O. Duda, P. E. Hart, D. G. Stork: *Pattern Classification*, 2nd ed., Wiley, New York, 2001. | 01, 02, 20 |
| `hastie2009` | T. Hastie, R. Tibshirani, J. Friedman: *The Elements of Statistical Learning — Data Mining, Inference, and Prediction*, 2nd ed., Springer, New York, 2009. | 01, 03, 04, 06, 07, 09, 19, 20, 21 |
| `bishop2006` | C. M. Bishop: *Pattern Recognition and Machine Learning*, Springer, New York, 2006. | 01, 05, 14 |
| `niemann1983` | H. Niemann: *Klassifikation von Mustern*, Springer, Berlin, 1983 (2nd revised ed. 2003, online). | 01, 02 |
| `niemann1982` | H. Niemann: *Pattern Analysis*, Springer Series in Information Sciences 4, Springer, Berlin, 1982. | 02 |
| `hosmer2000` | D. W. Hosmer, S. Lemeshow: *Applied Logistic Regression*, 2nd ed., Wiley, Hoboken, 2000. | 03, 04 |
| `ripley1996` | B. D. Ripley: *Pattern Recognition and Neural Networks*, Cambridge University Press, 1996. | 05, 09 |
| `trefethen1997` | L. N. Trefethen, D. Bau III: *Numerical Linear Algebra*, SIAM, Philadelphia, 1997. | 06, 07, 08 |
| `golub1996` | G. H. Golub, C. F. Van Loan: *Matrix Computations*, 3rd ed., Johns Hopkins University Press, Baltimore, 1996. | 08 |
| `boyd2004` | S. Boyd, L. Vandenberghe: *Convex Optimization*, Cambridge University Press, 2004. | 08, 11, 12, 13, 14 |
| `nocedal1999` | J. Nocedal, S. J. Wright: *Numerical Optimization*, Springer, New York, 1999 (2nd ed. 2006). | 11, 13 |
| `schoelkopf2002` | B. Schölkopf, A. J. Smola: *Learning with Kernels*, MIT Press, Cambridge, MA, 2002 (slides say 2003). | 12, 14, 15 |
| `vapnik2000` | V. N. Vapnik: *The Nature of Statistical Learning Theory*, 2nd ed., Springer, 2000. | 12, 14, 15 |
| `shawetaylor2004` | J. Shawe-Taylor, N. Cristianini: *Kernel Methods for Pattern Analysis*, Cambridge University Press, 2004. | 15 |
| `press2007` | W. H. Press, S. A. Teukolsky, W. T. Vetterling, B. P. Flannery: *Numerical Recipes*, 3rd ed., Cambridge University Press, 2007. | 17 |
| `cover2006` | T. M. Cover, J. A. Thomas: *Elements of Information Theory*, 2nd ed., Wiley, 2006. | 19 |
| `marsland2009` | S. Marsland: *Machine Learning: An Algorithmic Perspective*, CRC Press, 2009 (Ch. 10). | 16 (figure credit) |
| `schmidt1998` | R. F. Schmidt (Hrsg.): *Neuro- und Sinnesphysiologie*, 3rd ed., Springer, Berlin, 1998. | 10 |
| `schmidt2010` | R. F. Schmidt, F. Lang, M. Heckmann (Hrsg.): *Physiologie des Menschen mit Pathophysiologie*, 31st ed., Springer, Berlin, 2010. | 10 |
| `petersen` | K. B. Petersen, M. S. Pedersen: *The Matrix Cookbook* (online, matrixcookbook.com). | 06, 07 |

### Papers and other sources

| Key | Reference | Used in |
|---|---|---|
| `fisher1936` | R. A. Fisher: The use of multiple measurements in taxonomic problems, *Annals of Eugenics* 7(2):179–188, 1936. | 01 (Iris figure), 07 (Fisher LDA) |
| `dempster1977` | A. P. Dempster, N. M. Laird, D. B. Rubin: Maximum likelihood from incomplete data via the EM algorithm, *J. Royal Statistical Society B* 39(1):1–38, 1977. | 17 |
| `myung2003` | I. J. Myung: Tutorial on maximum likelihood estimation, *J. Mathematical Psychology* 47(1):90–100, 2003. | 17 |
| `wells1996` | W. M. Wells, W. E. L. Grimson, R. Kikinis, F. A. Jolesz: Adaptive segmentation of MRI data, *IEEE Trans. Medical Imaging* 15(4):429–442, 1996. | 17 (figures), 18 |
| `jaeger2009` | F. Jäger, J. Hornegger: Nonrigid registration of joint histograms for intensity standardization in MRI, *IEEE TMI* 28(1):137–150, 2009. | 18 |
| `pohl2005` | K. M. Pohl et al.: A unifying approach to registration, segmentation, and intensity correction, *Proc. MICCAI*, pp. 310–318, 2005. | 18 |
| `pohl2007` | K. M. Pohl et al.: Using the logarithm of odds to define a vector space on probabilistic atlases, *Medical Image Analysis* 11(6):465–477, 2007. | 18 |
| `hyvarinen2000` | A. Hyvärinen, E. Oja: Independent component analysis: algorithms and applications, *Neural Networks* 13(4–5):411–430, 2000. | 19 |
| `isomura2016` | T. Isomura, T. Toyoizumi: A local learning rule for independent component analysis, *Scientific Reports* 6:28073, 2016. | 19 (figure) |
| `vigario1998` | R. Vigário, V. Jousmäki, M. Hämäläinen, R. Hari, E. Oja: ICA for identification of artifacts in magnetoencephalographic recordings, *NIPS 10*, 1998 *(verify year)*. | 19 (figures) |
| `belkin2006` | M. Belkin, P. Niyogi, V. Sindhwani: Manifold regularization, *JMLR* 7:2399–2434, 2006. | 16 |
| `melacci2011` | S. Melacci, M. Belkin: Laplacian SVMs trained in the primal, *JMLR* 12:1149–1184, 2011. | 16 |
| `freund1997` | Y. Freund, R. E. Schapire: A decision-theoretic generalization of on-line learning and an application to boosting, *J. Computer and System Sciences* 55(1):119–139, 1997. | 21 |
| `viola2004` | P. Viola, M. J. Jones: Robust real-time face detection, *IJCV* 57(2):137–154, 2004. | 21 |
| `viola2001` | P. Viola, M. Jones: Rapid object detection using a boosted cascade of simple features, *Proc. CVPR*, 2001. | 21 (figure) |
| `hacker2006` | C. Hacker, A. Batliner, E. Nöth: Are you looking at me, are you talking with me — multimodal classification of the focus of attention, *Proc. TSD*, 2006 *(verify venue)*. | 21 (figures) |
| `matas` | J. Matas, J. Šochman: *AdaBoost* (lecture slides), Center for Machine Perception, CTU Prague. | 21 |
| `sawyer2005` | S. Sawyer: *Resampling Data: Using a Statistical Jackknife*, Washington University, 2005 (lecture notes). | 20 |
| `eskofier2008` | B. Eskofier, F. Hönig, P. Kühner: Classification of perceived running fatigue in digital sports, *Proc. ICPR*, Tampa, 2008. | 07 |
| `spiegel2009` | M. Spiegel, D. Hahn, V. Daum, J. Wasza, J. Hornegger: Segmentation of kidneys using a new active shape model generation technique based on non-rigid image registration, *Comput. Med. Imaging Graph.* 33(1):29–39, 2009. | 07 (figures) |

Image credits already on slides (keep as is): Wikimedia Commons — LadyofHats (01, flower diagram), Pbroks13 CC BY 3.0 (03, conic sections), Martin Waldseemüller (16, map).

---

## 2. Where to add citations

Format: *frame title / topic* → source. Add one source line per slide or block of slides that follows the source.

**01 Introduction**
- *Postulates for Pattern Recognition*, pattern/class definitions (ω, Ω_κ, ⁱf(x)) → `niemann1983`.
- Iris example / figure → `fisher1936` (already credited in figure; add full reference).
- *Performance Evaluation* (confusion matrix, recall/precision, ROC) → `duda2001` Ch. 2 or `hastie2009` Sec. 9.2.5 *(verify)*; or a standard ROC reference (Fawcett 2006, *Pattern Recognition Letters* 27(8):861–874 — not currently in the slides).
- *Literature* frame lists Duda/Hastie/Bishop → keep, fix typos (Part 3).

**02 Bayes Classifier**
- *Classification of Simple Patterns* (pipeline) → `niemann1983`.
- *Bayesian Classifier*, Bayes rule, decision rule → `duda2001` Ch. 2.
- *Optimality of the Bayesian Classifier* (loss, expected loss, 0/1 loss) → `duda2001` Sec. 2.2–2.3 *(verify)*; `bishop2006` Sec. 1.5.
- Generative vs. discriminative → `bishop2006` Sec. 1.5.4.

**03 Logistic Regression I**
- Posterior as logistic function, log-odds, decision boundary → `hastie2009` Sec. 4.4; `bishop2006` Sec. 4.2.
- Gaussian class conditionals → quadratic/linear boundary → `hastie2009` Sec. 4.3; `bishop2006` Sec. 4.2.1.
- Exponential family + lemma (linear boundary) → `bishop2006` Sec. 2.4 and 4.2.4.

**04 Logistic Regression II**
- Log-likelihood, gradient, Hessian, Newton–Raphson → `hastie2009` Sec. 4.4.1; `bishop2006` Sec. 4.3.2–4.3.3 (IRLS).
- Lifting / parameterization → `hosmer2000` (model building).

**05 Naive Bayes**
- Naive Bayes assumption, Gaussian example → `hastie2009` Sec. 6.6.3; `bishop2006` Sec. 4.2.3 *(verify)*.
- First-order dependency / tridiagonal precision → Gaussian Markov chain, e.g. `bishop2006` Sec. 8.1–8.2 (graphical models) *(verify)*.

**06 Discriminant Analysis**
- Gaussian classifier, shared covariance, LDA → `hastie2009` Sec. 4.3.
- Feature transform via SVD/eigendecomposition → `trefethen1997` (SVD lectures); `golub1996`.

**07 Discriminant Analysis II**
- Rank-reduced LDA → `hastie2009` Sec. 4.3.3.
- Fisher transform / Fisher's criterion → `fisher1936`; `bishop2006` Sec. 4.1.4.
- PCA → `bishop2006` Sec. 12.1; `hastie2009` Sec. 14.5.1.
- adidas_1 shoe example → `eskofier2008`; kidney shape model → `spiegel2009` (already in figure credits).
- Linear regression, ridge regression (incl. MAP interpretation), lasso → `hastie2009` Sec. 3.2, 3.4.1–3.4.2; `bishop2006` Sec. 3.1.4, 3.3.

**08 Norms**
- Norm definitions, unit balls → `golub1996` Sec. 2.2–2.3; `trefethen1997` Lecture 3.
- Norm-dependent regression, LS/Chebyshev/L1, penalty functions → `boyd2004` Ch. 6 (Sec. 6.1–6.3).
- Ridge/Lasso unit-ball picture → `hastie2009` Sec. 3.4.3 (Fig. 3.11).
- Compressed sensing → add a primary reference, e.g. E. J. Candès, M. B. Wakin: An introduction to compressive sampling, *IEEE Signal Processing Magazine* 25(2):21–30, 2008 (not currently in slides; the Rice/Duke URLs are outdated).

**09 Perceptron**
- Rosenblatt perceptron, update rule → `hastie2009` Sec. 4.5.1; `ripley1996`; original: F. Rosenblatt, *Psychological Review* 65(6):386–408, 1958 (not in slides).
- Convergence proof (Novikoff) → `ripley1996` or `bishop2006` Sec. 4.1.7 *(verify)*.

**10 MLP**
- Biological neuron slides → `schmidt1998`, `schmidt2010`.
- MLP, backpropagation → `bishop2006` Ch. 5 (Sec. 5.3); `hastie2009` Ch. 11.

**11 Optimization I**
- Whole chapter (descent methods, backtracking line search, steepest descent for L₁/L₂/L∞/P-norms, Newton) → `boyd2004` Ch. 9 (Sec. 9.2–9.5). Put one citation on the new "Notation in this Chapter" frame and one on each method's first slide.
- Alternative reference → `nocedal1999` Ch. 3.

**12 SVM I**
- Optimal separating hyperplane ("Vapnik 1996") → `vapnik2000`; `hastie2009` Sec. 4.5.2.
- Hard/soft margin formulation → `schoelkopf2002` Ch. 7; `bishop2006` Sec. 7.1.

**13 Optimization II**
- Whole chapter (Lagrangian, dual function, weak/strong duality, Slater, KKT) → `boyd2004` Ch. 5 (Sec. 5.1–5.5); the slide "Conclusions (Boyd 2004, Sec. 5.5.3)" already cites — use the same format everywhere.

**14 SVM II**
- Soft-margin Lagrangian, dual, complementary slackness, support vectors → `hastie2009` Sec. 12.2; `bishop2006` Sec. 7.1.1; `schoelkopf2002` Ch. 7.
- Figure "From Bishop: Pattern Recognition and Machine Learning" → give the figure number (e.g. `bishop2006`, Fig. 7.x) *(verify)*.
- Kernel functions (polynomial, RBF, sigmoid) → `schoelkopf2002` Ch. 2.

**15 Kernels**
- Kernel trick, Mercer's theorem, PSD kernels → `schoelkopf2002` Ch. 2; `shawetaylor2004` Ch. 3.
- Kernel PCA → B. Schölkopf, A. Smola, K.-R. Müller: Nonlinear component analysis as a kernel eigenvalue problem, *Neural Computation* 10(5):1299–1319, 1998 (not in slides); `schoelkopf2002` Ch. 14.
- Kernels for sequences (DTW) → add a reference (e.g. Bahlmann et al., Proc. IWFHR 2002) *(not in slides)*.
- Fisher kernels → T. Jaakkola, D. Haussler: Exploiting generative models in discriminative classifiers, *NIPS 11*, 1999 (not in slides).

**16 Laplacian SVM**
- Manifold regularization framework, LapSVM primal/dual → `belkin2006`; `melacci2011`.
- Graph Laplacian figure/algorithm → `marsland2009` (already in figure credit).

**17 EM**
- ML/MAP estimation basics → `myung2003`; `duda2001` Ch. 3.
- GMM and its EM updates → `bishop2006` Sec. 9.2; `hastie2009` Sec. 8.5.
- General EM, missing information principle, Q-function, monotonicity → `dempster1977`; `bishop2006` Sec. 9.3–9.4.
- Constrained optimization (Lagrange for priors) → `boyd2004` Ch. 5.
- MRI figures "(Courtesy of W. Wells)" → `wells1996` (the `\cite{IMG-Wells}` key has no bibliography entry — see Part 3).

**18 EM Applications**
- Bias-field model, MAP-EM derivation → `wells1996` (cite on the "Notation in this Chapter" frame and on the derivation slides).
- Intensity standardization → `jaeger2009`; extensions → `pohl2005`, `pohl2007`.

**19 ICA**
- Whole chapter (model, ambiguities, whitening, non-Gaussianity, kurtosis, negentropy, FastICA-type algorithm, mutual information) → `hyvarinen2000`.
- Entropy, maximum-entropy property of the Gaussian, mutual information → `cover2006` Ch. 2, 8, 12 *(verify)*.
- Factor analysis / latent variables → `hastie2009` Sec. 14.7.
- Figures → `isomura2016`, `vigario1998` (already credited).

**20 Model Assessment**
- No Free Lunch, off-training-set error, bias–variance (regression and classification), jackknife, bootstrap, cross-validation → `duda2001` Ch. 9 (Sec. 9.2–9.6) *(verify)*. Figures "adapted from Duda, Hart" → full reference + figure number.
- Jackknife details → `sawyer2005`.
- Bias–variance, CV, bootstrap (alternative) → `hastie2009` Ch. 7.

**21 AdaBoost**
- AdaBoost algorithm, exponential loss, forward stagewise additive modelling → `hastie2009` Sec. 10.1–10.5; original → `freund1997`.
- Face detection, Haar features, integral image, cascade → `viola2001` / `viola2004`.
- AdaBoost slides by Matas/Šochman → `matas`.
- Focus-of-attention figures → `hacker2006` (already in figure credits).

---

## 3. Problems in the existing references (fix while adding citations)

- [ ] **01 Literature + Further Readings:** "David G. **Stock**" → **Stork** (3×). Year: 2001 here, 2000 in Ch. 02/20 — use one (the 2nd edition is ©2001).
- [ ] **01 Literature:** remove the outdated book prices ("EUR 114.45" etc.); Hastie URL → https://hastie.su.domains/ElemStatLearn/ *(verify)*.
- [ ] **12:** "Vapnik 1996" — the cited book is 1995 (1st ed.) / 2000 (2nd ed.); match the bibliography entry.
- [ ] **14:** "From Bishop: Pattern Recognition and Machine Learning" — add figure number and full reference.
- [ ] **15:** Shawe-Taylor link is a Google search URL → replace with the publisher page or remove.
- [ ] **17:** `\caption[MRI enhancement \cite{IMG-Wells}]` — key `IMG-Wells` is undefined (no .bib in the project); replace with text "(Wells et al. 1996)" or add the bib entry.
- [ ] **17:** Dempster et al. entry is missing the year (1977).
- [ ] **20:** "adapted from Duda, Hart" (3×) — add Stork, year, figure number.
- [ ] **21:** text says Viola–Jones "in 2001" while Further Readings lists the 2004 IJCV paper — cite both (`viola2001`, `viola2004`).
- [ ] **08:** compressed-sensing URLs (Rice, Duke) are outdated → replace with a paper reference.
- [ ] **08/11:** Boyd URL → https://web.stanford.edu/~boyd/cvxbook/.
- [ ] Inconsistent formats across chapters ("T. Hastie" vs "Trevor Hastie", "2nd edition" vs "2nd Edition") — unify if using a bibliography style.

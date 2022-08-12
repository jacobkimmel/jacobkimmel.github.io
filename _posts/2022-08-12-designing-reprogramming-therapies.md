---
title: Designing reprogramming therapies
layout: post
date: 2022-08-12
tag:
- biology
- machine learning
- therapeutics
- newlimit
blog: true
use_math: false
---

*This is a cross-post from the [NewLimit Blog](https://blog.newlimit.com/p/developing-reprogramming-therapies)*

We all experience a decline in health with age. Many common diseases of aging — immune dysfunction, muscle atrophy, and systemic fibrosis among others — have been so recalcitrant that we consider them inevitable. 

At [NewLimit](https://newlimit.com), we’re developing medicines to treat age-related disease through a new therapeutic approach. While the tissues that make up our bodies age in different ways, we believe that therapies designed to reprogram the epigenome may unlock treatments for multiple diseases and increase the number of healthy years in each of our lives.

<aside>
🔗 See: [NewLimit — A company built to extend human healthspan](https://www.notion.so/Developing-reprogramming-therapies-949e909dc3e446ed9b344076bd67e4ae)

</aside>

How might these therapies work?

Your body is composed of a constellation of cell types that perform specialized functions, yet each of your cells contains the same DNA. The emergence of these diverse functions from a common genetic code is mediated by the epigenome, a set of modifications to DNA and associated proteins that control which genes are turned “on” and “off” in each cell.****

Genes known as transcription factors coordinate the machinery that sets and remodels these epigenetic marks. Transcription factors have evolved to control genetic programs by binding specific sites in the genome and recruiting other protein machines to make changes to the epigenome, giving rise to distinct cell types and functions. The epigenome can be broadly remodeled by manipulating just a *small number* of transcription factors, enabling us to reprogram cells to adopt different identities and perform new functions.

We believe that these developmental programs can be repurposed as a new class of medicines.

# Restoring cell function by partial reprogramming

What evidence is our belief based on? 

A series of experiments have begun to demonstrate that epigenetic reprogramming may be employed to address age-related diseases. Even old cells can be reprogrammed back to a pluripotent, embryonic state, then developed into healthy young animals by activating only four transcription factors. Researchers have found that after reprogramming, some cellular features of aging are reversed [^1]. Complete pluripotent reprogramming erases the identity and function of adult cells and is not a plausible therapy, but recent experiments suggest this biology may be harnessed by other means to address disease.

It has recently been shown that even transient activation of pluripotent reprogramming factors can reverse molecular and functional features of aging. Researchers have shown that this “partial reprogramming” process can restore healthy gene expression and cell phenotypes in old cells without permanently abolishing adult cell identity and function. Experiments in old and diseased animals have also shown that partial reprogramming can restore regenerative potential and provide therapeutic benefit in models of [metabolic disease](https://pubmed.ncbi.nlm.nih.gov/27984723/), [muscle injury](https://pubmed.ncbi.nlm.nih.gov/34035273/), [heart attacks](https://pubmed.ncbi.nlm.nih.gov/34554778/), [glaucoma](https://pubmed.ncbi.nlm.nih.gov/33268865/), [fibrosis](https://www.nature.com/articles/s43587-022-00183-2#Sec28), and [liver disease](https://www.cell.com/cell-reports/fulltext/S2211-1247(22)00491-0).

While promising, the reprogramming methods used in these experiments are not readily translatable into therapies for humans. Partial reprogramming with pluripotency factors can induce neoplastic teratomas — tumor-like growths that are often lethal. Beneficial and dangerous doses of these pluripotent reprogramming interventions are often only 2-fold different.

Is there a way we can capture the benefits of partial reprogramming, while reducing the risks? Several groups have shown that alternative epigenetic programs can likewise restore youthful phenotypes in old cells, while reducing undesirable effects. Even reprogramming strategies that completely avoid risky pluripotency factors can provide benefit [^2].

At NewLimit, we’re building a discovery platform to engineer new epigenetic programs that can similarly restore youthful regenerative potential to address age-related disease, while minimizing risks.

# How can we design reprogramming therapies?

Reprogramming interventions are traditionally designed by selecting a set of transcription factors using intuition, then testing to see if these factors can induce a small set of “markers” that correlate with a desired cell phenotype. These approaches have enabled the design of many reprogramming methods that convert between distinct cell types [^3]. Nonetheless, this traditional approach is limited by the use of coarse marker gene read-outs, the small experimental scales employed, and the heuristic nature of hypothesis generation.

NewLimit is building a technology platform that combines advances in single cell genomics, pooled perturbation screening, and machine learning to overcome these challenges. Each of these technologies has emerged only within the last decade, enabling a new approach to design reprogramming therapies.

1. **Measuring reprogramming outcomes with single cell genomics:** Nuanced changes in epigenetic state — like the difference between diseased and healthy cells of the same type — are rarely captured by a handful of marker genes.  By using single cell genomics to measure reprogramming outcomes, we’re can move beyond marker genes and use rich measurements of cell state to evaluate interventions *and* perform more experiments than was traditionally possible.
2. **Pooled reprogramming screens:** Pooled screening allows us to perform hundreds to thousands of experiments in the same population of cells, including combinations of reprogramming factors without burdensome molecular biology processes. Using these techniques, we can increase the number of reprogramming hypotheses we explore by orders of magnitude.
3. **Guiding epigenetic program design with machine learning:** Even with advances in single cell genomics and pooled screening, there are far more possible reprogramming strategies than we can ever test experimentally [^4]. Machine learning methods predict the outcomes of new experiments and allow us to search the experimental space intelligently, using data from past experiments to inform the selection of future experiments in a rigorous process.

Taking inspiration from the “Design-Build-Test-Learn” framework common to engineering disciplines, we’re focused on improving the number of reprogramming hypotheses we can test, how much we learn from each, and integrating information across historical experiments so that each experiment informs the design of those to come. 

We believe that this technology platform will transform the design of epigenetic programs from an artistic endeavor into an engineering discipline, enabling reprogramming discovery campaigns analogous to the small molecule and antibody campaigns that drive drug discovery today.

# Ambitious missions require excellent teams

The technologies that comprise our platform are necessary but not sufficient to realize our mission. The most critical component of the platform are the talented scientists and engineers who build and deploy it to discover new medicines. Our success depends upon these talented people more than any other variable.

NewLimit is now recruiting broadly across diverse fields of science, including single cell and functional genomics, immunology, computational biology, and machine learning. If this mission excites you, please reach out, even if none of our open roles are an exact fit for your talents.

**Apply now to build the future with us:** [newlimit.com/careers](https://www.newlimit.com/careers)

---

# Footnotes

[^1]: Beginning in the 1950s, John Gurdon performed a series of remarkable experiments where he transplanted the nuclei of mature frog cells into enucleated frog eggs ([Gurdon 1970](https://royalsocietypublishing.org/doi/epdf/10.1098/rspb.1970.0050)). The egg cytoplasm contained signals that were sufficient to reprogram the adult nucleus back to an embryonic state, and these reprogrammed eggs gave rise to young frogs. Shinya Yamanaka’s group later showed this process could be achieved by activating just four genes in 2006 ([Takahashi & Yamanaka, 2006](https://pubmed.ncbi.nlm.nih.gov/16904174/)). Gurdon and Yamanaka were jointly awarded the Nobel Prize for pluripotent reprogramming in 2007. Several researchers later found that somatic cells of different ages became highly similar after reprogramming back to a pluripotent state using Yamanaka’s method ([Lapasset et. al. 2011](https://pubmed.ncbi.nlm.nih.gov/22056670/), [Mertens et. al. 2015](https://pubmed.ncbi.nlm.nih.gov/26456686/)).
[^2]: Researchers have found that smaller, less risky sets of pluripotency factors ([Lu et. al. 2020](https://pubmed.ncbi.nlm.nih.gov/33268865/), [Neumann et. al. 2021](https://www.nature.com/articles/s43587-021-00109-4), [Roux et. al. 2022](https://www.cell.com/cell-systems/fulltext/S2405-4712(22)00223-X?_returnURL=https%3A%2F%2Flinkinghub.elsevier.com%2Fretrieve%2Fpii%2FS240547122200223X%3Fshowall%3Dtrue)) and alternative partial reprogramming factors can also provide benefit ([Ribeiro et. al. 2022](https://www.nature.com/articles/s43587-022-00209-9), [Roux et. al. 2022](https://www.cell.com/cell-systems/fulltext/S2405-4712(22)00223-X?_returnURL=https%3A%2F%2Flinkinghub.elsevier.com%2Fretrieve%2Fpii%2FS240547122200223X%3Fshowall%3Dtrue)).
[^3]: Hal Weintraub’s laboratory first discovered that epigenetic reprogramming could convert skin [fibroblasts into muscle cells all the way back in 1987](https://pubmed.ncbi.nlm.nih.gov/3690668/). Researchers have since found routes to convert fibroblasts into [cardiomyocytes](https://pubmed.ncbi.nlm.nih.gov/22522929/), [immune dendritic cells](https://pubmed.ncbi.nlm.nih.gov/30530727/), [hepatocytes](https://pubmed.ncbi.nlm.nih.gov/21562492/), [renal tubule cells](https://www.notion.so/f7ae9568b319416eb8fb9b05126e8bbb),  [neurons](https://www.notion.so/3e0dcc80ccfb46d2a8f06a9665659cae), and many other cell types.
[^4]: Even with a small set of 50 possible reprogramming factors, there are >10,000,000 possible combinations of six or fewer factors to test! 
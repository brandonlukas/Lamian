# Lamian (Forked by @brandonlukas)

This is a **fork** of the [original Lamian package](https://github.com/Winnie09/Lamian) for pseudotime uncertainty quantification and trajectory inference in single-cell transcriptomic data.

## ✨ Key Update in This Fork

The `infer_tree_structure()` function has been **extended to allow users to supply their own clustering labels**, instead of being restricted to k-means clustering.

### 🔧 Why this matters

The original function required k-means clustering on PCA-reduced dimensions. However, many single-cell workflows already use robust clustering algorithms like:
- Seurat’s Louvain/Leiden clustering
- Scanpy’s community detection methods
- Hierarchical or graph-based clustering

This fork gives you full flexibility to use **precomputed cluster assignments**.

---

## 🆕 New Function Signature

```r
infer_tree_structure(
  pca,
  cellanno,
  expression,
  origin.marker = NA,
  origin.celltype = NA,
  number.cluster = NA,
  plotdir = NA,
  xlab = 'PC1',
  ylab = 'PC2',
  max.clunum = 50,
  kmeans.seed = 12345,
  clusters = NULL  # <-- new argument
)
```

### `clusters` (default = `NULL`)

•	If `NULL`, the function falls back to k-means clustering (as in the original Lamian).

•	If a named vector of cluster labels is provided, the function uses these labels directly.

•	The names of the vector must match the rownames of the pca matrix.

## 🧪 Example Usage

### Your PCA-reduced matrix and expression matrix
```r
res <- infer_tree_structure(
  pca = my_pca,
  cellanno = my_cellanno,
  expression = my_expression,
  clusters = my_cluster_labels,  # user-supplied clusters
  origin.marker = c('CD34'),
  plotdir = 'plots/',
  xlab = 'PC1',
  ylab = 'PC2'
)
```

## 🔄 Compatibility

This fork retains full backward compatibility with the original Lamian interface. If clusters is not supplied, k-means clustering will be performed as before.

## 📦 Installation

You can install this forked version using:

### If using devtools
`devtools::install_github("brandonlukas/Lamian")`


# Privacy-Preserving-Methods-for-Outsourced-Computation
Under the assumption of untrusted cloud providers, outsourcing data intensive computation such as database services and data mining to public clouds raises privacy concerns. The primary purpose of this assignment is to understand the data privacy problem with outsourced computation in public clouds and implement several methods to mitigate this problem. This project consists of two parts.
(1) Multiplication perturbation methods for outsourced data mining; and 
(2) Crypto-index for outsourced database services.
# Part 1: Multiplication perturbation for outsourced data mining.

The idea of data perturbation is to change the original values of a dataset that is prepared for outsourced data mining, so that the untrusted cloud provider cannot figure out any original value while working on the perturbed data. The basic principle is to preserve both data privacy and data utility - the data owner can still obtain high quality data mining models with the perturbed data. In this experiment, we will be looking at one convenient method - geometric data perturbation (GDP). GDP is designed to preserve the utility for Euclidean-distance based data mining models such as kNN classifiers, linear classifiers, Support Vector Machine (SVM) classifiers (with certain kernels), and clustering with Euclidean distance as the similarity measure. In this project, we consider only classification modeling.

Let's define GDP first. The data for mining is often a table with k columns and n rows, denated as a k x n matrix. A column is also called a dimension. Let x be any record of the table, which is represented as a k-element column vector. x should be normalized. You can use the standardizaiton method xi = (xi-m)/s, where xi is the i-th dimension of the vector x, m is the mean of the i-th dimension, and s is the standard deviation of the i-th dimension. In some rare cases that a dimension contains only one identical value, you can set all values of that dimension to 0.

Let R be a secret random orthogonal k by k matrix (so that R times R's transpose is the identity matrix I). Note that R can be generated with simple methods like QR decomposition or eigendecomposition of random k by k matrices, which can be found in some Python or Java libraries. Let t be a secret random k-element column vector, which is drawn from some domain close to the normalized x, e.g., the normal distribution N(0,1). Both R and t should be shared by all records. Let d be a randomly generated k-element noise vector, individually for each record, drawn from a normal distribution N(0, σ2), where the variance σ2 is determined by the user. Let y be the perturbed vector for the original vector x. The geometric data perturbation is defined as

y=Rx+t+d

# Part 2: Crypto-index for range query processing

Database management is resource consuming. An appealing solution is to export database services to the cloud, which raises privacy concerns, too. Among the existing approaches, crypto-index is a simple solution (not so secure) that transforms a domain to a set of random IDs. It is easy to process queries on transformed data. However, the result may have low precision. In this task, you will implement a simple crypto-index method and experiment wtih single-dimensional range query on transformed data.

For simplicity, let's work on the continuous data. Assume one dimensional of the data, for example, the three datasets you have seen, is in the domain [min, max]. The crypto-index method partitions the domain into a few bins and use a random ID to represent each bin. Correspondingly, when you process a range query, say finding records with dimension i in the range [u, v], you will transform the query to the transformed data domain as "finding records with dimension i in the set of bin IDs [id1, id2,...]".

Reference: http://cecs.wright.edu/~keke.chen/cloud/labs/privacy/privacy.html

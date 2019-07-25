# Numerai_Algorithms
Releasing my own set of private tools initially used on the Numerai Dataset up to Round 168.

## Dependecies
Pandas

Numpy

Sci-kit Learn

Matplotlib

Keras

Tensorflow

## Algorithm List - Brief Description
1) Genetic MLP - Finds the most optimal structure for a MLP of a specified depth for a binary classification task. 
2) Scoring - Performs PCA (Optional) on Datasets. Evaluates the performance of a particular/predetermined model across a set number of epochs multiple times. Picks the best model based on a predefined "fitness" function, in this case validation accuracy, before applying the model to produce predictions for its test data.

## Notes on Algorithms/Notebooks
### Genetic MLP
Search for #Genes to find the list of activation functions, neuron count and layer dropout values that are considered for each "gene". A gene in this algorithm represents the values for a single layer, the algorithm initializes the genes at random if the gene_pool is empty. Changing the number of hidden_layers would affect the number of genes per NN, in turn affecting the number of layers per NN. 
The algorithm produces a set number of NNs per generation, they are then tested against a validation set whose accuracy will be used as the NNs fitness function. The top 5 NNs would be selected, the genes of each layer will be inserted into the gene pool and a new set of NNs will be created from the smaller gene pool. The process is iterative across the number_of_generation.
The mutation_factor can be adjusted to increase the likelyhood of a new gene being created rather than one being selected from the gene_pool during the model construction phase.
Graphs plotted at the end of each generation include the top 5 from the previous generation. The output dataframe, df, at the end of the whole run keeps a record of all the genes of the model and its accuracy score. This information can be used at the bottom of the script to reconstruct the "best model", manually, to train and predict on the final test set.

### Scoring
The data input for this notebook is designed to accept the broken up dataset using the dataset_split.py script, by era, that I provided in the Numerai_Dataset repository. This notebook also has the tools necessary to combine the broken up dataset produced by dataset_split.py, in this case from any era range specified by the user (if the data is split by its era), and stitch them together for training and validation. This notebook also allows for the testing of a model and its architecture by training and testing the same model with random initialisations multiple times to find the average validation accuracy of the model. This can help to determine if the model's high accuracy from a single run train/valid/test is an anomaly.
All adjustable variables can be found in main(). build_model function houses the model architecture needed for training. It accepts some variables that can allow for quick tuning from main() if needed.

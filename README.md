# Benchmarking Platform for Index Neural Nets

## Directory Structure
    .
    ├── src                    # Source Directory
    |   ├── Neural_Nets        # Neural Nets Scripts          
    │   └── Paco-Lcp           # Paco Lcp
    ├── rsc                    # Resource Directory
    │   └── uniform            # Uniform Dataset
    |── res                    # Results Directory
    |   └──uniform             # Uniform Dataset
    └── mdls                   # Models Directory   
        └──json                # Neural Nets Json 
    
## Neural Networks
### Create Datasets
In order to train Neural Nets and querying data, csv files, containing one element for each column, must be converted in hdf5 files containing their 64-bit binary rappresentation.

```
python [sourcePath]/createBinArray.py [-h] [-i INPUTFILE] [-id INPUTDIR] [-o OUTPUTPATH]


optional arguments:\n
  -h, --help            show this help message and exit  
  -i INPUTFILE, --input INPUTFILE  
                        Input file name   
                        default = 'uni01.sorted.csv'  
  -id INPUTDIR, --inputDir INPUTDIR  
                        Input file path  
                        deafult = 'rsc/uniform/'  
  -o OUTPUTPATH, --output OUTPUTPATH  
                        Output file path and file name  
                        default = 'rsc/uniform/uni01.sorted.bin.h5'  
```

### Train NN

Training is written in python using Tensorflow Keras high-level API as neural nets implementation.  
There are 3 kind of [models](mdls/json/):
1. NN0 is a Fully connected net with no hidden layers
2. NN1 is a fully connected net with 1 hidden layer composed by 256 units
3. NN2 is a fully connected net with 2 hidden layers composed by 256 units each one

To run the script use:  


```
python [sourcePath]/trainNN.py [-h] [-i INPUTFILE] [-id INPUTDIR] [-o OUTPUTPATH] [-m {1,2,3} [{1,2,3} ...]] [-p PARAMS]


optional arguments:
  -h, --help            show this help message and exit
  -i INPUTFILE, --input INPUTFILE
                        Input file name
                        default = 'uni01.sorted.bin.h5'
  -id INPUTDIR, --inputDir INPUTDIR
                        Input file path
                        default = 'rsc/uniform/'
  -o OUTPUTPATH, --output OUTPUTPATH
                        Output file path
                        default = 'res/uniform/'
  -m {1,2,3} [{1,2,3} ...], --model {1,2,3} [{1,2,3} ...]
                        Model numbers: 1 -> No hidden Layer(Perceptron); 2 ->
                        One hidden layer with 256 units; 3 -> Two hidden layer
                        with 256 units
                        default=1
  -p PARAMS, --params PARAMS
                        Params file path and file name 
                        default='mdls/params.json'
```

### Query Scripts

## Standard Data Structures
### Paco
An order-preserving minimal perfect hash function , that maps bijectively a set of ordered keys to their ordinal position position in a given list. It assumes that keys to be hashed are ordered. The [source code](src/Paco-Lcp/paco) is written in Java and it exploits the provided [libraries](src/Paco-Lcp/lib).

> Creation & Query
```
java -cp ./lib paco.PACO -f dataset.csv [-q queryFile]
```

### LCP 
A monotone minimal perfect hash function that map the keys of a lexicographically sorted set to its ordinal position. It assumes that keys to be hashed are ordered. The [source code](src/Paco-Lcp/lcp) is written in Java and it exploits the provided [libraries](src/Paco-Lcp/lib).

> Creation & Query
```
java -cp ./lib lcp.LCP -f dataset.csv [-q queryFile]
```

### B+tree
### CSS Tree
### Self Adjusting Binary Tree

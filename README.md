# CapsE: Knowledge Graph Completion and Search Personalization using Dynamic Routing between Capsules

This program provides the implementation of the dynamic routing between capsules-based model CapsE for the knowledge graph completion and the search personalization as described in the paper:

        @InProceedings{Nguyen2018,
          author={Dai Quoc Nguyen and Thanh Vu and Tu Dinh Nguyen and Dat Quoc Nguyen and Dinh Phung},
          title={{Knowledge Graph Completion and Search Personalization using Dynamic Routing between Capsules}},
          booktitle={arXiv},
          year={2018}
          }
  
Please cite the paper whenever CapsE is used to produce published results or incorporated into other software. I would highly appreciate to have your bug reports, comments and suggestions about CapsE. As a free open-source implementation, CapsE is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.

CapsE is free for non-commercial use and distributed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA) License. 

![alt text](https://github.com/daiquocnguyen/CapsE/blob/master/CapsE.png)

## Usage

### Requirements
- Python 3
- Tensorflow >= 1.6

### Training
To run the program:

        $ python CapsE.py --embedding_dim <int> --num_filters <int> --learning_rate <float> --name <dataset_name> [--useConstantInit] --model_name <name_of_saved_model>

**Required parameters:** 

`--embedding_dim`: Dimensionality of entity and relation embeddings.  

`--num_filters`: Number of filters.

`--learning_rate`: Initial learning rate.

`--name`: Dataset name (WN18RR or FB15k-237).

`--useConstantInit`: Initialize filters by [0.1, 0.1, -0.1]. Otherwise, initialize filters by a truncated normal distribution.

`--model_name`: Name of saved models.

`--num_epochs`: Number of training epochs.

`--vec_len_secondCaps`: Number of neurons within the capsule in the second layer (Default: 10).

`--run_folder`: Specify directory path to save trained models.

`--batch_size`: Batch size.

### Reproduce the CapsE results 

To reproduce the CapsE results published in the paper:      
                
        $ python CapsE.py --embedding_dim 100 --num_epochs 51 --num_filters 400 --learning_rate 0.0001 --name FB15k-237 --useConstantInit --savedEpochs 50 --model_name fb15k237
        
        $ python CapsE.py --embedding_dim 100 --num_epochs 31 --num_filters 400 --learning_rate 0.00001 --name WN18RR --savedEpochs 30 --model_name wn18rr
        
### Evaluation metrics

File `evalCapsE.py` provides ranking-based scores as evaluation metrics, including mean rank (MR), mean reciprocal rank (MRR), Hits@1 and Hits@10 in a setting protocol "Filtered".

See examples in `command.sh`. Depending on the memory resources, you should change the values of `--num_splits` to a suitable value to get a faster process. To get the results (supposing `num_splits = 8`):
        
        $ python evalCapsE.py --embedding_dim 100 --num_filters 400 --name FB15k-237 --useConstantInit --model_index 50 --model_name fb15k237 --num_splits 8 --decode
        
        $ python evalCapsE.py --embedding_dim 100 --num_filters 400 --name WN18RR --model_index 30 --model_name wn18rr --num_splits 8 --decode
         
## Acknowledgments     

I would like to thank Huadong Liao naturomics for implementing the CapsNet(Capsules Net) in Hinton's paper Dynamic Routing Between Capsules.

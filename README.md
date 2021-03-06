# SemEval-2019 Task 3 

SemEval-2019 Task 3: Contextual Emotion detection in Conversations through hierarchical LSTMs and BERT*


An overview of the proposed *HRLCE* Model:

![HRLCE](img/hred.jpg )


HRLCE is a single model that can achieve a score of 0.7666 on the final test set while only using the training dataset. 

We also finetune the *BERT-LARGE* model on this task. The results of BERT and HRLCE are combined to get the 0.7709 which ranked at 5th on the leaderboard of SemEval 2019 Task3. 

You can find the leaderboard from [CodaLab](https://competitions.codalab.org/competitions/19790#learn_the_details-data-set-format).
 
## Instructions
PyTorch1.0 with Python 3.6 serve as the backbones of this project.

The code is using one GPU by default, you have to modify the code to make it running on CPU or multiple GPUs.

The code includes more features than what has been described in the paper. For example, we experimented with multi-task learning and focal loss, but we found no significant difference.

To run the code, you have to specify the path to the *glove.840B.300d.txt* model file in *-glovepath* argument option. Other options are configured with some default value. 
In our experience, the *learning rate* and *decay* would have more impact than others.

## Performance
The results are shown in the following table:

|        | Macro-F1 |   Happy  |   Angry  |    Sad   | Harm. Mean  |
| ------ | :------: | :------: | :------: | :------: | :---------: |
| *SL*   |   Dev  <br/>  Test  |  0.6430  <br/>  0.6400  |  0.7530 <br/>  0.7190 |  0.7180  <br/> 0.7300  |  0.7016  <br/> 0.6939    |
| *SLD*   |   Dev  <br/>  Test  |  0.6470  <br/>  0.6350  |  0.7610 <br/>  0.7180 |  0.7360  <br/> 0.7360  |  0.7112  <br/> 0.6934    |
| *HRLCE*   |   Dev  <br/>  Test  |  0.7460  <br/>  0.7220  |  0.7590 <br/>  0.7660 |  0.8100  <br/> 0.8180  |  **0.7706**  <br/> **0.7666**    |
| *BERT*   |   Dev  <br/>  Test  |  0.7138  <br/>  0.7151  |  0.7736 <br/>  0.7654 |  0.8106  <br/> 0.8157  |  0.7638  <br/> 0.7631    |


Compared to HRLCE, we notice that BERT performs better on *Angry* but worse on *Happy*, therefore it makes sense to combine the results of these two. 

Another note, in order to get your submissions measured the same way as that from CodaLab, you will need to look at the harmonic mean of the three macro F1 scores of the three emotion categories. 
It is slightly different than using the micro F scores of the three emotion categories directly. 


## Related Work
A related work using RCNN can be found [here](https://github.com/zhongpeixiang/SemEval2019-Task3-EmotionDetection).

## Acknowledgement
This code is relying on the work of the following projects:

* [AllenNlp](https://github.com/allenai/allennlp)

* [torchMoji](https://github.com/huggingface/torchMoji)

* [pytorch-pretrained-BERT](https://github.com/huggingface/pytorch-pretrained-BERT)

* [ekphrasis](https://github.com/cbaziotis/ekphrasis)

Many thanks to my supervisor [Osmar R. Zaïane](http://webdocs.cs.ualberta.ca/~zaiane/) for supporting me working on this shared task. 



## following the below process
### dependencies installation
```
pip install --ignore-installed allennlp

rm -rf /home/ubuntu/anaconda3/envs/pytorch_p36/lib/python3.6/site-packages/numpy
pip install numpy
pip install emoji
pip install text_unidecode
pip install ekphrasis
```

### to get glove.840B.300d.txt
```
wget "http://nlp.stanford.edu/data/glove.840B.300d.zip"
unzip glove.840B.300d.zip
```
### to get pytorch_model.bin
```
wget "https://www.dropbox.com/s/q8lax9ary32c7t9/pytorch_model.bin?dl=0#"
mv pytorch_model.bin\?dl\=0 pytorch_model.bin
```

### to run
```
python3 trainer_hrlce.py -glovepath glove.840B.300d.txt
```

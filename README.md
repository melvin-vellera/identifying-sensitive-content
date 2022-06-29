
# identifying-sensitive-content
 

### <span style="color:blue">Introduction:</span>
Today a large part of our interactions with the world are done online. Whether it is zoom calls, tweets, comments on instagram and facebook. Technology made it super easy for everyone to express their opinions and engage in discussions online. But, these online interactions also bring their own challenges. The anonymity of online makes it easy for people to post insensitive and inappropriate comments. Such comments can spoil the dialogue and cause emotional distress. The online platforms are constantly striving to keep the discussions healthy by flagging such content and removing it. Here we aimed to train a machine learning model to label a comment based on it’s contents. The comment can have zero are multiple labels from the label list [toxic, severe_toxic, obscene, threat, insult, identity_hate]. A comment which is not flagged with any of these labels is a clean comment


### <span style="color:blue">What we did:</span>
We built multi label classification models using LSTM and Bert Hugging Face and trained it on the training data.
We experimented with both pretrained embeddings and initialising new embeddings.
Used the validation set for hyperparameter tuning and model selection.
Reported the metrics on a test set as generalisable metrics

### <span style="color:blue">Data Exploration:</span>

We used the kaggle data set from the toxic comment classification challenge: https://www.kaggle.com/competitions/jigsaw-toxic-comment-classification-challenge

### <span style="color:blue">Cleaning the data:</span>

Cleaning: We cleaned the text by removing symbols, hyperlinks, spaces, non alphanumeric characters etc
Removing the stop words: Removed the stop words such as is, am, and etc, this helps the model focus more on the salient words by not having to focus on the stop words.

### <span style="color:blue">Lemmatizing: </span>
Lemmatizing brings different forms of the word into one form, so that they are treated as a same word. For example words such as focussed, focussing, focuses, focus will all be lemmatized as same word.This is an important step in the preprocessing of the textual data.
Tokenizing: We need to tokenize the text so as to convert the text into categorical variables. This can be done in multiple ways. One of the ways is doing word tokenisation or sub word tokenisation. For LSTM we used work tokenizing where as for BERT we used the in built tokenizer. We removed the infrequently occurring words in the corpus to simplify training.

### <span style="color:blue">Encoding: </span>
We created a dictionary mapping all unique tokens to numbers and encoded the comments with the corresponding number for each token in the comment. This step is not required for BERT as we used pretrained embeddings for tokens.

### <span style="color:blue">Padding:</span>
 We chose 200 as the maximum sequence length based on the length of the comments. So the sequences are truncated if they have more than 200 tokens. It is important to maintain a fixed length for each sequence so that they can be batched together.
To achieve this we made all the sequences to be of length 200 by padding zeros in the front for comments that have fewer tokens.

### <span style="color:blue">Class imbalance Handling:</span>
<img width="606" alt="label frequency" src="https://user-images.githubusercontent.com/8666530/176560642-f5beee2d-45f3-4766-b512-456b7bb73eb6.png">
 The classes are heavily imbalanced with clean comments forming the majority percentage of all comments. We handled it in two ways.
One is by giving weights to the loss function, weighing the infrequent classes with higher weights. Other method is using a macro F1 score as a metric. Macro F1 score calculates the F1 score for each class individually and then takes an average of all such individual scores. This helps in giving equal weights to the classes.
We compared the performance of our models with and with out using the weights. 
### <span style="color:blue">Performance:</span>


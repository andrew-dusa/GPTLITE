# GPTLITE
## Decoder only GPT based on the architecture from Attention Is All You Need ##
GPTLite is a simplified, decoder-only implementation of the Transformer model that was introduced in the paper [Attention Is All You Need](https://arxiv.org/pdf/1706.03762). This model leverages self-attention and multiheaded-attention mechanisms in order to generate text based on an input document.

## Key Features ##
- **Decoder-Only Architecture:**
  - This simplified structure makes this model ideal solely for text generation tasks.
- **Self-Attention mechanisms:**
  - Self attention enables a model to weigh the value of different words from the input text differently based on their percieved relevance to the model.
- **Multi-Headed Attention:**
  - Multiheaded attention allows a model to focus on multiple different parts of an input sequence at the same time. This enhances the model's understanding of the text and improves generation. 
## Sample Output ##
```
Presently, he told him all at once, and find him on his seat.
Then you sailed to Telemachus, “Call now, Madam, wife of Ulysses, indeed
ships in the cave, he took the sea and drink offerings to the
doors. When, however, he the stool had reclined the fury of his mantle, and
fed against his due saying; then he said to the town, side the seat
that he had left, and keeping the stay him from the roots of the
doorway, and then would have gone again dinner reach one long with me,
for he could not help for she might be as a killed and so
spokilful with she giving hims abound his son.
```
This was trained on a [The Odyssey](https://www.loc.gov/item/10000284/) from the Library of Congress using 85 million parameters.

# What is Self-Attention? #
Self-Attention is a type of attention mechanism that relates different positions of an input sequence in order to compute a representaion of the sequence. It allows each position in the sequence to 'attend' to all of the other positions in the sequence. This is different from LSTM models because in self-attention the mechanism is used within the same sequence instead of being applied between encoder and decoder layers.

# What is Multi-Head Attention #
"Multi-head attention allows the model to jointly attend to information from different representation subspaces at different positions" (Vaswani et al., 2017, p. 5). What this means is that each head will independently compute a set of attention scores that allows the model to learn different aspects of the input data. We then concatenate the outputs from the heads and transform them into our expected format.
- ## Details ##
- Projection:
  - the input embeddings get transformed into three vectors: key, query and value.
- Scaled Dot-Product Attention:
  - The model uses the key and query vectors to compute attention scores, which are then scaled by the square root of the dimension of the key vectors.
  <img width="362" alt="Scaled Dot-Product Attention" src="https://github.com/user-attachments/assets/905a9f99-78e8-4e2d-9922-7f74b6f4ce87">

# Encoder/Decoder Models #
This model is a decoder only model. The transformer was initially developed as an encoder-decoder model to improve the performance of machine translation tasks as demonstrated in the paper [Attention Is All You Need](https://arxiv.org/pdf/1706.03762). This consists of two stacks of layers, one is responsible for encoding the input sequence and the other is responsible for decoding it. This is important in machine translation because the input and output sequences differ.
Decoder-only models, such as GPTLite only focus on generation tasks based on an input file. It relies on an attention mechanism that is unidirectional as opposed to bidirectional. Each tokem in the output sequence can attend to the previous tokens but not the future ones. This is suitable for tasks where the goal is to predict the next token in a sequence given the ones that came before it.
## Below is an image of the stack used in "Attention Is All You Need", My implementation does not use the left stack as it is decoder only ##

  <img width="578" alt="Encoder-Decoder Stack" src="https://github.com/user-attachments/assets/e606d050-eee9-42a5-a07a-c09c9ea97819">

# Use #
Using my implementation is fairly simple. first make sure you have Numpy and Pytorch installed and you have a text file that contains the information you want to train on.
You can tweak the hyperparameters as you wish but me wary of using too much VRAM on your CPU. Also make sure to change the file_path variable to the name of your file that you want to train on. I trained GPTLITE on an RTX 4080 and it took around 1 hour. My Implementation uses 85 million parameters.
## Credits ##
This project is based on Andrej Karpathy's YouTube series "Neural Networks: Zero to Hero" (https://www.youtube.com/playlist?list=PLAqhIrjkxbuWI23v9cThsA9GvCAUhRvKZ)

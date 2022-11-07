# VisualPretrainedLM
Some summary about the details of Pretrained Language Models and VisualPLMs.

## [BART](https://arxiv.org/pdf/1910.13461.pdf)
Seq2seq strcuture:   
Encoder: Bi-directional encoder, 
Decoder: Autoregressive deocer, the first input token is BOS token. **Each layer of the decoder is corss-attended with the final hidden states of the encoder.** For fine-tuning, an uncorrupted document is input to both the encoder and decoder, and we use representations from the final hidden state of the decoder.
Pretrain tasks: Token masking/deletion, Sentence permutation, Document rotation, text infilling. 
Finetune methods: 
 - Seq classification: Same input to the encoder and decoder. The final hidden state of the decoder is passed to a linear classifier.
 - Token classification: Same input to the encoder and decoder. The hidden state of the last layer of the decoder is used for that corresponding token.
 - Seq Generation: Text input to the encoder, decoder generate in autoregressive manner.
 - MT: Additional randomly initialized encoder which translate the input language into noisy 'English', which is passed to the encoder as input. 

# VisualPretrainedLM
Some summary about the details of Pretrained Language Models and VisualPLMs.

## [BART](https://arxiv.org/pdf/1910.13461.pdf)
Motivation: To generalize the BERT/GPT to adapt to various tasks. 
Seq2seq strcuture:   
**Encoder**: Bi-directional encoder.  
**Decoder**: Autoregressive deocer, the first input token is BOS token (*<start>*). **Each layer of the decoder is corss-attended with the final hidden states of the encoder.** For fine-tuning, an uncorrupted document is input to both the encoder and decoder, and we use representations from the final hidden state of the decoder.
Pretrain tasks: Token masking/deletion, Sentence permutation, Document rotation, text infilling.  
Model Size: Base: 6 layers for both encoder and decoder. Large: 12 layers. Dimension for each layer: 1024.   
Finetune methods: 
 - Seq classification: Same input to the encoder and decoder. The final hidden state of the decoder is passed to a linear classifier.
 - Token classification: Same input to the encoder and decoder. The hidden state of the last layer of the decoder is used for that corresponding token.
 - Seq Generation: Text input to the encoder, decoder generate in autoregressive manner.
 - MT: Additional randomly initialized encoder which translate the input language into noisy 'English', which is passed to the encoder as input. 

## ViT 
 
## [ClipCap](https://arxiv.org/pdf/2111.09734.pdf)  
 **Motivation**: Most models that deal with image captioning task follow the encoder-decoder structuere, which requires connections between visual and textual features and it is expensive. Therefore, it is desirable to develop a faster paradigm.  
 **Method**: Map the CLIP embedding to the textual embedding space with a fixed-length. Concate the caption embedding and the visual embedding. The training objective is to autoregressively predict the caption tokens conditioning on prefix.  
 Freeze the CLIP and the LM and only train the mapping network rather than fine-tuning the whole LM. The mapping network is MLP when LM is not freezed, while transformer is chosen when LM is freezed.  
 During inference, caption tokens are predicted based on the visaul embeddings.  
 **Difficulty**: **The transferring between CLIP features and LM features**, as their latent spaces are independent and a mapping network is needed. 

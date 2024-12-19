# LLM model based on chatGPT

Made with Python, Pytorch, and Jupyter Notebooks <br />
This is an LLM based on the gpt2 code and gpt3 papers. Inside the folders are two other models used for learning concepts <br />
nanoGPT is used to learn the general structure. It doesn't use the concept of tokens, using only the characters to determine the next best character. It is trained on the dataset [Tiny Shakespeare](https://raw.githubusercontent.com/karpathy/char-rnn/master/data/tinyshakespeare/input.txt). <br />
tokenizerGPT is used to learn the concept of tokens. It uses the same structure as nanoGPT but adds self-tokenization, adding extra tokens for the most common pairs. More tokens can be added, but depending on the dataset it might lead to overfitting The web-scrapping for wikipedia as well as the tokenizing happens in tokenizer.ipynb, in which it uses wikipediaapi to scrape all the websites read from input.txt and writes it to output.txt.<br />
train_my_gpt.py is the file that contains the code for a CPU based model. It can use many sources of input, depending on the file specified in DataLoaderLite. It is currenlty using Discord data, scrapped using readDiscord.py. There is code to get Fineweb, Hellaswag, and Reddit (from the pushshift torrent) data. It uses concepts from both nanoGPT and tokenizerGPT as well as the tiktoken database (the one used in gpt2) to formulate tokens. All models can be saved to a .pth file which it can setup in the next iteration, as well as being able to train and test inputs. 

# How it works
To use nanoGPT, running the code will allow it to run. Change the device to GPU if accessible. <br />
For tokenizerGPT, the current webpages it will read from are specified in the input.txt file. To change, rewrite the input.txt files with the proper Wikipedia article names and run the first block in tokenizer.ipynb. Run the second block to tokenize it as required. To run the code, change the `saved_model` parameter to whatever .pth you want it to be named, and it will save the current weights there. Switch it from testing to True and run the code. If you want to just see outputs, switch it to false. <br />
For the main GPT, for discord, refer to this [video](https://www.youtube.com/watch?v=xh28F6f-Cds) to learn how to use the code, then run it as many times, making sure not to abuse it. For reddit, refer to this [post](https://www.reddit.com/r/pushshift/comments/1akrhg3/separate_dump_files_for_the_top_40k_subreddits/). For Hellaswag and Fineweb, run the code and it will download. To train, make sure to switch the file location in DataLoaderLite to the corresponding .txt file you will be pulling text from. The model will save the weights into the file that corresponds to the `saved_model` value. Refer to the `train_GPT2.py` file for more detailed instructurns for multiple files or using multiple GPUs. <br/>

# Basis

Model is based on the model in the paper [Attention is all you need](https://arxiv.org/abs/1706.03762) on page 3. It uses [gpt2](https://github.com/openai/gpt-2) as well as [openAI research papers](https://openai.com/news/research/?limit=27) for information as well. Attention in the final model is switched to the [Flash Attention](https://arxiv.org/abs/2205.14135) and [Flash Attention 2](https://arxiv.org/abs/2307.08691) papers, which help speed up the training. Credits to [Andrej Kaparthy](https://www.youtube.com/@AndrejKarpathy/videos) for the inspiration for the code.

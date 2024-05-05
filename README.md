# Phi-1_5-kotlin-method-completion
The pipeline for fine-tuning phi-1_5 for method completion in Kotlin is the following:
- Parse desired repository written in Kotlin into a dataset:
     -  Pull the repository into "Kotlin" directory
     -  Run all the cells in dataset_parses.ipynb, which extract functions' names and       bodies and saves them in .json file
- Train the model:
     - Run all the cells in train.ipynb changin training parameters and configs if desired
     - push the model into hf, for easy later use
- Evaluate:
     - Run all the cells in evaluate.ipynb
     - add any charts as desired (sample code is provided)
 


Summary of Author's results:
- I performed a traing on training parameters present in train.ipynb file
- Only a part of the whole dataset (<50%) was used because of compute limitations
- While evaluating model on python, I was not using the docstring, I wanted python to go head to head with kotlin, thus passing only the name of the function as a prompt
- Data analysis:
    - Model improved on both Kotlin data (rogueLsum: 21%, rogueL: 20.6%, rogue2: 64%, rogue1: 22,6%) and Python data (rogueLsum: 6%, rogueL: 8.5%, rogue2: 4.4%, rogue1: 7,6%) despite not much compute
    - Model was performing 2x better on Python than on Kotlin - which was expected, as it was pretrained on unproportionally much more data than fine-tuned on
    - Increases in Python performance are a little bit suprising - I was expecting less. Maybe that is because, even tough Phi was trained to complete Python methods, it was trained to do so in a "code completion format", which I was not utilising by prompting only function names


Next possible steps:
 - Try newer version of phi
 - Perform the training on more data and more epochs (not just 2, like I did)
 - Analyze the data using different metrics (e.g. Bleu)


Notes:
- The charts for data anaylsis can be found in Examples/
- The fine-tuned model can be found in /Examples nad /megajajo/phi-1_5-finetuned on hugging face
- I was parsing "https://github.com/JetBrains/kotlin" repository, part of the parsed data can be found in /Examples
- for Python evaluation I was using CodeXGLUE Python method completion dataset

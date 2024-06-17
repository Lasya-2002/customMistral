This is a fine tuned version of Mistral 7B LLM on GST laws of INDIA. Mistral needs A100 or A100-80G for fine tuning on our data with LoRA or QLoRA adaptation. The GST laws data is collected from publicly available pdf files. The 2019 documentation is collected from the following link [GST 2019 data](https://gstcouncil.gov.in/sites/default/files/GST-Concept%20and%20Status01062019.pdf) and the 2024 updated laws is collected from the official GST website [GST data 2024](https://gstcouncil.gov.in/overview-gst-english). The mistral model is imported and used from the hugging face hub, using the transformers library.

# LMQG

LMQG is a python library which can be used to use and generate question and answers from the raw text. T5 based model is used for generating questions from the model. The model used is 'lmqg/t5-base-squad-qag'. To refer about it, you can check out [lmgq](https://github.com/asahi417/lm-question-generation).The generated question and answers were combined and one large dataset was constructed.

# Mistral setup

1. Before we get started with mistral, it is quite important to import the necessary libraries like transformers, BitsAndBytesConfig, peft, torch.
2. Login to the hugging face hub by passing the appropriate token to access and also upload the model to the hub.
3. Now set up the quantization of the model by loading it in 4-bit format but compute in bfloat16 to make up for the quatization. 
4. Now load the datasets for training and validation and start the training process using the transformers.trainer() class by loading the appropriate parameters.
5. After the training process is complete, it is quite necessary to save the model.
6. Now you can upload the model using the trainer.push_to_hub(). If you wish to use this model, you can load it from the transformers hub by using the peft configuration. Since we are using the LoRA configuration to run the training process, it gives us an adapter rather than a model.

The model is now ready to use. You can directly import it from the huggingface hub using the peft.PeftModel().

